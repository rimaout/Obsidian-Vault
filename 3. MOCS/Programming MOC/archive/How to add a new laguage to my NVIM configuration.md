---
type: Programming Note
programming language: "[[Nvim]]"
related: 
completed: false
created: 2024-07-10T12:12
updated: 2024-07-10T12:50
---
>[!abstract] Index
>1. 

>[!abstract] Related
>- 

---

## Syntax Highlighting

I use **treesitter** for syntax highlighting and since the auto install feature is activated you don’t need to do anything. Every time a new laguage is detected the syntax highlighter is automagicaly installed.

But if you want you can add it to the `ensure installed` section:
1. go to `treesitter.lua`.
2. find the `ensure installed` section.
3. add the name of the programming language.

>[!note]- Configuration Code
>```lua
>return {
>    "nvim-treesitter/nvim-treesitter",
>    build = ":TSUpdate",
>
>    config = function()
>        local config = require("nvim-treesitter.configs")
>        config.setup({
>            auto_install = true, -- automatically install syntax highlighters
>            ensure_installed = { "vim", "lua", "python", "rust", "java", "c" },
>            highlight = { enable = true },
>            indent = { enable = true }
>        })
 >   end
>}
>```

---
## LSP

I use **mason** and **mason-lsponfig** for using and managing and installing language servers. To add a new laguage server in my configuration you just need to:
1. go to `lsp-config.lua` file.
2. find the `MASON-LSPCONFIG` section.
3. add the new laguage server to the list `ensure installed`.

>[!note]- Configuration Code
>```lua
>-- MASON-LSPCONFIG (list of lsp to install) --
>    {
>        "Williamboman/mason-lspconfig.nvim",
>        config = function()
>            require("mason-lspconfig").setup({
>                ensure_installed = {
>                    "lua_ls",  -- lua language server
>                    "pyright", -- python language server
>                    "jdtls",   -- java language server
>                },
>            })
>        end,
>
>    },
>```
