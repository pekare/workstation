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

### Install docker in WSL
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update -y
sudo apt-get install -y docker-ce
sudo usermod -aG docker $USER
```

### Disable TLS for docker desktop daemon and configure docker-cli access to docker desktop
```
echo "export DOCKER_HOST=tcp://localhost:2375" >> ~/.bashrc && source ~/.bashrc
```

### Fix mount issue with WSL and relogg
```
sudo cat /etc/wsl.conf<<EOF
[automount]
root = /
options = "metadata"
EOF
```
