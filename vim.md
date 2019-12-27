# Install WSL debian
Invoke-WebRequest -Uri https://aka.ms/wsl-debian-gnulinux -OutFile debian.appx -UseBasicParsing
Add-AppxPackage .\debian.appx


