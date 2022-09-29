# Configurations

## Windows Terminal

### Color scheme

Setting [Cobalt2](https://github.com/Reidond/cobalt2-windows-terminal) theme for Windows Terminal

### How to update existing repository

…or push an existing repository from the command line

```
git remote add origin <https://github.com/anticam/configs.git>
git branch -M main
git push -u origin main
```

### Oh My Posh

Oh My Posh [pure](https://ohmyposh.dev/docs/themes) theme

#### Font

[Cascadia Code Font](https://github.com/microsoft/cascadia-code)
[Cascadia Code Nerd Font](https://github.com/AaronFriel/nerd-fonts/releases/tag/v1.2.0)
[Caskaydia Cove Nerd Font](https://www.nerdfonts.com/font-downloads)

### PowerShell

```
code $profile
```

Microsoft.PowerShell_profile.ps1

```
oh-my-posh init pwsh --config $env:POSH_THEMES_PATH\pure.omp.json | Invoke-Expression
```

## Tutorials

### JavaScript

The Net Ninja - Async JavaScript [Tutorial](https://www.youtube.com/playlist?list=PL4cUxeGkcC9jx2TTZk3IGWKSbtugYdrlu) 2020

Pluralsight - [JavaScript Promises and Async Programming](https://app.pluralsight.com/library/courses/javascript-promises-async-programming/table-of-contents)
[github samples](https://github.com/taylonr/async-programming-promises)

### BAS generators

SAP Business Technology Platform - [Extension Generators](https://www.youtube.com/playlist?list=PLkzo92owKnVwQ-0oT78691fqvHrYXd5oN)

### Code with Brandon

[SAP UI5](https://www.youtube.com/watch?v=mmSB85rWQ3w&list=PL1c8MA5nHXbokyx1fdMWDbhGtxvLBbW8_)
SAP Gateway
[SAP ABAP CDS](https://www.youtube.com/watch?v=h2149dCi0Cw&list=PL1c8MA5nHXbo-OO9e58FkMWZklwIkQyj4)

### Dani Krossing

[JavaScript Tutorials](https://www.youtube.com/playlist?list=PL0eyrZgxdwhxNGMWROnaY35NLyEjTqcgB))

### Code with Ania Kubóv

[YouTube](https://www.youtube.com/c/AniaKub%C3%B3w)

## Docker

### Download docker images

Pull latest images

```
sudo docker-compose pull
```

Start new containers

```
sudo docker-compose up -d
```

Remove orphaned images

```
docker system prune
```

Remove dangling and unused images

```
sudo docker image prune -a
```
