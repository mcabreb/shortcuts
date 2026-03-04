# Neovim Keybindings Reference

Personal reference for common developer keybindings in Neovim, including plugin requirements and configuration.

> Leader key: `<Space>` (`let mapleader=" "`)

---

## 1. File Navigation (Telescope)

Telescope is a fuzzy finder that lets you search files, content, buffers, and more with a live preview.

### Plugins

```vim
Plug 'nvim-lua/plenary.nvim'          " required dependency
Plug 'nvim-telescope/telescope.nvim'
```

### Keybindings

| Binding | Command | Description |
|---------|---------|-------------|
| `<Space>ff` | `:Telescope find_files` | Fuzzy-find files in project (respects `.gitignore`) |
| `<Space>fg` | `:Telescope live_grep` | Search text across all files (requires `ripgrep`) |
| `<Space>fb` | `:Telescope buffers` | List and switch between open buffers |
| `<Space>fh` | `:Telescope help_tags` | Search Neovim help documentation |
| `<Space>fr` | `:Telescope oldfiles` | List recently opened files |
| `<Space>fs` | `:Telescope grep_string` | Grep the word under cursor across files |

### Configuration

```vim
nnoremap <silent> <leader>ff :Telescope find_files<CR>
nnoremap <silent> <leader>fg :Telescope live_grep<CR>
nnoremap <silent> <leader>fb :Telescope buffers<CR>
nnoremap <silent> <leader>fh :Telescope help_tags<CR>
nnoremap <silent> <leader>fr :Telescope oldfiles<CR>
nnoremap <silent> <leader>fs :Telescope grep_string<CR>
```

```lua
require('telescope').setup{
  defaults = {
    file_ignore_patterns = { "node_modules", ".git/" },
  },
  pickers = {
    find_files = {
      find_command = { "fdfind", "--type", "f", "--hidden", "--follow", "--exclude", ".git" },
    },
  },
}
```

### External dependencies

- `ripgrep` — used by `live_grep` and `grep_string`: `sudo apt install ripgrep`
- `fd-find` — faster alternative to `find` for `find_files`: `sudo apt install fd-find`

---

## 2. LSP (Language Server Protocol)

LSP gives you IDE-level features: go-to-definition, autocomplete, rename, diagnostics, etc. Neovim has a built-in LSP client, but you need plugins to manage server installation and configuration.

### Plugins

```vim
Plug 'neovim/nvim-lspconfig'           " LSP configuration presets
Plug 'williamboman/mason.nvim'         " LSP server installer (UI)
Plug 'williamboman/mason-lspconfig.nvim'" bridge between mason and lspconfig
```

### Keybindings

| Binding | Action | Description |
|---------|--------|-------------|
| `gd` | `vim.lsp.buf.definition()` | Jump to where a symbol is defined |
| `gD` | `vim.lsp.buf.declaration()` | Jump to symbol declaration (e.g., header in C) |
| `gr` | `vim.lsp.buf.references()` | List all references to the symbol under cursor |
| `gi` | `vim.lsp.buf.implementation()` | Jump to interface implementation |
| `K` | `vim.lsp.buf.hover()` | Show documentation popup for symbol under cursor |
| `<Space>rn` | `vim.lsp.buf.rename()` | Rename symbol across the project |
| `<Space>ca` | `vim.lsp.buf.code_action()` | Show available code actions (fixes, refactors) |
| `<Space>e` | `vim.diagnostic.open_float()` | Show full diagnostic message in a floating window |
| `[d` | `vim.diagnostic.goto_prev()` | Jump to previous diagnostic (error/warning) |
| `]d` | `vim.diagnostic.goto_next()` | Jump to next diagnostic (error/warning) |

### Configuration

```lua
-- Setup mason (LSP installer)
require("mason").setup()
require("mason-lspconfig").setup({
  ensure_installed = { "ts_ls", "pyright", "lua_ls" },  -- add your languages
})

-- Keybindings applied when an LSP server attaches to a buffer
local on_attach = function(client, bufnr)
  local opts = { noremap = true, silent = true, buffer = bufnr }
  vim.keymap.set('n', 'gd', vim.lsp.buf.definition, opts)
  vim.keymap.set('n', 'gD', vim.lsp.buf.declaration, opts)
  vim.keymap.set('n', 'gr', vim.lsp.buf.references, opts)
  vim.keymap.set('n', 'gi', vim.lsp.buf.implementation, opts)
  vim.keymap.set('n', 'K', vim.lsp.buf.hover, opts)
  vim.keymap.set('n', '<leader>rn', vim.lsp.buf.rename, opts)
  vim.keymap.set('n', '<leader>ca', vim.lsp.buf.code_action, opts)
  vim.keymap.set('n', '<leader>e', vim.diagnostic.open_float, opts)
  vim.keymap.set('n', '[d', vim.diagnostic.goto_prev, opts)
  vim.keymap.set('n', ']d', vim.diagnostic.goto_next, opts)
end

-- Apply on_attach to each server
local lspconfig = require('lspconfig')
local servers = { "ts_ls", "pyright", "lua_ls" }
for _, server in ipairs(servers) do
  lspconfig[server].setup({ on_attach = on_attach })
end
```

