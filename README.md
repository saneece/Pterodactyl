# Pterodactyl

Notes for beginners to Linux:

- Anytime you need to run commands, it's best to use PuTTY or Solar-PuTTY so you can copy and paste.
- To copy FROM a PuTTY panel, just highlight the text you want to copy and press `Ctrl + V` on your local machine.
- To copy TO a PuTTY panel, copy from your local machine, use arrow keys to set your cursor where you want the data, then right-click.
- To save in a nano editor, use `Ctrl + X`, then `Y`, then `Enter`.

## Setup Ptero Panel VM and Container:

1. Setup Docker VM per standard Debian Setup [here](https://github.com/saneece/Scripts/blob/main/New%20Debian%20Setup.yml).
   - Note: Investigate NOT setting Portainer as the default volume that the website states and instead deploy using docker-compose and mapping volume elsewhere to backup stacks deployed via Portainer.
2. Create the NPM url/certs for panel.domain.com and wings1.domain.com.
   - **Note:**
     - Configure NPM for the Panel URL to pass http with the http port (801 in docker-compose.yml for Panel), but configure the SSL cert and force SSL.
     - Configure NPM for the Wings URL to pass http traffic with the https port (443 in docker-compose.yml for Wings), configure the SSL cert, and force SSL.
3. `cd dockconfigs && sudo mkdir ptero`
4. `cd ptero && sudo mkdir nginx && sudo mkdir certs && sudo mkdir logs && sudo mkdir var && sudo mkdir database`
5. `sudo nano docker-compose.yml`
   - Paste, Edit, and Save - [panel/docker-compose.yml](https://github.com/saneece/Pterodactyl/blob/main/panel/docker-compose.yml) (to save in the nano editor: `Ctrl + X`, then `Y`, then `Enter`).
6. `cd nginx`
7. `sudo nano panel.conf`
   - Paste, Edit, and Save - [panel/panel.conf](https://github.com/saneece/Pterodactyl/blob/main/panel/panel.conf) (to save in the nano editor: `Ctrl + X`, then `Y`, then `Enter`).
8. `cd ..` (Don't forget the space between CD and .. so you only go back one level).
9. Start the container with `docker compose up -d`.
10. Test the URL and the direct IP of the panel.
11. Make the user for the panel with `docker compose run --rm panel php artisan p:user:make`.

## Setup Ptero Wings VM and Container:

1. Setup Docker VM per standard Debian Setup [here](https://github.com/saneece/Scripts/blob/main/New%20Debian%20Setup.yml).
   - Note: This is where all of your games will live and run, so I recommend around 32GB or higher RAM and 100-200GB of storage to start. Account for the VM's overhead if you want to dedicate a full 32 to the games.
2. Create the NPM url/certs for panel.domain.com and wings1.domain.com (if you didn't do this already in step 2 of the panel configuration).
   - **Note:**
     - Configure NPM for the Panel URL to pass http with the http port (801 in docker-compose.yml for Panel), but configure the SSL cert and force SSL.
     - Configure NPM for the Wings URL to pass http traffic with the https port (443 in docker-compose.yml for Wings), configure the SSL cert, and force SSL.
3. `cd dockconfigs && sudo mkdir wings1 && cd wings1/`
4. `sudo nano docker-compose.yml`
   - Paste, Edit, and Save - [wings/docker-compose.yml](https://github.com/saneece/Pterodactyl/blob/main/wings/docker-compose.yml) (to save in the nano editor: `Ctrl + X`, then `Y`, then `Enter`).
5. `docker compose up -d`
6. `docker compose logs` You will see errors about no config.yml here. This is on purpose.
7. Go to your panel and login using the user you created in step 13 of the panel walkthrough.
8. Go to Admin Settings (top right) > Location (left menu) > Create New (mid top right).
9. Name it whatever, mine is "prod home" > create.
10. Go to "Nodes" (left menu) > Create New (mid top right).
    - Name it after the server hostname (prod-wings-01 for me).
    - Write a description if you want > Location = "prod home" or whatever you made in step 10.
    - Node Visibility = Public.
    - FQDN = the domain of the server "wings1.nevanstech.com".
    - Communicate over SSL = "Use SSL Connection" - We will be providing SSL via NPM.
    - Behind Proxy = "Behind Proxy" - again, we will be providing SSL via NPM.
    - Total Memory = Take the max memory you assigned the server and subtract 2gb and put that amount in the form of MiB. 1024 * x = Total Memory.
    - Memory Over-Allocation = 0.
    - Total Disk Space = Take the max you assigned the server and subtract 20gb and put that amount in the form of MiB. 1024 * x = Total Disk Space.
    - Disk Over-Allocation = 0.
    - Daemon Port = 443.
    - Daemon SFTP port = 2022.
    - Create node.
   - Note: If you go back to the Nodes overview, you will see a red heart. This is normal. This is the same issue that we saw in our docker compose logs. We need to create the "config.yml" on the server but we needed some data from this node before we could create it.
11. Go back into the node and click on "Configuration" and copy all the data out to a text editor.
12. On the Docker VM for wings, `cd /etc/pterodactyl && sudo nano config.yml` (use PuTTY).
13. Paste the config from your panel here: DON'T SAVE YET! Move to the next step.
14. Now paste the contents of [this file](https://github.com/saneece/Pterodactyl/blob/main/wings/config.yml) at the end of your config.yml from the last step.
15. Adjust the timezone if needed.
16. Adjust the Network settings you copied in step 28. Specifically, the "dns:" Change the DNS to reflect your local DNS server if you have one or to your preferred public. I like 1.1.1.1, 1.0.0.1 and 9.9.9.9 personally. Google is overrated.
   - Note: If you don't have any other services on this machine, you shouldn't need to edit anything other than the DNS. If you DO have other services (not recommended), they might be overlapping with the network so you may need to edit the "interfaces:" > "subnet:" and "gateway:" settings to adjust the network.
17. Save the document (ctrl+x > y > enter).
18. `cd && cd dockconfigs/wings1`
19. `docker compose up -d --force-recreate`
20. Check your node status heart in the Ptero Panel. If the heart isn't green, check all of the config.yml settings to make sure you didn't mistype something and check your NPM URL configuration to match what was written in the notes of step 2.
21. Go back to your Panel and click on the Node you created (if it's green. If it's not green, keep troubleshooting).
22. Go to the "Allocation" tab and on the right, put in the IP address of the Docker VM (the server docker is running on that hosts Wings).
23. In the Ports field, put 27000-27999. This will supply 1000 ports for this single node to use. You won't ever run out.

## Import an "unsupported" game (egg):

1. Go to [this link](https://github.com/parkervcp/eggs/tree/master) and find the game you want.
2. Download the .json file.
3. In your panel, go to Admin settings (top right) > Nests (bottom on the left side menu).
4. Click "Create New" > Name it the same as the game > Save.
5. Click on "Nests" in the left-hand menu again.
6. Click "Import Egg" in the top right (green button).
7. Click "Choose File" and select the .json file.
8. Click the dropdown under "Associated Nest" and select the Nest you created in step 4.
9. Click "Import".
10. Now go to Servers in the left-hand menu.
11. Click "Create New".
12. Select your Nest under the "Nest Configuration" and fill out the rest of the data.
13. Click "Create Server" at the bottom. If you missed anything required, it will tell you and not let you create the server.
