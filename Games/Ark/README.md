# Pterodactyl Server Setup

## Create the server in Ptero Admin

### Admin Panel in Ptero: https://ptero.nevanstech.com/admin

  1. Create server with Egg (if needed to download, follow https://github.com/saneece/Pterodactyl)
  2. Allocate Game Port (27016) and add 2 more ports. 1 is Query Port (27015) and the other is the RCON Port (27020) during setup
  3. Uncheck "Start Server when Installed"
  4. Set the "Backup Limit" to "2"
  5. Set the "Memory" and "Disk Space"
  6. Choose the "Nest" and the "Egg"
  7. Set the "Server Password" and the "Admin Password"
  8. Set the "Server Map" (including if is a MOD map)
  9. Set the "Server Name" to "Kingdom: MAP_NAME"
  10. Add mods from Games/Ark/Ark Server Files/2_GameUserSettings INI/Mods/DefaultMods.txt and add any additional
      - Add Mods settings to GameUserSettings.ini from Games/Ark/Ark Server Files/2_GameUserSettings INI/Mods/
     - Make sure to update the "[SessionSettings]" after the first reboot
    - If it's a MOD map, make sure it's loaded first. 
  12. Set Port Foward in Firewall to forward to the query port (27015), the game port (27016) and add to steam favorites with publicIP:27016
    - Don't port forward 27020 (RCON)
    - Once the server is setup, make sure that 27016

### Edit Game Files to tweak settings, configure mods and add player white list

  1. Go to the Game Server in Ptero: https://ptero.nevanstech.com/
  2. Start the server untill you see RCON error messages
  3. Go to the "Files" tab
  4. Copy contents from "Games/Ark/Ark Server Files/1_Game INI/DefaultGameINI.txt" and paste into "/home/container/ShooterGame/Saved/Config/LinuxServer/Game.ini" on the server
  5. Copy contents from "Games/Ark/Ark Server Files/2_GameUserSettings INI/DefaultGameUserSettingsINI.txt" and paste into "/home/container/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini" on the server
     - Add Mods settings to GameUserSettings.ini from Games/Ark/Ark Server Files/2_GameUserSettings INI/Mods/
     - Make sure to update the "[SessionSettings]" after the first reboot

### Files > ShooterGame/Binaries/Linux

  1. Upload "PlayersJoinNoCheckList.txt" from "GitHub > Games/Ark/Ark Server Files/PlayersJoinNoCheckList.txt" to 

## Configure the server in Ptero

### Create Reboot Schedule

  1. Go to the Game Server in Ptero: https://ptero.nevanstech.com/
  2. Go to Schedules tab of the server in Ptero
  3. Click "Create Schedule"
  4. Name is "Reboot Schedule"
  5. Set the Minute box to 0
  6. Set the Hour box to 6
  7. Click "Create Schedule"
  8. Go into the Reboot Schedule and click "New Task"
  9. Action = Send Power Action
  10. Payload = Restart the server
  11. Click "Create Task"

### Create Backup Schedule

  1. Go to Schedules tab of the server in Ptero
  2. Click "Create Schedule"
  3. Name is "Backup Schedule"
  4. Set the Minute box to 0
  5. Set the Hour box to 2
  6. Click "Create Schedule"
  7. Go into the Backup Schedule and click "New Task"
  8. Action = Create Backup
  10. Click "Create Task"

## Subscribe to chosen mods from step 4 of the previous section

### Ark: SE Workshop Collections:

  1. Go to Steam > All Collections
     - Ark >
     - Workshop >
     - Your Files (Drop down on the right side menu) >
     - Your Favorites >
     - Show: By Trep (on the top of the page) >
     - Collections
       - OR: https://steamcommunity.com/profiles/76561198001411306/myworkshopfiles/?section=collections&appid=346110
  3. Create new collection or choose existing (Kingdom Default)
  4. Subscribe to Collection to begin pre-downloading mods

## Local Client Configuration:

1. Go to "\ARK\Engine\Config" then open "BaseEngine.ini" within notepad, CTRL+F and fine the line "AspectRatioAxisConstraint=AspectRatio_MaintainXFOV" and replace it to "AspectRatioAxisConstraint=AspectRatio_MaintainYFOV" 
2. Then ingame adjust the FOV slider to your liking, but beware, FOV is much wider now so setting the slider to 20-30% is enough.
3. In-game, Set graphics preset to "High", turn off motion blur and scale down new FOV slider
