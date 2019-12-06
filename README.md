# workstation

## Enable hyper-v and reboot
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

### Install dev-tools
```
choco install git.install -y
choco install vscode -y
choco install putty-cac -y
choco install mremoteng -y
choco install winscp -y
choco install vagrant -y
choco install docker-desktop -y

### Install admin-tools
choco install rufus -y
choco install rsat -params '"/AD"' -y
choco install angryip -y
choco install wireshark -y
choco install nmap -y
