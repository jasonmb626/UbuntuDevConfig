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

Set default profile to nord, opacity to ~0.3

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

### Install nodemon globaly
```sh
npm i -g nodemon
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
  "workbench.iconTheme": "vscode-icons",
  "workbench.colorTheme": "Nord",
  "terminal.integrated.fontFamily": "Courier, PowerlineSymbols",
  "vim.camelCaseMotion.enable": true,
  "vim.leader": "<space>",
  "vim.replaceWithRegister": true,
  "vim.useSystemClipboard": true,
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
    {
      "before": [ "d", "i", "l" ],
      "after": [ "^", "d", "g", "_" ]
    },
    {
      "before": [ "y", "i", "l" ],
      "after": [ "^", "y", "g", "_" ]
    },
    {
      "before": [ "d", "a", "l" ],
      "after": [ "-1", "d", "$" ]
    },
    {
      "before": [ "y", "a", "l" ],
      "after": [ "-1", "y", "$" ]
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
    {
      "before": ["ctrl+r", "g"],
      "commands": [ {
        "command": "editor.action.codeAction",
        "args": {
          "kind": "refactor.extract.constant",
          "preferred": false,
          "apply": "ifsingle"
        },
      }]
    },
  ],
}
```

#### Configure keybindings.json
```json
[
  {
      "key": "ctrl+r",
      "command": "extension.vim_ctrl+r",
      "when": "editorFocus && vim.active && vim.use<C-r> && !inDebugRepl"
  },
  {
      "key": "ctrl+f",
      "command": "explorer.newFile",
      "when": "filesExplorerFocus"
  },
  {
      "key": "ctrl+v",
      "command": "explorer.newFolder",
      "when": "filesExplorerFocus"
  },
  {
      "key": "ctrl+r",
      "command": "renameFile",
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
    { //these first 4 lines probably already there.
      "type": "node",
      "request": "launch",
      "name": "Launch Program",
      "program": "${workspaceFolder}/server.js", //or app.js or whatever
      "restart": true,
      "runtimeExecutable": "nodemon",
      "console": "integratedTerminal",
      //what does this do? I added it but seems unnecessary
      "skipFiles": [
        "<node_internals>/**"
      ],
    }
  ]
}
```

Make sure nodemon is installed globally if you do this.

## Install and configure PostgreSQL

### Install PostgreSQL
```sh
sudo apt install postgresql postgresql-contrib
```

### Switch to postgres user
```sh
sudo -i -u postgres
```

### Create user dev
Choose y as super user
The Postgres authentication system makes the sassumption that by default that for any role used to log in, that role will have a database with the same name which it can access so also create db for said user
```sh
createuser --interactive --pwprompt dev
createdb sammy
```
### Exit back to your dev user
```sh
exit
```

### Create user app
Choose n as super user
The Postgres authentication system makes the sassumption that by default that for any role used to log in, that role will have a database with the same name which it can access so also create db for said user
```sh
createuser --interactive --pwprompt app
createdb app
```

### Create db for your project
```sh
createdb project_name
```

### Login to database as app user
```sh
psql -U app -h localhost project_name
```

### Confirm you're using the right database
```sql
SELECT current_database();
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

## Create quick test app
Create project folder with app.js
```sh
npm init
npm i pg
```
Create your javascript file
```javascript
const { Client } = require('pg');

const connectionString = 'postgresql://app:123456@localhost:5432/project_name'

const client = new Client({
  connectionString,
});

(async () => { 
  try {
    await client.connect();
    const res = await client.query('SELECT * FROM test');
    console.log(res.rows[0]);
    await client.end();
  } catch (err) {
    console.error(err);
  }
})();
```

Does it work? Success!
