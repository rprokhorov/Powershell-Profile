This is my configuration files for modify Powershell console.

I use modules:

- [posh-git](https://github.com/dahlbyk/posh-git)
- [oh-my-posh](https://github.com/JanDeDobbeleer/oh-my-posh)
- [ColorTool](https://github.com/microsoft/terminal/releases/tag/1904.29002)
- [ColorTool theme](https://github.com/dracula/powershell)

And edit theme Fish and default.ps1 file.

Font [JetBrains mono](https://www.jetbrains.com/lp/mono/)

Commands for install

```PowerShell
git clone 'https://github.com/rprokhorov/Powershell-Profile.git'
Install-Module -Name 'oh-my-posh' -Scope CurrentUser -Force
Install-Module -Name 'posh-git' -Scope CurrentUser -Force
Copy-Item -Path .\profile.ps1 -Destination $PROFILE.AllUsersAllHosts -Force
$OhMyPosh = ((Get-Module -ListAvailable oh-my-posh).Path -split '\\')
Copy-Item -Path .\oh-my-posh\defaults.ps1 -Destination "$($OhMyPosh[0..($OhMyPosh.Length-2)] -join '\')\defaults.ps1" -Force
Copy-Item -Path .\oh-my-posh\Themes\Fish.psm1 -Destination "$($OhMyPosh[0..($OhMyPosh.Length-2)] -join '\')\Themes\Fish.psm1" -Force
# Download ColorTool from Microsoft and expand archive to Program Files (if do not trust ColorTool.zip in this repository).
# Invoke-WebRequest -Uri 'https://github.com/microsoft/terminal/releases/download/1904.29002/ColorTool.zip' -UseBasicParsing -OutFile ColorTool.zip
Expand-Archive -Path .\ColorTool.zip -DestinationPath 'C:\Program Files\ColorTool'
Copy-Item -Path .\ColorTool\schemes\* -Destination 'C:\Program Files\ColorTool\schemes\' -Force
# set theme
&'C:\Program Files\ColorTool\ColorTool.exe' -b 'C:\Program Files\ColorTool\schemes\Dracula-ColorTool.itermcolors'
```

Commands for Uninstall

```PowerShell
Remove-Module -Name 'posh-git' -Force
Remove-Module -Name 'oh-my-posh' -Force
Remove-Item $PROFILE.AllUsersAllHosts -Force
Remove-Item -Path 'C:\Program Files\ColorTool\' -Recurse
&'C:\Program Files\ColorTool\ColorTool.exe' -b 'C:\Program Files\ColorTool\schemes\campbell.ini'
```

Screenshot: 

![alt text][logo]

[logo]: https://github.com/rprokhorov/Powershell-Profile/blob/master/example.png?raw=true "Example PowerShell console"
