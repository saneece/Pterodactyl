# Pterodactyl
Notes for begginers to linux:</br>
To copy out of a PuTTY panel, just highlight the test you want to copy and ctrl+v on your local machine</br>
To copy TO a PuTTY panel, copy from your local machine > use arrow keys to set your cursor where you want the data > right click</br>
To save in a nano editor, use "ctrl+x > y > enter"</br>
</br>
Setup Ptero Panel VM and Container:</br>
</br>
1. Setup Docker VM per standard Debian Setup here: https://github.com/saneece/Scripts/blob/main/New%20Debian%20Setup.yml</br>
Note: Investigate NOT setting Portainer is the default volume that the website states and isntead deploy using docker-compose and mapping volume else where to backup stacks deployed via Portainer </br>
2. Create the NPM url/certs for panel.domain.com and wings1.domain.com</br>
NOTE: </br>
Configure NPM for the Panel URL to pass http with the http port (801 in docker-compose.yml for Panel), but configure the SSL cert and force SSL </br>
Configure NPM for the Wings URL to pass http traffic with the https port (443 in docker-compose.yml for Wings), configure the SSL cert and force SSL </br>
3. "cd /dockconfigs && sudo mkdir ptero"
4. "cd ptero && sudo mkdir nginx && sudo mkdir certs && sudo mkdir logs && sudo mkdir var && sudo mkdir database"
5. "sudo nano docker-compose.yml"
6. Paste, Edit and Save - https://github.com/saneece/Pterodactyl/blob/main/panel/docker-compose.yml (to save in the nano editor: ctrl+x > y > enter)
7. "cd nginx"
8. "sudo nano panel.conf"
9. Paste, Edit and Save - https://github.com/saneece/Pterodactyl/blob/main/panel/panel.conf (to save in the nano editor: ctrl+x > y > enter)
10. "cd .." Don't forget the space between CD and .. so you only go back one level
11. start container with "docker compose up -d"
12. test the url and the direct IP of the panel
13. Make the user for the panel with "docker compose run --rm panel php artisan p:user:make"< /br>


Setup Ptero Wings VM and Container:

1. Setup Docker VM per standard Debian Setup here: https://github.com/saneece/Scripts/blob/main/New%20Debian%20Setup.yml</br>
2. Create the NPM url/certs for panel.domain.com and wings1.domain.com (if you didn't do this already in step 2 of the panel configuration)</br>
NOTE: </br>
Configure NPM for the Panel URL to pass http with the http port (801 in docker-compose.yml for Panel), but configure the SSL cert and force SSL </br>
Configure NPM for the Wings URL to pass http traffic with the https port (443 in docker-compose.yml for Wings), configure the SSL cert and force SSL </br>
3. "cd /dockconfigs && sudo mkdir wings1"
4. "sudo nano docker-compose.yml"
5. Paste, Edit and Save - https://github.com/saneece/Pterodactyl/blob/main/wings/docker-compose.yml (to save in the nano editor: ctrl+x > y > enter)
6. "docker compose up -d"
7. "docker compose logs" You will see errors about no config.yml here. This is on purpose
8. Go to your panel and login using the user you created in step 13 of the panel walk through
9. Go to Admin Settings (top right) > Location (left menu) > Create New (mid top right)
10. Name it what ever, mine is "prod home" > create
11. Go to "Nodes" (left menu) > Create New (mid top right)
12. Name it after the server host name (prod-wings-01 for me)
13. Write a description if you want > Location = "prod home" or whatever you made in step 10
14. Node Visibility = Public
15. FQDN = the domain of the server "wings1.nevanstech.com"
16. Communicatie over SSL = "Use SSL Connection" - We will be providing SSL via NPM
17. Behind Proxy = "Behind Proxy" - again, we will be providing SSL via NPM
18. Total Memory = Take the max memory you assigned the server and subtract 2gb and put that amount in form of MiB. 1024 * x = Total Memory
19. Memory Over-Allocation = 0
20. Total Disk Space = Take the max you assigned the server and subtract 20gb and put that amount in form of MiB. 1024 * x = Total Disk Space
21. Disk Over-Allocation = 0
22. Daemon Port = 443
23. Daemon SFTP port = 2022
24. Create node. You will see a red heart. This is normal. This is the same issue that we saw in our docker compose logs. We need to create the "config.yml" on the server but we needed some data from this node before we could create it.
25. Go back into the node and click on "Configuration" and copy all the data out to a text editor
26. On the Docker VM for wings, "cd /etc/pterodactyl *&& sudo nano config.yml" (use putty)
27. Paste the config from here: https://github.com/saneece/Pterodactyl/blob/main/wings/config.yml DON'T SAVE YET! Move to next step.
28. Copy the three lines "uuid:" "token_id:" "token:" and the string of text after each one and paste them over the same three lines in the copied config
29. Edit the "cert" and "key" lines to have the correct URL. You won't use them but just incase you need to in the future
30. Adjust the timezone if needed
31. Adjust the Network "Interface:", "dns:", "interfaces:" > "subnet:" and "gateway:" if neccessary. If you don't have any other services on this machine, you shouldn't need to edit anything other than the DNS. Change the DNS to reflect your local DNS server if you have one or to your prefered public. I like 1.1.1.1, 1.0.0.1 and 9.9.9.9 personally. Google is over rated.
32. Save the document and check your node status in the Ptero Panel. If the heart isn't green, check all of the config.yml settings to make sure you didn't miss type something and check your NPM URL configuration to match what was written in the notes of step 2.
