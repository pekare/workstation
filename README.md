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
choco install ldapadmin -y
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
sudo tee /etc/wsl.conf<<EOF
[automount]
root = /
options = "metadata,umask=22,fmask=11"
EOF
```
```
sudo tee /etc/profile.d/file-perm-wsl.sh<<EOF
#!/bin/sh
if [[ "$(umask)" = "0000" ]]; then
  umask 0022
fi
EOF
```
### Fix permissions in Remote-WSL
```
mkdir ~/.vscode-server
tee ~/.vscode-server/server-env-setup<<EOF
#!/bin/sh
echo "Current umask: $(umask)"
umask 0022
echo "Changed umask to: 0022"
EOF
```
### Add weasel-pageant
Download https://github.com/vuori/weasel-pageant/releases/latest.
Unpack at /c/Users/${USER}/Documents/ssh/weasel-pageant/.
Add weasel-pageant to bashrc.
```
cat <<'EOF'>> ~/.bashrc
eval $(/c/Users/${USER}/Documents/ssh/weasel-pageant/weasel-pageant -r)
EOF
```


