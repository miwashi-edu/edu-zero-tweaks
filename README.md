# edu-zero-tweaks

## Upgrade system

> sudo apt full-upgrade upgrades all installed packages to their latest available versions, but unlike `apt upgrade`, it's allowed to add or remove packages if that's what's needed to resolve dependencies. A regular `apt upgrade` will skip a package rather than touch the dependency graph; `full-upgrade` will go through with it.

```bash
sudo apt update # refresh the package index
sudo apt full-upgrade  # apply all upgrades
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

set cursorline
set scrolloff=5
set nowrap
set tabstop=4
set shiftwidth=4
set expandtab
set smartindent
set colorcolumn=80
set background=dark

set lazyredraw
set ttyfast
set updatetime=300
EOF
```
### Toggle numbers when copy/pasting in VIM

```txt
ESC
:set nonumber
:set number
```
## Starship (If we don't install Zsh)

```bash
curl -sS https://starship.rs/install.sh | sh
echo 'eval "$(starship init bash)"' >> ~/.bashrc
source ~/.bashrc
```

## Zsh (zeeshell)

```bash
sudo apt install zsh
chsh -s $(which zsh)
```

## Git

```bash
git config --global alias.tree "log --oneline --graph --all --decorate"
```

## Tools

```bash
# ls replacement
sudo apt install lsd
# ls replacement
sudo apt install eza
# cat replacement batcat
sudo apt install bat
# top replacement
sudo apt install htop
```

## Time

> These doesn't work in docker.

```bash
sudo timedatectl set-ntp true
sudo timedatectl set-timezone Europe/Stockholm
```

## SSH

> By removing reverse DNS, we can speed up SSH
> CAREFUL mDNS might stop working

```bash
sudo sed -i 's/#ClientAliveInterval 0/ClientAliveInterval 60/' /etc/ssh/sshd_config
sudo sed -i 's/#ClientAliveCountMax 3/ClientAliveCountMax 3/' /etc/ssh/sshd_config
sudo sed -i 's/#UseDNS no/UseDNS no/' /etc/ssh/sshd_config
sudo systemctl restart sshd
# Check
grep -E 'ClientAlive|UseDNS' /etc/ssh/sshd_config
```

