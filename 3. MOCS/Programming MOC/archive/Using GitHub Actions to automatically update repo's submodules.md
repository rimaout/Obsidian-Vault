---
type: Programming Note
programming language: "[[Git]]"
related:
  - "[[Quartz Setup]]"
completed: false
created: 2024-12-08T10:34
updated: 2024-12-09T11:16
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


---
## 3. Create workflow inside the child repository


---
## 4. Create workflow inside the parent repository

