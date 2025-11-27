#ProjectI (Self-Hosted Cloud Server with Nextcloud)
A step by step approach on how to setup a self-hosted cloud server with Nextcloud and access it remotely with TailScale

#Requirements
Docker.
Nextcloud apache image.
TailScale.
Web browser.
Windows PowerShell/Command Prompt.

#Installation
1. Download and install docker.
https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe?utm_location=module.
2. Download and install TailScale.
https://pkgs.tailscale.com/stable/tailscale-setup-latest.exe.
3. Open powershell/command prompt and download the latest windows subsystem for Linux by running this command: wsl --update in cmd. 
4. Start Docker.
5. Run: docker run -d -p 8080:80 nextcloud in powershell/cmd to install nextcloud apache image.
6. Start nextcloud from docker container if it did not start automatically.
7. Visit http://localhost:8080.
8. Follow the instruction to setup your account.

# Accessing nextcloud remotely on home network (No port Forwarding)
1. TailScale and login to your account
2. Under the Machines section, add devices on your local network (You need admin access from host machine)
3. Retrive your TailScale static Address. OR you can: run tailscale ip -4 in powershell/cmd to see your tailscale address.

# Locate nextcloud's config
1. Run powershell/cmd as admin.
2. Execute: docker ps to reveal docker id.
3. To open a shell inside the container with root access, run: docker exec -it <container_id> /bin/bash.
4. Navigate to /var/www/html/config .

#edit nextcloud's config.php
1. Run: nano config.php .
2. Add your TailScale address to the trusted_domains array section.
3. Save file by pressing ctrl + O and hit enter. ctrl + x to exit.

#restart docker 
1. Run: docker restart <container_id> .

#Test your cloud by entering your TailScale address in your browser with  port:8080

# Connect Remotely
1. Download TailScale mobile.
2. Add your device to host TailScale account.(Device must be on the same network).
3. Login to your nextcloud's app with your host TailScale Address.
