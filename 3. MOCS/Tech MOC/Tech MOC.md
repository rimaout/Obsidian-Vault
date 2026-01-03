---
created: 2023-09-24T12:21
updated: 2025-12-15T10:25
---
>[!note] Programming Tools
>- [[Git]]
>- [[Nvim]]
>-  [[MacOS Setup]]

>[!note] Personal Websites
>- [[Quartz]] 
>  [[My Quartz Setup Process]]
>- [[Jekyll]]

---

Docker environments commands:
- `brew services start colima`
- `brew services stop colima`
- `docker ps`
- `docker stop <container-id>`
- `docker system prune -a --volumes`
- `devcontainer build --workspace-folder .`
- `devcontainer exec --workspace-folder . bash/zsh`
- `devcontainer up --workspace-folder .`
- `devcontainer up --mount "type=bind,source=$HOME/.config/nvim,target=/home/vscode/.config/nvim" --workspace-folder .`

To remove a built image, you can use the `docker rmi` command followed by the image ID or the image name. Here are the steps:
1. **List all Docker images**: Run the command `docker images` to list all Docker images on your system.
2. **Find the image ID or name**: Look for the image you want to remove and note its ID or name.
3. **Remove the image**: Run the command `docker rmi <image_id>` or `docker rmi <image_name>`.

