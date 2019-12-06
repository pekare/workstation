# workstation

### Enable hyper-v and reboot (admin)
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

### Enable wsl (admin)
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

### Install ubuntu wsl (user)
```
Invoke-WebRequest -Uri https://aka.ms/wsl-ubuntu-1804 -OutFile Ubuntu.appx -UseBasicParsing
Add-AppxPackage .\Ubuntu.appx
```

### Install chocolatey (admin)
```
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

### Install dev-tools (admin)
```
choco install git.install -y
choco install vscode -y
choco install putty-cac -y
choco install mremoteng -y
choco install winscp -y
choco install vagrant -y
choco install docker-desktop -y
```

### Install admin-tools (admin)
```
choco install rufus -y
choco install rsat -params '"/AD"' -y
choco install angryip -y
choco install wireshark -y
choco install nmap -y
```
