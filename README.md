# Pterodactyl



Setup Ptero Panel VM and Container:

1. Setup Docker VM per standard Debian Setup here: https://github.com/saneece/Scripts/blob/main/New%20Debian%20Setup.yml</br>
Note: Investigate NOT setting Portainer is the default volume that the website states and isntead deploy using docker-compose and mapping volume else where to backup stacks deployed via Portainer </br>
2. Create the NPM url/certs for panel.domain.com and wings1.domain.com</br>
NOTE: </br>
Configure NPM for the Panel URL to pass http with the http port (801 in docker-compose.yml for Panel), but configure the SSL cert and force SSL </br>
Configure NPM for the Wings URL to pass http traffic with the https port (443 in docker-compose.yml for Wings), configure the SSL cert and force SSL </br>
3. "cd /dockconfigs && sudo mkdir ptero"
4. "cd ptero && sudo mkdir nginx && sudo mkdir certs && sudo mkdir logs && sudo mkdir var && sudo mkdir database"
5. "sudo nano docker-compose.yml"
6. Paste, Edit and Save - https://github.com/saneece/Pterodactyl/blob/main/panel/docker-compose.yml
7. "cd nginx"
8. "sudo nano panel.conf"
9. Paste, Edit and Save - https://github.com/saneece/Pterodactyl/blob/main/panel/panel.conf
10. "cd .." Don't forget the space between CD and .. so you only go back one level
11. start container with "docker compose up -d"
12. test the url and the direct IP of the panel
13. Make the user for the panel with "docker compose run --rm panel php artisan p:user:make"< /br>
