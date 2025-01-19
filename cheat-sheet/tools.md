# Tools

### Install Git client

Git for Windows - [download](https://gitforwindows.org/)  
update Git from CLI

```shell
git update-git-for-windows
```

### Clink

[Clink](https://chrisant996.github.io/clink/)
[Clink custom prompt](https://chrisant996.github.io/clink/clink.html#gettingstarted_customprompt)
[Clink flex prompt - Nerd Fonts](https://github.com/chrisant996/clink-flex-prompt)

### Editors

| Tool  |   |   |   |   |
|---|---|---|---|---|
| Neovim  | `choco install neovim` |   |   |   |
|   |   |   |   |   |
|   |   |   |   |   |

### Neovim

Install neovim

```bash
choco install neovim
```

check config path

```bash
:echo stdpath('config)
C:\Users\<user>\AppData\Local\nvim
```

put [init.lua](https://github.com/nvim-lua/kickstart.nvim/blob/master/init.lua) to config path

```bash
C:\Users\<user>\AppData\Local\nvim\init.lua
```

next start, plugins will be installed

### How to generate UUID
https://www.uuidgenerator.net/dev-corner/bash  
https://www.uuidgenerator.net/  
npx uuid  
