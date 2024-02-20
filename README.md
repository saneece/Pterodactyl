# Pterodactyl

## Notes for Beginners to Linux

- Anytime you need to run commands, it's best to use PuTTY or Solar-PuTTY so you can copy and paste.
- To copy FROM a PuTTY panel, just highlight the text you want to copy and press `Ctrl + V` on your local machine.
- To copy TO a PuTTY panel, copy from your local machine, use arrow keys to set your cursor where you want the data, then right-click.
- To save in a nano editor, use `Ctrl + X`, then `Y`, then `Enter`.

## Setup Ptero Panel VM and Container:

1. Setup Docker VM per standard Debian Setup [here](https://github.com/saneece/Scripts/blob/main/New%20Debian%20Setup.yml).
2. Create the NPM url/certs for panel.domain.com and wings1.domain.com.
3. Navigate to `dockconfigs` directory and create `ptero` directory: `cd dockconfigs && sudo mkdir ptero`.
4. Inside `ptero` directory, create necessary directories: `sudo mkdir nginx && sudo mkdir certs && sudo mkdir logs && sudo mkdir var && sudo mkdir database`.
5. Create and edit `docker-compose.yml`: `sudo nano docker-compose.yml`. 
   - Paste, Edit, and Save the content from [here](https://github.com/saneece/Pterodactyl/blob/main/panel/docker-compose.yml).
6. Navigate to `nginx` directory: `cd nginx`.
7. Create and edit `panel.conf`: `sudo nano panel.conf`.
   - Paste, Edit, and Save the content from [here](https://github.com/saneece/Pterodactyl/blob/main/panel/panel.conf).
8. Navigate back to the root directory: `cd ..`.
9. Start the container: `docker-compose up -d`.
10. Test the URL and the direct IP of the panel.
11. Make the user for the panel: `docker-compose run --rm panel php artisan p:user:make`.

## Setup Ptero Wings VM and Container:

1. Setup Docker VM per standard Debian Setup [here](https://github.com/saneece/Scripts/blob/main/New%20Debian%20Setup.yml).
2. Create the NPM url/certs for panel.domain.com and wings1.domain.com.
3. Navigate to `dockconfigs` directory and create `wings1` directory: `cd dockconfigs && sudo mkdir wings1 && cd wings1/`.
4. Create and edit `docker-compose.yml`: `sudo nano docker-compose.yml`.
   - Paste, Edit, and Save the content from [here](https://github.com/saneece/Pterodactyl/blob/main/wings/docker-compose.yml).
5. Start the container: `docker-compose up -d`.
6. Check the logs: `docker-compose logs`.
7. Go to your panel and login using the user you created in the panel setup.
8. Go to Admin Settings (top right) > Location (left menu) > Create New (mid top right).
9. Name it whatever you like > create.
10. Go to "Nodes" (left menu) > Create New (mid top right).
    - Name it after the server hostname.
    - Write a description if you want.
    - Node Visibility = Public.
    - FQDN = the domain of the server.
    - Communicate over SSL = "Use SSL Connection".
    - Behind Proxy = "Behind Proxy".
    - Total Memory = <max memory - 2GB in MiB>.
    - Memory Over-Allocation = 0.
    - Total Disk Space = <max disk space - 20GB in MiB>.
    - Disk Over-Allocation = 0.
    - Daemon Port = 443.
    - Daemon SFTP port = 2022.
    - Create node.
11. Go back into the node and click on "Configuration" and copy all the data.
12. On the Docker VM for wings, edit `config.yml`: `cd /etc/pterodactyl && sudo nano config.yml`.
    - Paste the copied config from the panel.
    - Paste the contents of [this file](https://github.com/saneece/Pterodactyl/blob/main/wings/config.yml) at the end.
    - Adjust the timezone if needed.
    - Adjust the Network settings.
13. Save the document (ctrl+x > y > enter).
14. Navigate to the `wings1` directory: `cd && cd dockconfigs/wings1`.
15. Restart the container: `docker-compose up -d --force-recreate`.
16. Check your node status heart in the Ptero Panel.
17. Go to your Panel and click on the Node you created.
18. Go to the "Allocation" tab and enter the IP address of the Docker VM.
19. In the Ports field, put 27000-27999.
20. Click "Create Server" at the bottom.