### Notes

- Run `:Mason` to open the installer UI and add/remove language servers.
- `ts_ls` = TypeScript/JavaScript, `pyright` = Python, `lua_ls` = Lua. Add servers for your stack.

---

## 3. Autocompletion

Autocompletion shows suggestions as you type, powered by LSP, snippets, and buffer content.

### Plugins

```vim
Plug 'hrsh7th/nvim-cmp'               " completion engine
Plug 'hrsh7th/cmp-nvim-lsp'           " LSP source for nvim-cmp
Plug 'hrsh7th/cmp-buffer'             " buffer words source
Plug 'hrsh7th/cmp-path'               " filesystem path source
Plug 'L3MON4D3/LuaSnip'              " snippet engine (required by nvim-cmp)
Plug 'saadparwaiz1/cmp_luasnip'       " snippet source for nvim-cmp
```

### Keybindings (inside completion menu)

| Binding | Action | Description |
|---------|--------|-------------|
| `<C-n>` | Next item | Move down in completion list |
| `<C-p>` | Previous item | Move up in completion list |
| `<C-y>` | Confirm | Accept the selected completion |
| `<C-e>` | Abort | Close the completion menu |
| `<C-Space>` | Trigger | Manually trigger completion |

### Configuration

```lua
local cmp = require('cmp')
local luasnip = require('luasnip')

cmp.setup({
  snippet = {
    expand = function(args)
      luasnip.lsp_expand(args.body)
    end,
  },
  mapping = cmp.mapping.preset.insert({
    ['<C-n>'] = cmp.mapping.select_next_item(),
    ['<C-p>'] = cmp.mapping.select_prev_item(),
    ['<C-y>'] = cmp.mapping.confirm({ select = true }),
    ['<C-e>'] = cmp.mapping.abort(),
    ['<C-Space>'] = cmp.mapping.complete(),
  }),
  sources = cmp.config.sources({
    { name = 'nvim_lsp' },
    { name = 'luasnip' },
    { name = 'buffer' },
    { name = 'path' },
  }),
})
```

---

## 4. Git Integration

### Plugins

```vim
Plug 'tpope/vim-fugitive'             " git commands inside nvim
Plug 'lewis6991/gitsigns.nvim'        " git gutter signs + hunk operations
```

### Keybindings

| Binding | Command / Action | Description |
|---------|-----------------|-------------|
| `<Space>gs` | `:Git` (fugitive) | Open git status in a split |
| `<Space>gb` | `:Gitsigns blame_line` | Show git blame for current line |
| `<Space>gd` | `:Gitsigns diffthis` | Diff current file against index |
| `<Space>gp` | `:Gitsigns preview_hunk` | Preview the hunk under cursor in a popup |
| `<Space>gr` | `:Gitsigns reset_hunk` | Discard changes in the current hunk |
| `<Space>gS` | `:Gitsigns stage_hunk` | Stage the current hunk |
| `]c` | Next hunk | Jump to next changed hunk |
| `[c` | Previous hunk | Jump to previous changed hunk |

### Configuration

```lua
require('gitsigns').setup({
  on_attach = function(bufnr)
    local gs = package.loaded.gitsigns
    local opts = { noremap = true, silent = true, buffer = bufnr }

    vim.keymap.set('n', ']c', function() gs.nav_hunk('next') end, opts)
    vim.keymap.set('n', '[c', function() gs.nav_hunk('prev') end, opts)
    vim.keymap.set('n', '<leader>gp', gs.preview_hunk, opts)
    vim.keymap.set('n', '<leader>gb', function() gs.blame_line({ full = true }) end, opts)
    vim.keymap.set('n', '<leader>gd', gs.diffthis, opts)
    vim.keymap.set('n', '<leader>gr', gs.reset_hunk, opts)
    vim.keymap.set('n', '<leader>gS', gs.stage_hunk, opts)
  end,
})
```

```vim
nnoremap <silent> <leader>gs :Git<CR>
```

---

## 5. File Explorer

A sidebar tree view for browsing project files.

### Plugin

