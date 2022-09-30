# Configurations

## Windows Terminal

### Color scheme

Setting [Cobalt2](https://github.com/Reidond/cobalt2-windows-terminal) theme for Windows Terminal

### How to update existing Git repository

…or push an existing repository from the command line

```
git remote add origin <https://github.com/anticam/configs.git>
git branch -M main
git push -u origin main
```

### Oh My Posh

Oh My Posh [pure](https://ohmyposh.dev/docs/themes) theme

```
choco install oh-my-posh
```

#### Font

[Cascadia Code Font](https://github.com/microsoft/cascadia-code)
[Cascadia Code Nerd Font](https://github.com/AaronFriel/nerd-fonts/releases/tag/v1.2.0)
[Caskaydia Cove Nerd Font](https://www.nerdfonts.com/font-downloads)

```
choco install cascadia-code-nerd-font
```

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
Pluralsight - [JavaScript 2018 Variables and Types](https://app.pluralsight.com/library/courses/javascript-variables-types/table-of-contents)
[github samples](https://github.com/bmaluijb/GetYourLoanApp)

### BAS generators

SAP Business Technology Platform - [Extension Generators](https://www.youtube.com/playlist?list=PLkzo92owKnVwQ-0oT78691fqvHrYXd5oN)

### Code with Brandon

[SAP UI5](https://www.youtube.com/watch?v=mmSB85rWQ3w&list=PL1c8MA5nHXbokyx1fdMWDbhGtxvLBbW8_)
SAP Gateway
[SAP ABAP CDS](https://www.youtube.com/watch?v=h2149dCi0Cw&list=PL1c8MA5nHXbo-OO9e58FkMWZklwIkQyj4)

### Dani Krossing

[JavaScript Tutorials](https://www.youtube.com/playlist?list=PL0eyrZgxdwhxNGMWROnaY35NLyEjTqcgB)

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

## Tools

#### Chocolatey

Chocolatey [installation steps](https://chocolatey.org/install)

Tool list
| Name | Command | Description |
| --- | --- | --- |
| [Cascadia Font Nerd](https://www.nerdfonts.com/font-downloads) | `choco install cascadia-code-nerd-font` | --- |
| [CMake](https://cmake.org/cmake/help/v2.8.1/cmake.html) | `choco install cmake`  | --- |
| [Ditto Clipboard](https://ditto-cp.sourceforge.io/) | `choco install ditto` | --- |
| [Everything](https://www.voidtools.com/) | `choco install everything`| --- |
| [Git](https://gitforwindows.org/) | `choco install git` | Git Bash, openssl |
| [Gradle](https://gradle.org/) | `choco install gradle` | --- |
| [Kubelogin (CLI)](https://github.com/int128/kubelogin) | `choco install kubelogin` | `kubectl oidc-login` |
| [Kubernetes CLI](https://kubernetes.io/) | `choco install kubernetes-cli` | Google |
| [helm](https://helm.sh/) | `choco install kubernetes-helm` | --- |
| [Insomnia](https://insomnia.rest/) | `choco install insomnia-rest-api-client`| REST client |
| [JetBrains IntelliJ IDEA (Community Edition)](https://www.jetbrains.com/idea/) | `choco install intellijidea-community` ||
| [JetBrains PyCharm (Community Edition)](http://www.jetbrains.com/pycharm/) | `choco install pycharm-community`| JetBrains Python IDE |
| [JXplorer](http://jxplorer.org/) | `choco install jxplorer` | Java LDAP client |
| [Keystore explorer](http://keystore-explorer.org/) | `choco install keystore-explorer.portable` ||
| [Maven](https://maven.apache.org/) | `choco install maven` | --- |
| [Miller](https://github.com/johnkerl/miller) | `choco install miller` | CSV tool |
| [Nmap](https://nmap.org/) | `choco install nmap` | network tool |
| [Notepad++](https://notepad-plus-plus.org/) | `choco install notepadplusplus` | --- |
| [Notepad++ plugin manager](https://github.com/chtof/chocolatey-packages/tree/master/automatic/notepadplusplus-npppluginmanager) | `choco install npppluginmanager` | --- |
| [Oh-My-Posh](https://ohmyposh.dev/) | `choco install oh-my-posh` | --- |
| [Postman for Windows](https://www.postman.com/) | `choco install postman` ||
| [Python 3.x](https://www.python.org/downloads/) | `choco install python3`| ---|
| SAPMachine JDK 11 | `choco install sapmachine11` | --- |
| SAPMachine JDK 13 | `choco install sapmachine13` | --- |
| SAPMachine JDK 17 | `choco install sapmachine17` | --- |
| SAPMachine JDK 19 | `choco install sapmachine` | --- |
| [Screenpresso](https://www.screenpresso.com/) | `choco install screenpresso` | Capture tool |
| [Sizer](http://www.brianapps.net/sizer4/) | `choco install sizer` | Window resizer |
| [Treesize free](https://www.jam-software.com/treesize_free) | `choco install treesizefree` | Folder allocation |
| [VSCode](https://code.visualstudio.com/) | `choco install vscode` | --- |
| [Visual Studio 2022 Community](https://visualstudio.microsoft.com/) | `choco install visualstudio2022community`||
| [WinSCP](https://winscp.net/eng/download.php) | `choco install winscp` | --- |
| [Wireshark](https://www.wireshark.org/) | `choco install wireshark` | Network sniffer |
| [XCA](https://www.hohnstaedt.de/xca/) | `choco install xca` | Certificate and key manager |

Choco commands
| Task | Command | Description |
| --- | --- | --- |
| list installed packages | `choco list --localonly` | --- |
| list outdated packages | `choco outdated` | --- |
| upgrade one package | `choco upgrade <package>` ||
| upgrade all packages | `cup all -y`| --- |

#### Cloud Foundry

CF CLI tools

Install CF CLI
[CloudFoundry/CLI](https://github.com/cloudfoundry/cli)

or with Chocolatey

```
choco install cloudfoundry-cli
```

Add the community repository in CF CLI

```
cf add-plugin-repo CF-Community <https://plugins.cloudfoundry.org>
```

Plugins
| Plugin | Command | Description |
| --- | --- | --- |
|[service manager](https://github.com/SAP/cf-cli-smsi-plugin)|  `cf install-plugin service-management` | service manager installation|
| [multiapps](https://github.com/cloudfoundry/multiapps-cli-plugin) | `cf install-plugin multiapps` | multiapps installation |

Tasks
| Task | Command | Description |
| --- | --- | --- |
| look for outdated plugins | `cf plugins --outdated` | --- |
| update plugin | `cf install-plugin <name>` | --- |

#### Cloud MTA Build Tool

[Installation steps](https://sap.github.io/cloud-mta-build-tool/download/)

#### BTP

BTP CLI for Feature set B
[Tool](https://tools.hana.ondemand.com/#cloud)

## Resources

Community - [Cloud SDK](https://community.sap.com/topics/cloud-sdk)
[Cloud SDK](https://sap.github.io/cloud-sdk/)
[CAP](https://cap.cloud.sap/docs/)
[BTP Community](https://community.sap.com/topics/business-technology-platform)
