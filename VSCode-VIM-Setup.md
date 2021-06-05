# Setting up my Fedora 34 development machine

From a fresh Fedora 34 installation, updated.

## Install your ssh keys

Copy your github-ssh_keys.zip to ~/.ssh

```sh
unzip github-ssh_keys.zip
```

(Enter password)

```sh
rm github-ssh_keys.zip
ls -l
```

You should now have these files and permissions in that folder.

```
-rw------- 1 dev dev 3.4K xxxx-xx-xx 07:14 id_rsa
-rw-r--r-- 1 dev dev  749 xxxx-xx-xx 06-02 07:14 id_rsa.pub
-rw-r--r-- 1 dev dev 2.2K xxxx-xx-xx 02-07 16:28 known_hosts
```

(you might not have known_hosts)

## Enable Flathub

Follow directions [here](https://developer.fedoraproject.org/deployment/flatpak/flatpak-usage.html)

```sh
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak remote-add --if-not-exists fedora oci+https://registry.fedoraproject.org
```

## Install [RPM Fusion](https://rpmfusion.org/)

```sh
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf groupupdate core
```

## Desktop Appearance

Change the look and feel to your prefrences.

### Get your wallpaper

Download your [wallpaper](https://wallpaperaccess.com/download/blue-lagoon-3908317) and set it as your desktop wallpaper

### Install dependencies for extending Gnome functionality

```sh
sudo dnf install gnome-tweaks
flatpak install org.gnome.Extensions
```

### Enable Gnome Extensions

#### Enable User Themes

Install from the [User Themes](https://extensions.gnome.org/extension/19/user-themes/) extension page
You'll need to install the browser plugin (it'll prompt you) and then refresh the page

#### Enable [Clipboard Indicator](https://extensions.gnome.org/extension/779/clipboard-indicator/)

## Download your preferred theme

[Nordic GTK3 theme](https://www.gnome-look.org/p/1267246/)

- Download Nordic-bluish-accent.tar.xz, unzip contents to ~/.themes
- Download Nordic-Folders.tar.xz, unzip its "nordic" folder to ~/.icons (you can ignore the noric-dark folder)

### Set the themes

Open tweaks -> Appearance -> set shell, applications to Nordic-bluish-accent, set icons to Nordic
-> Window Titlebars -> Placement = Left

### Install Alacritty & zsh

```sh
sudo dnf install alacritty zsh util-linux-user
chsh
```

set to /usr/bin/zsh

### Setup Alacritty

#### Install Theme

Follow directions on their [GitHub page](https://github.com/arcticicestudio/nord-alacritty)

#### Modify entry in .desktop

(This will give it normal windows borders)

```sh
sudo vim /usr/share/applications/Alacritty.desktop
```

Change

```
Exec=alacritty
```

to

```
Exec=env WINIT_UNIX_BACKEND=x11 alacritty
```

#### Reboot

This is a good time to reboot so all the changes get sourced properly.

### Install and Configure Powerline 10k

Steal some of the zsh powerlevel10k stuff from Manjaro

Install the meslo fonts recommended for Powerline 10k
Links [here](https://github.com/romkatv/powerlevel10k#meslo-nerd-font-patched-for-powerlevel10k)

```sh
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```

(To do: which options?)

### Install [zsh-nvm](https://github.com/lukechilds/zsh-nvm)

```sh
git clone https://github.com/lukechilds/zsh-nvm.git ~/.zsh-nvm
source ~/.zsh-nvm/zsh-nvm.plugin.zsh
```

### Install Node LTS

```sh
nvm i --lts
```

### Install nodemon globaly

```sh
npm i -g nodemon
```

### Install [VS Code](https://code.visualstudio.com/docs/setup/linux#_rhel-fedora-and-centos-based-distributions)

(Todo - VSCodium? Code-OSS)

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
sudo dnf check-update
sudo dnf install code
```

### Configure VS Code

#### Install VS Code extensions

TODO: Do we need Prettier extension if ESLint is configured to use prettier?

- Vim (vscodevim)
- Bracket Pair Colorizer 2 (CoenraadS)
- ESLint (Dirk Baemuer)
- Prettier (Prettier)
- mci_marina_nord (armoredelephant.theme)
- vscode-icons (VSCode Icons Team)

#### Configure settings.json

```json
{
  "workbench.iconTheme": "vscode-icons",
  "workbench.colorTheme": "Nord",
  "terminal.integrated.fontFamily": "Courier, PowerlineSymbols",
  "vim.camelCaseMotion.enable": true,
  "vim.leader": "<space>",
  "vim.replaceWithRegister": true,
  "vim.useSystemClipboard": true,
  "vim.useCtrlKeys": true,
  "vim.handleKeys": {
    "<C-v>": false,
    "<C-s>": false,
    "<C-a>": false,
    "<C-c>": false,
    "<C-p>": false
  },
  "editor.lineNumbers": "relative",
  "editor.formatOnSave": true,
  "editor.tabSize": 2,
  "editor.insertSpaces": true,
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
      "commands": ["revealInExplorer"]
    },
    {
      "before": ["<leader>", "d", "b"],
      "commands": ["editor.debug.action.toggleBreakpoint"]
    },
    {
      "before": ["<leader>", "d", "B"],
      "commands": ["editor.debug.action.conditionalBreakpoint"]
    },
    {
      "before": ["<leader>", "d", "C"],
      "commands": ["editor.debug.action.runToCursor"]
    },
    {
      "before": ["<leader>", "<space>"],
      "commands": ["workbench.action.debug.continue"]
    },
    {
      "before": ["<leader>", "d", "j"],
      "commands": ["workbench.action.debug.stepOver"]
    },
    {
      "before": ["<leader>", "d", "l"],
      "commands": ["workbench.action.debug.stepInto"]
    },
    {
      "before": ["<leader>", "d", "h"],
      "commands": ["workbench.action.debug.stepOut"]
    },
    {
      "before": ["<leader>", "d", "p"],
      "commands": ["workbench.action.debug.pause"]
    },
    {
      "before": ["<leader>", "d", "r"],
      "commands": ["workbench.action.debug.restart"]
    },
    {
      "before": ["<leader>", "d", "s"],
      "commands": ["workbench.action.debug.stop"]
    },
    {
      "before": ["<leader>", "d", "c"],
      "commands": ["workbench.panel.repl.view.focus"]
    },
    {
      "before": ["<leader>", "d", "t"],
      "commands": ["terminal.focus"]
    },
    {
      "before": ["<leader>", "d", "o"],
      "commands": ["workbench.panel.output.focus"]
    },
    {
      "before": ["<leader>", "m"],
      "commands": ["workbench.action.closePanel"]
    },
    {
      "before": ["d", "i", "l"],
      "after": ["^", "d", "g", "_"]
    },
    {
      "before": ["y", "i", "l"],
      "after": ["^", "y", "g", "_"]
    },
    {
      "before": ["d", "a", "l"],
      "after": ["-1", "d", "$"]
    },
    {
      "before": ["y", "a", "l"],
      "after": ["-1", "y", "$"]
    }
  ],
  "vim.visualModeKeyBindingsNonRecursive": [
    {
      "before": [">"],
      "after": [">", "g", "v"]
    },
    {
      "before": ["<"],
      "after": ["<", "g", "v"]
    },
    {
      "before": ["ctrl+r", "m"],
      "commands": [
        {
          "command": "editor.action.codeAction",
          "args": {
            "kind": "refactor.extract.function"
          }
        }
      ]
    },
    {
      "before": ["ctrl+r", "c"],
      "commands": [
        {
          "command": "editor.action.codeAction",
          "args": {
            "kind": "refactor.extract.constant",
            "preferred": true,
            "apply": "ifsingle"
          }
        }
      ]
    },
    {
      "before": ["ctrl+r", "g"],
      "commands": [
        {
          "command": "editor.action.codeAction",
          "args": {
            "kind": "refactor.extract.constant",
            "preferred": false,
            "apply": "ifsingle"
          }
        }
      ]
    }
  ]
}
```

#### Configure keybindings.json

```json
[
  {
    "key": "ctrl+l",
    "command": "explorer.newFile",
    "when": "filesExplorerFocus"
  },
  {
    "key": "ctrl+;",
    "command": "explorer.newFolder",
    "when": "filesExplorerFocus"
  },
  {
    "key": "ctrl+p",
    "command": "selectPrevSuggestion",
    "when": "suggestWidgetMultipleSuggestions && suggestWidgetVisible && textInputFocus"
  },
  {
    "key": "ctrl+n",
    "command": "selectNextSuggestion",
    "when": "suggestWidgetMultipleSuggestions && suggestWidgetVisible && textInputFocus"
  },
  {
    "key": "ctrl+p",
    "command": "showPrevParameterHint",
    "when": "editorFocus && parameterHintsMultipleSignatures && parameterHintsVisible"
  },
  {
    "key": "ctrl+n",
    "command": "showNextParameterHint",
    "when": "editorFocus && parameterHintsMultipleSignatures && parameterHintsVisible"
  }
]
```

#### Configure user snippets

File -> Preferences -> User Snippets -> JavaScript

```json
	"Destructure Require": {
		"prefix": ["dreq"],
		"body": ["const { $2 } = require('$1');"],
		"description": "Destructured Require"
	}
```

### Install Screenkey

```sh
sudo dnf install screenkey
```

Note: as of the time of this writing screenkey doesn't work on Wayland.

### (optional) Make screenkey start on boot

Superkey -> type "Startup" open startup applications
Add new

```
screenkey -p fixed -g 325x50-5+5 --key-mode composed --bak-mode normal --mods-mode normal --bg-color '#434C5E' --font-color '#A3BE8C' --opacity '0.8'
```

### Install Docker

```sh
sudo dnf install emby-engine
```

### create a test table

```sql
CREATE TABLE test (
  id SERIAL,
  val1 VARCHAR(20),
  val2 VARCHAR(20)
);
```

### Insert some dummy data for testing

```sql
INSERT INTO test VALUES(default, 'Hi', 'There');
```

### Set your environment variables

```sh
cd
vi .bashrc
```

Add

```
export PGUSER='app'
export PGPASSWORD='123456'
export PGDATABASE='project_name'
```

Log out and log back in

## Create quick test app

Create project folder with app.js

```sh
npm init
npm i pg
```

Create your javascript file

```javascript
const { Pool } = require("pg");

// If you've set environment variables this is not needed
// const connectionString = 'postgresql://app:123456@localhost:5432/project_name'

const pool = new Pool({
  // If you've set environment variables this is not needed
  // connectionString,
});

(async () => {
  const client = await pool.connect();
  try {
    let res = await client.query("SELECT * FROM test");
    console.log(res.rows[0]);
    res = await client.query(
      "INSERT INTO test VALUES (default, $1, $2) RETURNING *", //or RETURNING id
      ["Hi", "Back"]
    );
    console.log(res.rows[0]);
  } catch (err) {
    console.error(err);
  } finally {
    client.release();
  }
})().finally(() => pool.end());
```

Does it work? Success!

## Install additional development tools

- Google Chrome
- Postman
- Dia
- MongoDB

## For each project

TODO: find out if can use npm instead of npx, -D instead of --dev for eslint-config-airbnb

```sh
npm i -D eslint prettier eslint-plugin-prettier eslint-config-prettier
npx install-peerdeps --dev eslint-config-airbnb
```

### If node

```sh
npm i -D eslint-plugin-node eslint-config-node
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

### Configure debugger

Choose: Run->Add Configuration->NodeJS

```json
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      //these first 4 lines probably already there.
      "type": "node",
      "request": "launch",
      "name": "Launch Program",
      "program": "${workspaceFolder}/server.js", //or app.js or whatever
      "restart": true,
      "runtimeExecutable": "nodemon",
      "console": "integratedTerminal",
      //what does this do? I added it but seems unnecessary
      "skipFiles": ["<node_internals>/**"]
    }
  ]
}
```

Make sure nodemon is installed globally if you do this.
