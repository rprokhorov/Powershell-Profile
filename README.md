This is my configuration files for modify Powershell console.

I use modules:

- [posh-git](https://github.com/dahlbyk/posh-git)
- [oh-my-posh](https://github.com/JanDeDobbeleer/oh-my-posh)
- [ColorTool](https://github.com/microsoft/terminal/releases/tag/1904.29002)
- [ColorTool theme](https://github.com/dracula/powershell)

And edit theme Fish and default.ps1 file.


Steps for install
1) Install font [JetBrains mono](https://www.jetbrains.com/lp/mono/)
2) Change font in Powershell console.

![alt text][Change_font_1]

[change_font_1]: https://github.com/rprokhorov/Powershell-Profile/blob/master/change_font_1.png?raw=true "Change font in PowerShell console"

![alt text][Change_font_2]

[change_font_2]: https://github.com/rprokhorov/Powershell-Profile/blob/master/change_font_2.png?raw=true "Change font in PowerShell console"

3) Run install script
4) *Optional. If the background color doesn't change, you might change it manually.

![alt text][change_background]

[change_background]: https://github.com/rprokhorov/Powershell-Profile/blob/master/change_background.png?raw=true "Change background"


```PowerShell
git clone 'https://github.com/rprokhorov/Powershell-Profile.git'
Install-Module -Name 'oh-my-posh' -Scope CurrentUser -Force
Install-Module -Name 'posh-git' -Scope CurrentUser -Force
$git_repository_path = (Read-Host -Prompt "Path to your's git repositories") -replace '"' -replace "'"
(Get-Content -Path .\Powershell-Profile\profile.ps1) -replace '%~%', $git_repository_path | Out-File .\Powershell-Profile\profile.ps1 -Force
Copy-Item -Path .\Powershell-Profile\profile.ps1 -Destination $PROFILE.AllUsersAllHosts -Force
Copy-Item -Path .\Powershell-Profile\profile.ps1 -Destination $PROFILE -Force
$OhMyPosh = ((Get-Module -ListAvailable oh-my-posh).Path -split '\\')
Copy-Item -Path .\Powershell-Profile\oh-my-posh\defaults.ps1 -Destination "$($OhMyPosh[0..($OhMyPosh.Length-2)] -join '\')\defaults.ps1" -Force
Copy-Item -Path .\Powershell-Profile\oh-my-posh\Themes\Fish.psm1 -Destination "$($OhMyPosh[0..($OhMyPosh.Length-2)] -join '\')\Themes\Fish.psm1" -Force
# Download ColorTool from Microsoft and expand archive to Program Files (if do not trust ColorTool.zip in this repository).
# Invoke-WebRequest -Uri 'https://github.com/microsoft/terminal/releases/download/1904.29002/ColorTool.zip' -UseBasicParsing -OutFile ColorTool.zip
Expand-Archive -Path .\Powershell-Profile\ColorTool.zip -DestinationPath 'C:\Program Files\ColorTool'
Copy-Item -Path .\Powershell-Profile\ColorTool\schemes\* -Destination 'C:\Program Files\ColorTool\schemes\' -Force
# set theme
&'C:\Program Files\ColorTool\ColorTool.exe' -b 'C:\Program Files\ColorTool\schemes\Dracula-ColorTool.itermcolors'
$Host.UI.RawUI.BackgroundColor = 'Black' #sometimes it doesn't work, so you need change background color to "black" 
cls
```

Commands for Uninstall

```PowerShell
Remove-Module -Name 'posh-git' -Force
Remove-Module -Name 'oh-my-posh' -Force
Remove-Item $PROFILE.AllUsersAllHosts -Force
Remove-Item $PROFILE -Force
Remove-Item -Path 'C:\Program Files\ColorTool\' -Recurse
&'C:\Program Files\ColorTool\ColorTool.exe' -b 'C:\Program Files\ColorTool\schemes\campbell.ini'
```

Screenshot: 

![alt text][logo]

[logo]: https://github.com/rprokhorov/Powershell-Profile/blob/master/example.png?raw=true "Example PowerShell console"
