---
type: Programming Note
programming language: "[[Git]]"
related:
  - "[[Quartz Setup]]"
completed: true
created: 2024-12-08T10:34
updated: 2025-01-17T18:29
---

>[!abstract] Related
>- [[Git]]
>- [[Quartz Setup]]

---
## Introduction

We will create a workflow that automatically updates the submodule inside the *parent repository* each time the *child repository* (submodule) is updated.
- ***Parent Repository:*** The repository that contains the submodule as a directory.
- ***Child Repository:*** The repository that is used as a submodule.

This is the basic structure:
* A GitHub Action inside the *child repository* that notifies the *parent repository* when a change occurs.
* A GitHub Action inside the *parent repository* that is triggered by the notification from the *child repository*, reads the updated *child repository*, and updates the submodule with the new changes.

To achieve this, we need to complete the following 4 steps:
1. [[#1. Create access token|Create access token]]
2. [[#2. Save the token as a secret inside each repository|Save the token as a secret inside each repository]]
3. [[#3. Create workflow inside the child repository|Create workflow inside the child repository]]
4. [[#4. Create workflow inside the parent repository|Create workflow inside the parent repository]]

>[!note] Sources
>- [Using GitHub Actions to automatically update the repo's submodules - StackOverflow](https://stackoverflow.com/questions/64407333/using-github-actions-to-automatically-update-the-repos-submodules)
>- [Managing your personal access tokens - GitHub Docs](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)
>- [Using secrets in GitHub Actions - GitHub Docs](https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions)

---
## 1. Create access token

To begin, we need to create a token that will allow GitHub Actions to access and modify the other repository.

To create a token, follow these steps:
1. Go to the GitHub website and navigate to `Settings > Developer settings > Personal access tokens > Fine-grained tokens`.
2. Click on `Generate new token`. Alternatively, you can use this direct link: [https://github.com/settings/personal-access-tokens/new](https://github.com/settings/personal-access-tokens/new).

>***Token Name***
>
>Choose a name for your token that describes its purpose. In this example, we'll create a token to synchronize the `quartz` repository (parent) with the `obsidian-vault` repository (submodule), so we'll name it `quartz-sync`. You can choose any name that suits your needs.

>***Expiration***
>
>Select the expiration date for your token. Since the repositories in this example are public and not mission-critical, we'll choose `No Expiration`. However, you may want to set a specific expiration date depending on your security requirements.

>***Repository Access***
>
>Select the repositories that you want to grant access to. In this case, we'll choose `Only select repositories` and select the following repositories:
>
>- `Notes-In-Public` (parent)
>- `Obsidian-Vault` (child)

>***Permissions***
>
>For this workflow, we're only interested in repository permissions, not account permissions. Under `Repository permissions`, select the following permissions:
>
>- `Actions` (read and write)
>- `Contents` (read and write)
>- `Deployments` (read and write)
>- `Secrets` (read)
>- `Workflow` (read and write)
>
>**Warning:** I've selected these permissions based on my understanding of the workflow requirements, but I'm not entirely sure if they're all necessary. In fact, I'm probably over-privileging the token by granting too many permissions. If you're concerned about security, I recommend reviewing the permissions carefully and adjusting them according to your specific needs. It's essential to understand the implications of granting these permissions and to ensure that you're not over-privileging the token.

>***Generate Token***
>
>Click `Generate token` and copy the token. Save it in a secure location, such as a password manager. Make sure to clear your clipboard history to prevent any potential security risks.

---
## 2. Save the token as a secret inside each repository

Now that we have created the token, we need to save it as a repository secret inside both the parent and child repositories.

>**Parent Repository**
>
>To save the token as a secret in the parent repository, follow these steps:
>
>1. Open your GitHub parent repository (the repository that contains the submodule).
>2. Go to `Settings > Actions > Secrets`.
>3. Click on `New repository secret`.
>4. Enter a name for the secret, such as `PARENT_SUBMODULE_TOKEN`.
>5. Paste the token into the secret section.
>6. Click `Add secret`.

>**Child Repository**
>
>Repeat the same steps for the child repository (the repository used as a submodule). Use the same name (`PARENT_SUBMODULE_TOKEN`) and paste the same token.

---
## 3. Create workflow inside the child parent

Now that we have created the token and saved it as a secret, we can create the workflow in the parent repository that can be called by the child repository when a change occurs.

This workflow simply updates all the submodules present in the repo.

To create the workflow, follow these steps:
1. Open the directory of your parent repository (in my case, `Notes-In-Public`) using your preferred IDE.
2. If it doesn't already exist, create a directory called `.github`.
3. Inside the `.github` directory, create another directory called `workflows`.
4. In the `workflows` directory, create a new file for your workflow. For example, you can name it `submodule-sync.yml`.
5. Inside the file write this:

```yaml
name: 'Submodules Sync'

on:
  # Allows you to run this workflow manually from the Actions tab or through HTTP API
  workflow_dispatch:

jobs:
  sync:
    name: 'Submodules Sync'
    runs-on: ubuntu-latest

    # Use the Bash shell regardless whether the GitHub Actions runner is ubuntu-latest, macos-latest, or windows-latest
    defaults:
      run:
        shell: bash

    steps:
    # Checkout the repository to the GitHub Actions runner
    - name: Checkout
      uses: actions/checkout@v2
      with:
        token: ${{ secrets.YOUR_TOKEN }}
        submodules: true

    # Update references
    - name: Git Submodule Update
      run: |
        git pull --recurse-submodules
        git submodule update --remote --recursive

    - name: Commit update
      run: |
        git config --global user.name 'Git bot'
        git config --global user.email 'bot@noreply.github.com'
        git remote set-url origin https://x-access-token:${{ secrets.GITHUB_TOKEN }}@github.com/${{ github.repository }}
        git commit -am "Auto updated submodule references" && git push || echo "No changes to commit"
```

>**Important:** Make sure to replace `YOUR_TOKEN` with the actual name of the secret you created in [[#2. Save the token as a secret inside each repository|Step 2]] for your parent repository, in my case `PARENT_SUBMODULE_TOKEN`.

⚠️ Now commit all changes and push to your Github account.

---
## 4. Create workflow inside the child repository

The final step is to create a workflow in the child repository, this workflow activate the workflow created in [[#3. Create workflow inside the child parent|step 3]] in the parent repo, each time a change in the child is occurred.

To create the workflow, follow these steps:

1. Open the directory of your child repository (in your case, `obsidian-vault`) using your preferred IDE.
2. If it doesn't already exist, create a directory called `.github`.
3. Inside the `.github` directory, create another directory called `workflows`.
4. In the `workflows` directory, create a new file for your workflow. For example, you can name it `submodule-notify-parent.yml`.

Here's an example of what the `submodule-notify-parent.yml` file might look like:

```yaml
name: 'Submodule Notify Parent'

on:
  push:
    branches:
      - main    

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

jobs:
  notify:
    name: 'Submodule Notify Parent'
    runs-on: ubuntu-latest

    # Use the Bash shell regardless whether the GitHub Actions runner is ubuntu-latest, macos-latest, or windows-latest
    defaults:
      run:
        shell: bash

    steps:
    - name: Github REST API Call
      env:
        CI_TOKEN: ${{ secrets.YOUR_TOKEN }}
        PARENT_REPO: <you_name/your-repo>
        PARENT_BRANCH: <branch>
        WORKFLOW_ID: <your_workflow_id>
      run: |
        curl -fL --retry 3 -X POST -H "Accept: application/vnd.github.v3+json" -H "Authorization: token ${{ env.CI_TOKEN }}" https://api.github.com/repos/${{ env.PARENT_REPO }}/actions/workflows/${{ env.WORKFLOW_ID }}/dispatches -d '{"ref":"${{ env.PARENT_BRANCH }}"}'
```

>**Important:** Make sure to replace the following placeholders with your actual values:
>
>- `YOUR_TOKEN`: The name of the secret you created in [[#2. Save the token as a secret inside each repository|Step 2]] for your parent repository, in my case `PARENT_SUBMODULE_TOKEN`.
>- `<you_name/your-repo>`: The name of your parent repository, including you Github username, in my case *rimaout/Notes-In-Public* (open your Github repo page from a browser and reed the URL to get the right name)
> - `<branch>`: The branch in your parent repository that you want to update, if you are using is `main`, but if you are using using this for you [quartz](https://quartz.jzhao.xyz/) site is `v4` .
>- `<your_workflow_id>`: The ID of the workflow in your parent repository that you want to trigger, read [[#How to get a Github Workflow ID|this]] to learn how to get the workflow ID.

⚠️ Now commit all changes and push to your Github account.

---
## How to get a Github Workflow ID

To get the workflow ID, you can use the GitHub API to see the list of workflows associated with to the repository that can be accessed with a specific token.

In particular you can use this command to get the list of workflows:

```bash
curl -X GET -H "Authorization: token $YOUR_TOKEN_CODE" https://api.github.com/repos/$PARENT_REPO/actions/workflows
```

The result will be a list of workflows you have to get the ID of the workflow created in step [[#3. Create workflow inside the child repository|step 3]], just search the same name.

>**Important:** Make sure to replace the following placeholders with your actual values:
>
>- `$YOUR_TOKEN_CODE`: use the token code generate in [[#1. Create access token|step 1]].
>- `$PARENT_REPO`: The name of your parent repository, *Notes-In-Public* (open your Github repo page from a browser and look the URL to get the right name)

---
## The end

That's it! With these you should now have a working setup that automatically updates the submodule in your parent repository whenever changes are made to the child repository.