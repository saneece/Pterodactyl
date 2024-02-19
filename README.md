# Pterodactyl



Setup Ptero Panel VM and Container:

1. Setup Docker VM per standard Debian Setup here: https://github.com/saneece/Scripts/blob/main/New%20Debian%20Setup.yml</br>
Note: Investigate NOT setting Portainer is the default volume that the website states and isntead deploy using docker-compose and mapping volume else where to backup stacks deployed via Portainer </br>
2. Create the NPM url/certs for panel.domain.com and wings1.domain.com</br>
NOTE: </br>
Configure NPM for the Panel URL to pass http with the http port (801 in docker-compose.yml for Panel), but configure the SSL cert and force SSL </br>
Configure NPM for the Wings URL to pass http traffic with the https port (443 in docker-compose.yml for Wings), configure the SSL cert and force SSL </br>
</br>
4. cd to /dockconfigs and "sudo mkdir ptero"</br>
</br>
5. "cd ptero && sudo mkdir nginx && sudo mkdir certs && sudo mkdir logs && sudo mkdir var"</br>
</br>
6. sudo nano docker-compose.yml</br>
</br>
7. Paste, Edit and Save - https://github.com/saneece/Pterodactyl/blob/main/panel/docker-compose.yml </br>
</br>
8. cd nginx && sudo nano panel.conf</br>
</br>
9. Paste, Edit and Save - https://github.com/saneece/Pterodactyl/blob/main/panel/panel.conf</br>
</br>
10. start container with "docker-compose up -d"</br>
</br>
11. test the url and the direct IP of the panel</br>
</br>
12. Make the user for the panel with "docker-compose run --rm panel php artisan p:user:make"< /br>