```vim
Plug 'nvim-tree/nvim-tree.lua'
Plug 'nvim-tree/nvim-web-devicons'    " file icons (optional, requires a Nerd Font)
```

### Keybindings

| Binding | Action | Description |
|---------|--------|-------------|
| `<Space>e` | `:NvimTreeToggle` | Toggle the file tree sidebar |
| `a` | Create file/dir | Inside the tree, create a new file or directory |
| `d` | Delete | Inside the tree, delete selected file |
| `r` | Rename | Inside the tree, rename selected file |
| `x` | Cut | Inside the tree, cut file |
| `p` | Paste | Inside the tree, paste file |
| `<CR>` | Open | Open file or expand directory |

### Configuration

```lua
require("nvim-tree").setup()
```

```vim
nnoremap <silent> <leader>e :NvimTreeToggle<CR>
```

> **Note**: If you use `<Space>e` for both diagnostics (LSP) and file tree, pick one. Common alternative for diagnostics: `<Space>d`.

### External dependency

- A [Nerd Font](https://www.nerdfonts.com/) installed and set in your terminal for file icons.

---

## 6. Buffer & Window Management

No plugins needed — these are built-in Neovim features with custom keybindings.

### Keybindings

| Binding | Command | Description |
|---------|---------|-------------|
| `<Space>w` | `:w` | Save current file |
| `<Space>q` | `:q` | Quit current window |
| `<Space>bd` | `:bdelete` | Close current buffer without closing the window |
| `<C-h>` | `<C-w>h` | Move focus to the left split |
| `<C-j>` | `<C-w>j` | Move focus to the split below |
| `<C-k>` | `<C-w>k` | Move focus to the split above |
| `<C-l>` | `<C-w>l` | Move focus to the right split |

### Configuration

```vim
nnoremap <silent> <leader>w :w<CR>
nnoremap <silent> <leader>q :q<CR>
nnoremap <silent> <leader>bd :bdelete<CR>

" Navigate between splits with Ctrl + h/j/k/l
nnoremap <C-h> <C-w>h
nnoremap <C-j> <C-w>j
nnoremap <C-k> <C-w>k
nnoremap <C-l> <C-w>l
```

---

## 7. Code Comments

Toggle comments on lines or selections.

### Plugin

```vim
Plug 'numToStr/Comment.nvim'
```

### Keybindings

| Binding | Mode | Description |
|---------|------|-------------|
| `gcc` | Normal | Toggle comment on current line |
| `gc` | Visual | Toggle comment on selected lines |
| `gbc` | Normal | Toggle block comment on current line |
| `gb` | Visual | Toggle block comment on selection |

### Configuration

```lua
require('Comment').setup()
```

No custom keybindings needed — the plugin sets these defaults automatically.

---

## 8. Syntax Highlighting (Treesitter)

Treesitter provides accurate, language-aware syntax highlighting (much better than regex-based highlighting).

### Plugin

```vim
Plug 'nvim-treesitter/nvim-treesitter', {'do': ':TSUpdate'}
```

### Configuration

```lua
require('nvim-treesitter.configs').setup({
  ensure_installed = { "lua", "python", "typescript", "javascript", "bash", "json", "yaml", "markdown" },
  highlight = { enable = true },
  indent = { enable = true },
})
```

No keybindings — Treesitter works automatically once installed.

---

## Full Plugin List (vim-plug)

All plugins from the sections above in one block, ready to paste into `init.vim`:

```vim
call plug#begin(stdpath('data') . '/plugged')

" Telescope (fuzzy finder)
Plug 'nvim-lua/plenary.nvim'
Plug 'nvim-telescope/telescope.nvim'

" LSP
Plug 'neovim/nvim-lspconfig'
Plug 'williamboman/mason.nvim'
Plug 'williamboman/mason-lspconfig.nvim'

" Autocompletion
Plug 'hrsh7th/nvim-cmp'
Plug 'hrsh7th/cmp-nvim-lsp'
Plug 'hrsh7th/cmp-buffer'
Plug 'hrsh7th/cmp-path'
Plug 'L3MON4D3/LuaSnip'
Plug 'saadparwaiz1/cmp_luasnip'

" Git
Plug 'tpope/vim-fugitive'
Plug 'lewis6991/gitsigns.nvim'

" File tree
Plug 'nvim-tree/nvim-tree.lua'
Plug 'nvim-tree/nvim-web-devicons'

" Comments
Plug 'numToStr/Comment.nvim'

" Treesitter
Plug 'nvim-treesitter/nvim-treesitter', {'do': ':TSUpdate'}

call plug#end()
```

After adding plugins, run `:PlugInstall` inside Neovim, then `:Mason` to install language servers.
