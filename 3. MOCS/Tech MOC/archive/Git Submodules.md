---
created: 2024-03-09
related:
  - "[[Git]]"
completed: 
type: 
updated: 2024-05-27T13:29
---
---
how to use a git hub repository as a other git hub repository directory

To use a GitHub repository as a directory in another GitHub repository, you can add the first repository as a submodule in the second repository. Here’s how to do it step-by-step:

1. Clone the second repository to your local machine using the following command:
    
    ```shell
    git clone https://github.com/your-username/second-repo.git
    ```
    

Navigate to the cloned repository:

```shell
cd second-repo
```

Add the first repository as a submodule. Replace `https://github.com/your-username/first-repo.git` with the actual URL of the first repository you want to add as a submodule.

```shell
git submodule add https://github.com/your-username/first-repo.git
```

or 

```shell
git submodule add https://github.com/username/repo.git path/to/directory
```

Commit the changes to the second repository:

```shell
git commit -m "Add first-repo as a submodule"
```

Push the changes to the remote repository:

```shell
git push
```

Now, the first repository will be included as a directory in the second repository. You can access its contents by navigating to the submodule directory (e.g., `cd first-repo`) within the second repository.

Remember that submodules have their own separate repository history, so you’ll need to manage their updates separately. To update a submodule to the latest commit on its default branch, run:

```shell
git submodule update --remote first-repo
```

If you want to update the submodule reference in the parent repository, commit and push the changes to the parent repository:

```shell
git add first-repo
git commit -m "Update first-repo submodule reference"
git push
```

By using this approach, you can effectively use a GitHub repository as a directory in another GitHub repository.