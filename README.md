# Pterodactyl
Notes for begginers to linux:</br>
Anytime you need to run commands, it's best to use PuTTY or Solar-PuTTY so you can copy and paste.</br>
To copy FROM a PuTTY panel, just highlight the test you want to copy and ctrl+v on your local machine</br>
To copy TO a PuTTY panel, copy from your local machine > use arrow keys to set your cursor where you want the data > right click</br>
To save in a nano editor, use "ctrl+x > y > enter"</br>
</br>
Setup Ptero Panel VM and Container:</br>

1. Setup Docker VM per standard Debian Setup here: https://github.com/saneece/Scripts/blob/main/New%20Debian%20Setup.yml</br>
Note: Investigate NOT setting Portainer is the default volume that the website states and isntead deploy using docker-compose and mapping volume else where to backup stacks deployed via Portainer </br>
2. Create the NPM url/certs for panel.domain.com and wings1.domain.com</br>
NOTE: </br>
Configure NPM for the Panel URL to pass http with the http port (801 in docker-compose.yml for Panel), but configure the SSL cert and force SSL </br>
Configure NPM for the Wings URL to pass http traffic with the https port (443 in docker-compose.yml for Wings), configure the SSL cert and force SSL </br>
3. "cd dockconfigs && sudo mkdir ptero"
4. "cd ptero && sudo mkdir nginx && sudo mkdir certs && sudo mkdir logs && sudo mkdir var && sudo mkdir database"
5. "sudo nano docker-compose.yml"
6. Paste, Edit and Save - https://github.com/saneece/Pterodactyl/blob/main/panel/docker-compose.yml (to save in the nano editor: ctrl+x > y > enter)
7. "cd nginx"
8. "sudo nano panel.conf"
9. Paste, Edit and Save - https://github.com/saneece/Pterodactyl/blob/main/panel/panel.conf (to save in the nano editor: ctrl+x > y > enter)
10. "cd .." Don't forget the space between CD and .. so you only go back one level
11. Start the container with "docker compose up -d"
12. Test the URL and the direct IP of the panel
13. Make the user for the panel with "docker compose run --rm panel php artisan p:user:make"< /br>


Setup Ptero Wings VM and Container:

1. Setup Docker VM per standard Debian Setup here: https://github.com/saneece/Scripts/blob/main/New%20Debian%20Setup.yml</br>
</br>
Note: this is where all of your games will live and run so I recommend around 32GB or higher RAM and 100-200GB of storage to start. Account for the VM's overhead if you want to dedicate a full 32 to the games.
</br>
3. Create the NPM url/certs for panel.domain.com and wings1.domain.com (if you didn't do this already in step 2 of the panel configuration)</br>
</br>
NOTE: </br>
Configure NPM for the Panel URL to pass http with the http port (801 in docker-compose.yml for Panel), but configure the SSL cert and force SSL </br>
Configure NPM for the Wings URL to pass http traffic with the https port (443 in docker-compose.yml for Wings), configure the SSL cert and force SSL </br>
</br>
4. "cd dockconfigs && sudo mkdir wings1 && cd wings1/"
5. "sudo nano docker-compose.yml"
6. Paste, Edit and Save - https://github.com/saneece/Pterodactyl/blob/main/wings/docker-compose.yml (to save in the nano editor: ctrl+x > y > enter)
7. "docker compose up -d"
8. "docker compose logs" You will see errors about no config.yml here. This is on purpose
9. Go to your panel and login using the user you created in step 13 of the panel walk through
10. Go to Admin Settings (top right) > Location (left menu) > Create New (mid top right)
11. Name it what ever, mine is "prod home" > create
12. Go to "Nodes" (left menu) > Create New (mid top right)
13. Name it after the server host name (prod-wings-01 for me)
14. Write a description if you want > Location = "prod home" or whatever you made in step 10
15. Node Visibility = Public
16. FQDN = the domain of the server "wings1.nevanstech.com"
17. Communicatie over SSL = "Use SSL Connection" - We will be providing SSL via NPM
18. Behind Proxy = "Behind Proxy" - again, we will be providing SSL via NPM
19. Total Memory = Take the max memory you assigned the server and subtract 2gb and put that amount in form of MiB. 1024 * x = Total Memory
20. Memory Over-Allocation = 0
21. Total Disk Space = Take the max you assigned the server and subtract 20gb and put that amount in form of MiB. 1024 * x = Total Disk Space
22. Disk Over-Allocation = 0
23. Daemon Port = 443
24. Daemon SFTP port = 2022
25. Create node.</br>
</br>
Note: If you go back to the Nodes overview, you will see a red heart. This is normal. This is the same issue that we saw in our docker compose logs. We need to create the "config.yml" on the server but we needed some data from this node before we could create it.
</br>
27. Go back into the node and click on "Configuration" and copy all the data out to a text editor
28. On the Docker VM for wings, "cd /etc/pterodactyl && sudo nano config.yml" (use putty)
29. Paste the config from your panel here: DON'T SAVE YET! Move to next step.
30. Now paste the contents of this file at the end of you config.yml from the last step: https://github.com/saneece/Pterodactyl/blob/main/wings/config.yml
31. Adjust the timezone if needed
32. Adjust the Network settings you copied in step 28. Specifically, the "dns:" Change the DNS to reflect your local DNS server if you have one or to your prefered public. I like 1.1.1.1, 1.0.0.1 and 9.9.9.9 personally. Google is over rated.</br>
</br>
Note: If you don't have any other services on this machine, you shouldn't need to edit anything other than the DNS. If you DO have other services (not recommended), they might be overlapping with the network so you may need to edit tghe "interfaces:" > "subnet:" and "gateway:" settings to adjust the network.
</br>
33. Save the document (ctrl+x > y > enter
34. "cd && cd dockconfigs/wings1"
35. "docker compose up -d --force-recreate"
36. Check your node status heart in the Ptero Panel. If the heart isn't green, check all of the config.yml settings to make sure you didn't miss type something and check your NPM URL configuration to match what was written in the notes of step 2.
