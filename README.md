# edu-zero-tweaks

## VIM

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
