# 🗃️ Neovim project manager plugin

**Neovim project** plugin simplifies project management by maintaining project history and providing quick access to saved sessions via [Telescope](https://github.com/nvim-telescope/telescope.nvim). It runs on top of the [Neovim Session Manager](https://github.com/Shatur/neovim-session-manager), which is needed to store all open tabs and buffers for each project.

- ✅ Start where you left off last time.
- ✅ Switch from project to project in second.
- ✅ Sessions and history can be synced across your devices (rsync, Syncthing, Nextcloud, Dropbox, etc.)
- ✅ Find all your projects by glob patterns defined in config.

![Neovim project manager plugin dracula theme](https://github.com/coffebar/neovim-project/assets/3100053/b75e9373-d694-48e4-abbf-3abfe98ae46f)

![Neovim project manager plugin onedark theme](https://github.com/coffebar/neovim-project/assets/3100053/2bc9b472-071c-4975-97b0-545bd1390053)

🙏 **Neovim project manager** plugin is heavily inspired by [project.vim](https://github.com/ahmedkhalf/project.nvim)

## Usage

1. Set patterns in the [configuration](#%EF%B8%8F-configuration) to discover your projects.
2. Use [commands](#commands) to open your project. Or open nvim in the project directory. Both methods will create a session.
3. Open files inside the project and work.
4. The session will be saved before closing nvim or switching to another project.
5. Open nvim in any non-project directory and the latest session will be loaded.
   
## 📦 Installation

You can install the plugin using your preferred package manager.

<details><summary><h3>Lazy.nvim</h3></summary>

```lua
{
  "coffebar/neovim-project",
  opts = {
    -- your configuration comes here
    -- or leave it empty to use the default settings
  },
  dependencies = { "nvim-telescope/telescope.nvim", "Shatur/neovim-session-manager" },
  priority = 100,
},
{
  "Shatur/neovim-session-manager",
  lazy = true,
  dependencies = { "nvim-lua/plenary.nvim" }
},
{
  "nvim-telescope/telescope.nvim",
  tag = "0.1.0",
  dependencies = { "nvim-lua/plenary.nvim" },
}
```

</details>

<details><summary><h3>packer.nvim</h3></summary>

```lua
use {
  "coffebar/neovim-project",
  config = function()
    require("neovim-project").setup {
      -- your configuration comes here
      -- or leave it empty to use the default settings
    }
  end
  requires = { "nvim-telescope/telescope.nvim", "Shatur/neovim-session-manager" }
}

use {
  "Shatur/neovim-session-manager",
  requires = { "nvim-lua/plenary.nvim" }
}

use {
  "nvim-telescope/telescope.nvim",
  tag = "0.1.0",
  requires = { "nvim-lua/plenary.nvim" },
}
```

</details>

## ⚙️ Configuration

### Default options:

```lua
{
  -- Project directories
  projects = {
    "~/projects/*",
    "~/p*cts/*", -- glob pattern is supported
    "~/projects/repos/*",
    "~/.config/*",
    "~/work/*",
  },
  -- Path to store history and sessions
  datapath = vim.fn.stdpath("data"), -- ~/.local/share/nvim/

  -- Overwrite some of Session Manager options
  session_manager_opts = {
    autosave_ignore_dirs = {
      vim.fn.expand("~"), -- don't create a session for $HOME/
      "/tmp",
    },
    autosave_ignore_filetypes = {
      -- All buffers of these file types will be closed before the session is saved
      "ccc-ui",
      "gitcommit",
      "gitrebase",
      "qf",
    },
  },
}
```

## Commands

Plugin will add these commands:

- `:Telescope neovim-project discover` - find a project based on patterns.

- `:Telescope neovim-project history` - select a project from your recent history.


#### Telescope mappings

Use `Ctrl+d` in Telescope to delete the project's session and remove it from the history.

## ⚡ Requirements

- Neovim >= 0.8.0

## Demo video

https://github.com/coffebar/neovim-project/assets/3100053/c83ae8ab-625e-4a44-88e1-7d7e61c4bad8

## 🤝 Contributing

- Pull requests are welcome.
- If you encounter bugs please open an issue.
