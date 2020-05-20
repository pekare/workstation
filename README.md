# VScode with docker

### Enable wsl and hyper-v (admin)
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

### Install debian wsl (user)
```
Invoke-WebRequest -Uri https://aka.ms/wsl-debian-gnulinux -OutFile debian.appx -UseBasicParsing
Add-AppxPackage .\debian.appx
```

### Install chocolatey (admin)
```
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

### Install dev-tools (admin)
```
choco install -y git.install vscode putty-cac winscp docker-desktop burp-suite-free-edition ghidra
```

### Install admin-tools (admin)
```
choco install -y rufus rsat wireshark winpcap nmap ldapadmin
```

### Upgrade debian to buster
```
sudo sed -i 's/stretch/buster/g' /etc/apt/sources.list
sudo apt update
sudo apt dist-upgrade -y
sudo apt autoremove
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
Fix issue in remote-WSL for renaming files. Add to vscode settings.json.
```
"remote.WSL.fileWatcher.polling": true
```

### Add weasel-pageant
Download https://github.com/vuori/weasel-pageant/releases/latest.
Unpack at /c/Users/${USER}/Documents/ssh/weasel-pageant/.
Add weasel-pageant to bashrc.
```
cat <<'EOF'>> ~/.bashrc
eval $(/c/Users/${USER}/Documents/ssh/weasel-pageant/weasel-pageant -r) >/dev/null
EOF
```
### Install docker in WSL
```
sudo apt install -y \
     apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     software-properties-common
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
sudo apt update
sudo apt install -y docker-ce-cli
```

### Disable TLS for docker desktop daemon and configure docker-cli access to docker VM
```
echo "export DOCKER_HOST=tcp://localhost:2375" >> ~/.bashrc && source ~/.bashrc
```


