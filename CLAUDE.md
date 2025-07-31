# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Neovim configuration based on kickstart.nvim - a well-documented starting point for Neovim setup. The configuration uses Lua and the lazy.nvim plugin manager.

## Architecture

- **init.lua**: Main configuration file containing all core settings, keymaps, and plugin specifications
- **lua/kickstart/**: Contains modular plugin configurations that extend the base setup
- **lua/custom/plugins/**: User-specific plugin additions (bufferline, fugitive, lualine)
- **lazy-lock.json**: Plugin version lockfile for reproducible installs

## Key Configuration Structure

### Core Components
- **Plugin Manager**: lazy.nvim with automatic installation
- **LSP**: Full LSP setup with mason.nvim for automatic server installation
- **Completion**: blink.cmp with LuaSnip for snippets
- **File Explorer**: neo-tree.nvim
- **Fuzzy Finding**: telescope.nvim with fzf-native extension
- **Git Integration**: gitsigns.nvim + vim-fugitive
- **Formatting**: conform.nvim with format-on-save
- **Syntax Highlighting**: nvim-treesitter

### Plugin Loading Pattern
The configuration uses lazy.nvim's modular loading:
1. Core plugins defined in init.lua
2. Kickstart modules loaded via `require 'kickstart.plugins.*'`
3. Custom plugins imported via `{ import = 'custom.plugins' }`

## Common Commands

### Plugin Management
- `:Lazy` - Open plugin manager interface
- `:Lazy update` - Update all plugins
- `:Mason` - Open LSP server/tool manager

### LSP & Development
- `:checkhealth` - Check Neovim configuration health
- `:ConformInfo` - Check formatter configuration
- `<leader>f` - Format current buffer
- `grn` - LSP rename
- `gra` - LSP code action
- `grd` - Go to definition

### File Operations
- `<leader>sf` - Search files
- `<leader>sg` - Live grep
- `<leader>sn` - Search Neovim config files
- `<leader><leader>` - Find buffers

## Configuration Guidelines

### Adding New Plugins
Add plugins to `lua/custom/plugins/` as separate .lua files following the lazy.nvim plugin spec format. Each file should return a plugin configuration table.

### LSP Configuration
LSP servers are managed through mason.nvim. Add new servers to the `servers` table in init.lua:708 and they will be auto-installed.

### Key Mapping Conventions
- `<leader>` is space
- `gr*` prefix for LSP operations (go to references, rename, etc.)
- `<leader>s*` prefix for search operations
- `<leader>t*` prefix for toggle operations

### External Dependencies
Ensure these tools are installed for full functionality:
- `git`, `make`, `unzip`, C compiler
- `ripgrep`, `fd-find` for telescope
- Clipboard tool (xclip/xsel)
- Nerd Font (set `vim.g.have_nerd_font = true` in init.lua:94)

## Important Notes

- This is a single-file configuration (init.lua) by design for educational purposes
- The configuration automatically installs missing plugins and LSP servers on first run
- Custom modifications should be made in `lua/custom/` to avoid conflicts with kickstart updates
- All plugins use lazy loading for optimal startup performance