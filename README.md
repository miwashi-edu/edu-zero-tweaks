# edu-zero-tweaks

## Upgrade system

```bash
sudo apt update
sudo apt full-upgrade
```

## VIM

### Compatibility & Basics

- `set nocompatible` - Disables VI compatiblity mode, enabling full VIM features.
- `syntax on` - Enables syntax highligthing
- `set number` — shows absolute line numbers in the gutter
- `set relativenumber` — shows line numbers relative to the cursor; combined with `number`, the - current line shows its absolute number while others show distance from it

### Visual Comfort

- `set cursorline` — highlights the entire line the cursor is on
- `set scrolloff=5` — keeps 5 lines of context visible above/below the cursor when scrolling
- `set nowrap` — disables line wrapping; long lines extend off-screen
- `set colorcolumn`=80 — draws a vertical highlight at column 80 (a common line-length guide)
- `set background=dark` — hints to Vim that your terminal has a dark background, affecting how - some colorschemes render
- `colorscheme desert` — applies the built-in desert colorscheme

### Indentation

- `set tabstop=4` — a tab character displays as 4 spaces wide
- `set shiftwidth=4` — indent/dedent operations (>>, <<, auto-indent) move by 4 spaces
- `set expandtab` — pressing Tab inserts spaces instead of a tab character
- `set smartindent` — automatically indents new lines based on code structure (brackets, keywords, etc.)

### Performance

- `set lazyredraw` — Vim won't redraw the screen during macros or scripts, speeding up execution
- `set ttyfast` — signals a fast terminal connection, enabling smoother redrawing
- `set updatetime=300` — reduces the delay (in ms) before Vim writes the swap file and fires the - `CursorHold` event; 300ms is popular for plugins like LSP/diagnostics that hook into that event (default is 4000ms)

```bash
cd ~
cat > .vimrc << EOF
set nocompatible
syntax on
set number
set relativenumber
set cursorline
set scrolloff=5
set nowrap
set tabstop=4
set shiftwidth=4
set expandtab
set smartindent
set colorcolumn=80
set background=dark
colorscheme desert

" performance
set lazyredraw
set ttyfast
set updatetime=300
EOF
```
