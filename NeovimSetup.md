# Setting up my Ubuntu development machine

From a fresh Ubuntu 20.04 installation, updated and guest additions installed.

## Desktop Appearance

Change the look and feel to your prefrences.

### Get your wallpaper

Download your [wallpaper](https://wallpaperaccess.com/download/blue-lagoon-3908317) and set it as your desktop wallpaper

### Set Ubuntu Dark Theme

### Install dependencies for extending Gnome functionality

- chrome-gnome-shell for shell extension installation via web
- gnome-tweaks is the gnome tweak tool

```sh
sudo apt install chrome-gnome-shell gnome-tweaks
```

### Enable user themes

Install from the [User Themes](https://extensions.gnome.org/extension/19/user-themes/) extension page

## Download your preferred theme

[Nordic GTK3 theme](https://www.gnome-look.org/p/1267246/)
- Download Nordic-bluish-accent.tar.xz, unzip contents to ~/.themes
- Download Nordic-Folders.tar.xz, unzip its "nordic folder" to ~/.icons (you can ignore the noric-dark folder)

### Set the themes

Open tweaks -> Appearance -> set shell, applications to Nordic-bluish-accent, set icons to Nordic
            -> Window Titlebars -> Placement = Left

## Install neovim. Customize it and terminal appearance
### Install neovim
```sh
sudo snap install nvim --classic
```

### Install additional dependencies
- curl for script downloads
- git for version control
- python3-pip for Vimspector
- fonts-powerline for fancy prompt, vim airline
- xsel for clipboard support

```sh
sudo apt install curl git python3-pip fonts-powerline xsel
```

### Install theme for Gnome Terminal (TODO - try termite, terminator, alacritty)
```sh
git clone https://github.com/arcticicestudio/nord-gnome-terminal.git
cd nord-gnome-terminal/src
./nord.sh
```
<sup>Copied from `https://www.nordtheme.com` -> Ports -> Gnome Terminal -> GitHub page</sup>

### Set Nord as default profile in Gnome Terminal

### Install Fancy Prompt
```sh
git clone --recursive https://github.com/andresgongora/synth-shell.git
cd synth-shell
./setup.sh
```
<sup>Copied from `https://github.com/andresgongora/synth-shell`</sup>

### Install Python Provider for neovim
```sh
python3 -m pip install --user --upgrade pynvim
```

### Install nvm
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
```
<sup>Copied from `https://github.com/nvm-sh/nvm`. Suggest you check for more recent version.</sup>

Close and reopen terminal

### Install Node v10 LTS
#### Both COC and Vimspector need this older node version
```sh
nvm i --lts 10
```

### Make nvm set node version on load
```sh
echo "nvm use 10" >> ~/.bashrc
```

### Install node support

```sh
npm i -g neovim
```

### Install VIMPlug
```sh
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```
Copied from `https://github.com/junegunn/vim-plug#unix-linux`

### Create your neovim config
```sh
mkdir -p ~/.config/nvim
cd ~/.config/nvim
touch init.vim settings.vim coc.vim keys.vim keys-whichkey.vim
nvim ~/.config/nvim/init.vim
```

### Put in your plugins, sensible defaults, etc
```
call plug#begin('~/.config/nvim/autoload/plugged')

Plug 'neoclide/coc.nvim', {'branch': 'release'}
Plug 'jasonmb626/nord-vim'
Plug 'puremourning/vimspector'
Plug 'szw/vim-maximizer'
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'
Plug 'kdheepak/lazygit.nvim', { 'branch': 'nvim-v0.4.3' }
Plug 'tpope/vim-surround'
Plug 'tpope/vim-fugitive'
Plug 'tpope/vim-commentary'
Plug 'bkad/CamelCaseMotion'
Plug 'liuchengxu/vim-which-key'
Plug 'sheerun/vim-polyglot'
Plug 'voldikss/vim-floaterm'
Plug 'JamshedVesuna/vim-markdown-preview'

call plug#end()

let g:airline_theme='simple'

"Optional set node path for coc (If running multiple node versions)
"let g:coc_node_path = '/path/to/node'

source ~/.config/nvim/settings.vim
source ~/.config/nvim/coc.vim
source ~/.config/nvim/keys.vim
source ~/.config/nvim/keys-whichkey.vim
" Register which key map
call which_key#register('<Space>', "g:which_key_map")

let g:airline#extensions#tabline#enabled = 1
let g:airline#extensions#tabline#left_sep = ' '
let g:airline#extensions#tabline#left_alt_sep = '|'
let g:airline_powerline_fonts = 1
```
Save

### Now gf on ~/.config/nvim/settings.vim to edit it
```
colorscheme nord
syntax enable                           " Enables syntax highlighing
set hidden                              " Required to keep multiple buffers open multiple buffers
set nowrap                              " Display long lines as just one line
set tabstop=2                           " Insert 2 spaces for a tab
set shiftwidth=2                        " Change the number of space characters inserted for indentation
set smarttab                            " Makes tabbing smarter will realize you have 2 vs 4
set expandtab                           " Converts tabs to spaces
set smartindent                         " Makes indenting smart
set autoindent                          " Good auto indent
set ruler              			            " Show the cursor position all the time
set cmdheight=2                         " More space for displaying messages
set mouse=a                             " Enable your mouse
set splitbelow                          " Horizontal splits will automatically be below
set splitright                          " Vertical splits will automatically be to the right
"set t_Co=256                            " Support 256 colors
set termguicolors
set conceallevel=0                      " So that I can see `` in markdown files
set laststatus=2                        " Always display the status line
set number                              " Line numbers
set cursorline                          " Enable highlighting of the current line
set showtabline=2                       " Always show tabs
set noshowmode                          " We don't need to see things like -- INSERT -- anymore
set nobackup                            " This is recommended by coc
set nowritebackup                       " This is recommended by coc
set shortmess+=c                        " Don't pass messages to |ins-completion-menu|.
set signcolumn=yes                      " Always show the signcolumn, otherwise it would shift the text each time
set updatetime=300                      " Faster completion
set timeoutlen=100                      " By default timeoutlen is 1000 ms
set clipboard=unnamedplus               " Copy paste between vim and everything else
set incsearch
```
save

### Now edit ~/.config/nvim/coc.vim
Copy and paste example vim config from COCs [github](https://github.com/neoclide/coc.nvim) page.
Save

### Edit keys.vim
Copy and paste from your workbook
Save

### Edit keys-whichkey.vim
Copy and paste from your workbook
Save

### Populate ~/.config/nvim/coc-settings.json
```json
{
  // autoformat
  "coc.preferences.formatOnSaveFiletypes": [
    "css",
    "markdown",
    "javascript",
    "graphql",
    "html",
    "yaml",
    "json",
    "python",
    "java"
  ],
  "coc.preferences.hoverTarget": "float",
  // emmet
  "emmet.includeLanguages": {
    "vue-html": "html",
    "javascript": "javascriptreact"
  },

  // explorer
  "explorer.width": 30,
  "explorer.file.root.template": "[icon] [git] [hidden & 1][root]",
  "explorer.icon.enableNerdfont": true,
  "explorer.previewAction.onHover": false,
  "explorer.icon.enableVimDevicons": false,
  "explorer.file.showHiddenFiles": false,
  "explorer.keyMappings.global": {
    "<cr>": ["expandable?", "expand", "open"],
    "v": "open:vsplit"
  },

  "bookmark.sign": "}",

  //coc-emoji
  "coc.source.emoji.filetypes": ["markdown"]}
```

Restart neovim

### Install your plugins
```
:PlugInstall
```

Restart neovim again

### Install CoC Plugins
```
CocInstall coc-marketplace coc-json coc-tsserver coc-tslint coc-explorer coc-deno
```

For any plugins you don't know the exact name of do 
```
CoCList marketplace
```
and do a fuzzy find

### Install Vimspector adapter
```
:VimspectorInstall vscode-node-debug2
```
<sup>Copied from `Copied from https://github.com/puremourning/vimspector#installation`</sup>

### You'll need a .vimspector.json in the root of your project folder
Copy from here
-https://github.com/puremourning/vimspector#javascript-typescript-etc  
-https://github.com/puremourning/vimspector#python

### Install Screenkey
```sh
sudo snap install --edge screenkey
```

### Make screenkey start on boot
Superkey -> type "Startup" open startup applications
Add new
```
/snap/bin/screenkey -p fixed -g 325x50-5+5 --key-mode composed --bak-mode normal --mods-mode normal --bg-color '#434C5E' --font-color '#A3BE8C' --opacity '0.8'
```

## Install additional development tools
- Google Chrome
- Postman
