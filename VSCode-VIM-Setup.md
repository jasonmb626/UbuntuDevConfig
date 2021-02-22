# Setting up my Ubuntu development machine

From a fresh Ubuntu 20.04 installation, updated and guest additions installed (if in virtualbox).

## Install your ssh keys

Copy your ssh_keys.zip to ~/.ssh
```sh
unzip ssh_keys.zip
```
(Enter password)
```sh
rm ssh_keys.zip
```
You should now have these files and permissions in that folder.
```
-rw------- 1 dev dev 3.4K xxxx-xx-xx 07:14 id_rsa
-rw-r--r-- 1 dev dev  749 xxxx-xx-xx 06-02 07:14 id_rsa.pub
-rw-r--r-- 1 dev dev 2.2K xxxx-xx-xx 02-07 16:28 known_hosts
```

(might not have known_hosts)

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

### Install git/curl/powerline fonts

```sh
sudo apt install git curl fonts-powerline
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

### Install nvm
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
```
<sup>Copied from `https://github.com/nvm-sh/nvm`. Suggest you check for more recent version.</sup>

Close and reopen terminal

### Install Node LTS
```sh
nvm i --lts
```

### Install VS Code
```sh
sudo snap install code --classic
```

### Configure VS Code

### Set terminal fonts


#### Install VS Code extensions
TODO: Do we need Prettier extension if ESLint is configured to use prettier?
- Vim (vscodevim)
- Bracket Pair Colorizer 2 (CoenraadS)
- ESLint (Dirk Baemuer)
- Prettier (Prettier)
- Nord (arcticstudio)
- vscode-icons (VSCode Icons Team)

#### Replace Nord comment color
Open ~/.vscode/extensions/arcticicestudio.nord-visual-studio-code-0.15.1/themes/nord-color-theme.json 

Change comment color to 
```json
{
  "name": "Comment",
  "scope": "comment",
  "settings": {
    "foreground": "#B48EAD"
  }
},
```

```json
{
  "name": "Punctuation Definition Comment",
  "scope": [
    "punctuation.definition.comment",
    "punctuation.end.definition.comment",
    "punctuation.start.definition.comment"
  ],
  "settings": {
    "foreground": "#B48EAD"
  }
},
```

#### Configure settings.json
```json
{
  "terminal.integrated.fontFamily": "Courier, PowerlineSymbols",
  "vim.camelCaseMotion.enable": true,
  "vim.leader": "<space>",
  "vim.replaceWithRegister": true,
  "vim.useSystemClipboard": true,
  "editor.lineNumbers": "relative",
  "vim.normalModeKeyBindingsNonRecursive": [
    {
      "before": ["<leader>", "x"],
      "commands": ["workbench.action.toggleSidebarVisibility"]
    },
    {
      "before": ["<leader>", "z"],
      "commands": ["workbench.action.focusSideBar"]
    },
    {
      "before": ["<leader>", "f"],
      "commands": [ "revealInExplorer" ],
    },
    {
      "before": ["<leader>", "d", "b"],
      "commands": [ "editor.debug.action.toggleBreakpoint" ]
    },
    {
      "before": ["<leader>", "d", "B"],
      "commands": [ "editor.debug.action.conditionalBreakpoint" ]
    },
    {
      "before": ["<leader>", "d", "C"],
      "commands": [ "editor.debug.action.runToCursor" ]
    },
    {
      "before": ["<leader>", "<space>"],
      "commands": [ "workbench.action.debug.continue" ]
    },
    {
      "before": ["<leader>", "d", "j"],
      "commands": [ "workbench.action.debug.stepOver" ]
    },
    {
      "before": ["<leader>", "d", "l"],
      "commands": [ "workbench.action.debug.stepInto" ]
    },
    {
      "before": ["<leader>", "d", "h"],
      "commands": [ "workbench.action.debug.stepOut" ]
    },
    {
      "before": ["<leader>", "d", "p"],
      "commands": [ "workbench.action.debug.pause" ]
    },
    {
      "before": ["<leader>", "d", "r"],
      "commands": [ "workbench.action.debug.restart" ]
    },
    {
      "before": ["<leader>", "d", "s"],
      "commands": [ "workbench.action.debug.stop" ]
    },
    {
      "before": ["<leader>", "d", "c"],
      "commands": [ "workbench.panel.repl.view.focus" ]
    },
    {
      "before": ["<leader>", "d", "t"],
      "commands": [ "terminal.focus" ]
    },
    {
      "before": ["<leader>", "d", "o"],
      "commands": [ "workbench.panel.output.focus" ]
    },
    {
      "before": ["<leader>", "m"],
      "commands": [ "workbench.action.closePanel" ]
    },
  ],
  "vim.visualModeKeyBindingsNonRecursive": [
    {
        "before": [">"],
        "after": [">", "g", "v"]
    },
    {
        "before": ["<"],
        "after": ["<", "g" ,"v"]
    },
    {
      "before": ["ctrl+r", "m"],
      "commands": [ {
          "command": "editor.action.codeAction",
          "args": {
              "kind": "refactor.extract.function"
          },
      }]
    },
    {
      "before": ["ctrl+r", "c"],
      "commands": [ {
          "command": "editor.action.codeAction",
          "args": {
              "kind": "refactor.extract.constant",
              "preferred": true,
              "apply": "ifsingle"
          },
      }]
    },
  ]
}
```

#### Configure settings.json
```json
[
  {
    "editor.formatOnSave": true
  },
  {
      "key": "ctrl+r",
      "command": "extension.vim_ctrl+r",
      "when": "editorFocus && vim.active && vim.use<C-r> && !inDebugRepl"
  },
  { 
      "key": "ctrl+p",
      "command": "list.focusUp",
      "when": "listFocus && !inputFocus"
  },
  { 
      "key": "ctrl+n",
      "command": "list.focusDown",
      "when": "listFocus && !inputFocus"
  },
  {
      "key": "f",
      "command": "explorer.newFile",
      "when": "filesExplorerFocus"
  },
  {
      "key": "v",
      "command": "fileutils.newFolder",
      "when": "filesExplorerFocus"
  },
  {
      "key": "r",
      "command": "fileutils.renameFile",
      "when": "filesExplorerFocus"
  },
  {
      "key": "ctrl+d",
      "command": "editor.action.addSelectionToNextFindMatch",
      "when": "editorFocus && vim.active && vim.mode == 'Visual' && !inDebugRepl"
  }
]
```
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
- Dia
- MongoDB
- Postgres

## For each project
TODO: find out if can use npm instead of npx, -D instead of --dev for eslint-config-airbnb
```sh
npm i -D eslinit prettier eslint-plugin-prettier eslint-conig-prettier
npx install-peerdeps --dev eslint-config-airbnb
```

### If node
```sh
npm i -D eslint-plugin-node eslint-conig-node
```
### Prettier
Create .prettierrc
```json
{
  "singleQuote": true
}
```

### ESLint
Create .eslintrc.json manually OR
```sh
eslint --init
```

.eslintrc.json
```json
{
  "extends": ["airbnb", "prettier", "plugin:node/recommended"],
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": "error",
    "no-unused-vars": "warn"
  } 
}
```