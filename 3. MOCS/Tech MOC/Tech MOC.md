---
created: 2023-09-24T12:21
updated: 2025-10-05T16:02
---
>[!note] Programming Tools
>- [[Git]]
>- [[Nvim]]

>[!note] Personal Websites
>- [[Quartz]] 
>  [[My Quartz Setup Process]]
>- [[Jekyll]]

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

