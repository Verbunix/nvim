### Init
To know the correct path for your system, run `:echo stdpath('config')`
- Win `~/AppData/Local/nvim/init.lua`
- Ubutnu `~/.config/nvim/init.lua`

<details>
<summary>init.lua</summary>

```
-- Bootstrap lazy.nvim
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not (vim.uv or vim.loop).fs_stat(lazypath) then
  local lazyrepo = "https://github.com/folke/lazy.nvim.git"
  local out = vim.fn.system({ "git", "clone", "--filter=blob:none", "--branch=stable", lazyrepo, lazypath })
  if vim.v.shell_error ~= 0 then
    vim.api.nvim_echo({
      { "Failed to clone lazy.nvim:\n", "ErrorMsg" },
      { out, "WarningMsg" },
      { "\nPress any key to exit..." },
    }, true, {})
    vim.fn.getchar()
    os.exit(1)
  end
end
vim.opt.rtp:prepend(lazypath)

-- Make sure to setup `mapleader` and `maplocalleader` before
-- loading lazy.nvim so that mappings are correct.
-- This is also a good place to setup other settings (vim.opt)
vim.g.mapleader = " "
vim.g.maplocalleader = "\\"

-- Setup lazy.nvim
require("lazy").setup({
  spec = {
    -- add your plugins here
    {
      "vhyrro/luarocks.nvim",
      priority = 1000, -- Very high priority is required, luarocks.nvim should run as the first plugin in your config.
      config = true,
    },
    {
      "nvim-neo-tree/neo-tree.nvim",
        keys = {
          { "<leader>ft", "<cmd>Neotree toggle<cr>", desc = "NeoTree" },
        },
        opts = {},
    },
    { "nvim-tree/nvim-web-devicons", lazy = true },
    { "williamboman/mason.nvim" },    
  },
  -- Configure any other settings here. See the documentation for more details.
  -- colorscheme that will be used when installing plugins.
  install = { colorscheme = { "habamax" } },
  -- automatically check for plugin updates
  checker = { enabled = true },
})
```

</details>

### Package manager lazy.nvim
[lazy.folke.io](https://lazy.folke.io/installation)

Use health check install in nvim:
```
:checkhealth lazy
```

### Install Lua(luarocks.nvim)
- Win:
```
https://github.com/rjpcomputing/luaforwindows
```
- MacOS (brew):
```
brew install luajit
```
- Ubuntu (apt):
```
sudo apt install liblua5.1-0-dev
```
