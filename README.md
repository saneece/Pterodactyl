# Pterodactyl



Setup Ptero Panel VM and Container:

1. Setup Docker VM per standard Debian Setup here: https://github.com/saneece/Scripts/blob/main/New%20Debian%20Setup.yml</br>
Note: Investigate NOT setting Portainer is the default volume that the website states and isntead deploy using docker-compose and mapping volume else where to backup stacks deployed via Portainer </br>
2. Create the NPM url/certs for panel.domain.com and wings1.domain.com
3. cd to /dockconfigs and "sudo mkdir ptero"
4. "cd ptero && sudo mkdir nginx && sudo mkdir certs && sudo mkdir logs && sudo mkdir var"
5. sudo nano docker-compose.yml
6. Paste, Edit and Save - https://github.com/saneece/Pterodactyl/blob/main/panel/docker-compose.yml
7. cd nginx && sudo nano panel.conf
8. Paste, Edit and Save - https://github.com/saneece/Pterodactyl/blob/main/panel/panel.conf
9. start container with "docker-compose up -d"
10. test the url and the direct IP of the panel
11. Make the user for the panel with "docker-compose run --rm panel php artisan p:user:make"< /br>
