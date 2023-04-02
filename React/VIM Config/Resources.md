# Setting up the Terminal
[Video](https://www.youtube.com/watch?v=CF1tMjvHDRA)

# Joseans' Githhub Repo

[Link](https://github.com/josean-dev/dev-environment-files)

# LSP servers

[Link](https://github.com/williamboman/mason-lspconfig.nvim)


# AstroNvim Config

I decided after fiddling around a lot with Josean's config to go with [AstroNvim](https://github.com/AstroNvim/AstroNvim), it has a ton of functionality out of the box and doesn't seem to be as buggy as Josean's config.

I followed this [video](https://www.youtube.com/watch?v=GEHPiZ10gOk) to config most of the custom settings.

I had an issue after installing AstroNvim, when opening any of the `.lua` files, `treesitter` will complain about not able to highlight something, I fixed it by installing `lua` lsp:

```bash
:TSInstall lua
```

