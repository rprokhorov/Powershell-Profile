This is my configuration files for modify Powershell console.

I use modules:

- [posh-git (https://github.com/dahlbyk/posh-git)](https://github.com/dahlbyk/posh-git)
- [oh-my-posh (https://github.com/JanDeDobbeleer/oh-my-posh)](https://github.com/JanDeDobbeleer/oh-my-posh)

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
```

Screenshot: 

![alt text][logo]

[logo]: https://github.com/rprokhorov/Powershell-Profile/blob/master/example.png?raw=true "Example PowerShell console"
