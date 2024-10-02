---
link: https://catcodeme.github.io/1100_blog_content/others/publish-workflow
site: "@catcodeme.github.io"
excerpt: union quartz and obsidian to publish your notes to github page.
twitter: https://twitter.com/@hulj13
slurped: 2024-10-02T19:34
title: publish workflow
---

> Based on the [quartz](https://quartz.jzhao.xyz/) and [ccm-publisher](https://github.com/CatCodeMe/ccm-publisher) plugins, publish Obsidian notes to GitHub Pages.
> 
> - Use `submodule` to completely separate the compilation and publishing of blog content, making it more flexible and convenient.

> 1. This article uses `quartz_demo` as the compilation library for Quartz.
> 2. In practical applications, your repository name (compilation repo) should be `yourname.github.io`
> 3. Use `content_demo` as the notes repository, here we’re using `content_demo` for illustration.

## TLDR

1. Prepare the Quartz environment, refer to [Quartz: Get Started](https://quartz.jzhao.xyz/), as the compilation library.
    - Pay attention to modifying the **baseUrl** to `yourname.github.io` in the `quartz.config.ts` configuration file， `base_url` item.
2. Prepare an empty repository for uploading your notes (notes repository).
    - At least one **index.md** file is required in the root path.
3. Copy GitHub Action configuration files.
    1. Copy and **configure** this action [configuration file](https://github.com/CatCodeMe/catcodeme.github.io/blob/v4/.github/workflows/deploy.yml) to the **compilation library**.
    2. Copy and **configure** this action [configuration file](https://github.com/CatCodeMe/blog_from_obsidian/blob/main/.github/workflows/deploy.yml) to the **notes repository**.
4. Try pushing notes to the notes repository and check if both libraries’ actions succeed.
5. Once all actions have been executed successfully, go to `yourname.github.io` to see the effect.

## Operation Steps

### Preparation of Environment

1. Prepare the Quartz environment, refer to [Quartz: Get Started](https://quartz.jzhao.xyz/).
2. Initialize your own Quartz compilation library, which should be called `yourname.github.io`, replacing `yourname` with your GitHub account name.
    
    - Refer to [Quartz: Setting up your GitHub repository](https://quartz.jzhao.xyz/setting-up-your-GitHub-repository).
    - Up to this point, running `git remote -v` locally will yield the following result:
        - quart_demo[1](https://catcodeme.github.io/1100_blog_content/others/publish-workflow#user-content-fn-1) (quartz_demo is for illustration purposes; replace it with `yourname`)
    
    ```
    $ git remote -v
    # Replace quartz_demo with your own yourname.github.io
    origin	git@github.com:CatCodeMe/quartz_demo.git (fetch)
    origin	git@github.com:CatCodeMe/quartz_demo.git (push)
    upstream	https://github.com/jackyzha0/quartz.git (fetch)
    upstream	https://github.com/jackyzha0/quartz.git (push)
    ```
    
3. As with previous steps, initialize another empty repository on GitHub, used for uploading your Obsidian notes, let’s call it `content_demo`[2](https://catcodeme.github.io/1100_blog_content/others/publish-workflow#user-content-fn-2).
    - Only initialization is needed here; no further operations are required, like this:  
        ![20240322-publish_init_content.png|633](https://catcodeme.github.io/img/user/999_repository/20240322-publish_init_content.png)

### Configure Submodule

1. Starting from this step, distinguish from the official single-library publishing method. We’ll use `submodule`.
2. Configure submodule.

```
$ cd quartz_repo
$ git rm -r --cached content
# Replace CatCodeMe/content_demo.git with the path to your own repository
$ git submodule add git@github.com:CatCodeMe/content_demo.git content
$ git commit -m "add submodule"
$ git push
```

3. At this step, the `quartz_demo` repository and the `content_demo` repository are connected using submodule; the blue links may be different, which is normal. If clicking on the content folder takes you to the `content_demo` repository, it means the configuration is successful.  
    ![20240324-publish_add_submodule.png](https://catcodeme.github.io/img/user/999_repository/20240324-publish_add_submodule.png)

### Configure GitHub Actions for Automatic Compilation

> For beginners, you can follow the subsequent steps. If you are familiar with the github action , you can directly refer to and adjust these files. [notes repo action config](https://github.com/CatCodeMe/content_demo/blob/main/.github/workflows/deploy.yml) and [compilation repo action config](https://github.com/CatCodeMe/quartz_demo/blob/v4/.github/workflows/ci.yaml)

#### Configure Notes Repository (content_demo)

> You can do it directly on GitHub, or if you prefer Git client tools, you can clone it to your local machine for operation.

Create a new file (click the `create a new file` blue link above), called `.github/workflows/deploy.yml`.

- **The folder path must be `.github/workflows` , and the file extension must be `.yml`**. The filename doesn’t matter as long as it meets GitHub’s requirements.
- For `deploy.yml`, you can refer to [deploy.yml](https://github.com/CatCodeMe/content_demo/blob/main/.github/workflows/deploy.yml); after copying and modifying the content, click the `commit` button in the upper right corner to save the current file.  
    ![20240322-publish_zh_yml.png](https://catcodeme.github.io/img/user/999_repository/20240322-publish_zh_yml.png)
    - Replace `repo` option with the name from step 2, structured as `yourname/yourname.github.io`.
    - The `token` option is the GitHub authentication token, pay attention when using it.
        1. `${{ secrets.gh_action_token_PAT}}` In this setting, `gh_action_token_PAT` is a custom token name that you can decide on. It’s better not to use Chinese or spaces.
        2. Generate the token [here](https://github.com/settings/tokens?type=beta) (it’s better to open it in a new tab in your browser for convenience).  
            ![20240323-publish_start_generate_token.png](https://catcodeme.github.io/img/user/999_repository/20240323-publish_start_generate_token.png)
        3. Choose which repositories this token can access.  
            ![20240322-publish_select_repo.png](https://catcodeme.github.io/img/user/999_repository/20240322-publish_select_repo.png)
        4. Set token permissions; scroll down on the current page; expand `Repository permissions`, find `Actions` and `Contents`, and set Access to `Read and write`.
        5. Click `generate token` (❗️**Copy and save this generated token somewhere else first, as you will need it later**). If you forget, you can redo steps 3-5 to generate a new token.
        6. After copying it, you can refresh the page or click the left navigation bar again to enter the `Fine grained tokens` page, select and click on the token you just generated, and you will see something similar to the screenshot below.  
            ![20240324-publish_token_settings.png](https://catcodeme.github.io/img/user/999_repository/20240324-publish_token_settings.png)
        7. Go back to the homepage of the repository `content_demo`, click the `settings` tab, enter the settings page, and add the authorization of the token you just generated to the current repository. Click `New repository secret` button.  
            ![20240322-publish_add_token_repo.png](https://catcodeme.github.io/img/user/999_repository/20240322-publish_add_token_repo.png)
        8. Add TokenNext, add the token, **pay attention to**:
            1. The `Name` must be consistent with the `gh_action_token_PAT` name in acition config file(`.yaml`). Of course, if you are using a different name, just modify the configuration of `.github/workflows/deploy.yml` to match the `Name` here.
            2. The `Secret` **is the token you copied and saved earlier**.
            3. Once set, click `Add secret` to save.  
                ![20240322-publish_add_token_repo_2.png](https://catcodeme.github.io/img/user/999_repository/20240322-publish_add_token_repo_2.png)
        9. Once this is done, the actions for the current repository should be configured. At this point, the repository structure should look like this:  
            ![20240322-publish_content_repo_demo.png](https://catcodeme.github.io/img/user/999_repository/20240322-publish_content_repo_demo.png)

#### Configure Quartz Compilation Repository

1. Go back to the `quartz_demo` repository and directly modify the `ci.yaml` file content after cloning the original repository (quartz).
    1. Like the notes repository, this file must also be in the `.github/workflows/` folder, with no specific name requirements.
    2. You can either overwrite the content of `ci.yaml` directly or delete it and create a new YAML configuration file.
2. Here, we choose to modify it.
    - Use the content after modification from my [configuration file](https://github.com/CatCodeMe/quartz_demo/blob/v4/.github/workflows/ci.yaml).
    - only on point need to update, `token name`, `gh_action_token_PAT` need to same as your config  
        ![20240324-pulish_quartz_action_token.png](https://catcodeme.github.io/img/user/999_repository/20240324-pulish_quartz_action_token.png)

#### Configuration Completion

- With all configurations completed, try publishing notes to the `content_demo` repository and check if the actions (which by default will send notifications to your GitHub email) are successful.
- Then, check your target webpage at `https://yourname.github.io`.

## Pros and Cons

### Pros

- Using the submodule pattern enables complete separation between notes and compilation tools. Even if you migrate to other tools later, theoretically there should be no impact.
- All processes are automated after configuration. All you need to do is write notes, publish them to the notes repository, and wait for them to take effect.
    - You can use Obsidian’s plugin for publishing notes; here, I recommend my own developed [ccm-publisher](https://github.com/CatCodeMe/ccm-publisher) plugin.

### Cons

- Does not support local preview; this can be resolved with Obsidian plugins.
    - The ccm-publisher plugin is currently under development for this feature, so stay tuned.

1. [quartz_demo repo](https://github.com/CatCodeMe/quartz_demo) [↩](https://catcodeme.github.io/1100_blog_content/others/publish-workflow#user-content-fnref-1)
    
2. [content_demo repo](https://github.com/CatCodeMe/content_demo.git) [↩](https://catcodeme.github.io/1100_blog_content/others/publish-workflow#user-content-fnref-2)
    

---