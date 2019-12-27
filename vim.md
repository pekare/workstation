# Install WSL debian
```
Invoke-WebRequest -Uri https://aka.ms/wsl-debian-gnulinux -OutFile debian.appx -UseBasicParsing
Add-AppxPackage .\debian.appx
```

# Fix mount issue with WSL and relogg
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
