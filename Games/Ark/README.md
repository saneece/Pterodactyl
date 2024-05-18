# Pterodactyl Server Setup

## Create the server in Ptero Admin

### Admin Panel in Ptero: https://ptero.nevanstech.com/admin

  1. Create server with Egg (if needed to download, follow https://github.com/saneece/Pterodactyl)
  2. Allocate Game Port, Query Port and RCON Port during setup
  3. Set Port Foward in Firewall to forward to the query port (27015) and add to steam favorites with publicIP:27015
  4. Go to Build COnfiguration tab and set Backup Limit to 2 on the server after it's created

## Configure the server in Ptero

### Game Server in Ptero: https://ptero.nevanstech.com/

  1. Choose server
  2. Go to the "Startup" tab of the server in Ptero
  3. Set Server Name to "Kingdom - MAP NAME"
  4. Add mods from Games/Ark/Ark Server Files/2_GameUserSettings INI/Mods/DefaultMods.txt
     - (If doing a mod map, make sure it's the first MOD to be loaded)

### Create Reboot Schedule

  1. Go to Schedules tab of the server in Ptero
  2. Click "Create Schedule"
  3. Name is "Reboot Schedule"
  4. Set the Minute box to 0
  5. Set the Hour box to 6
  6. Click "Create Schedule"
  7. Go into the Reboot Schedule and click "New Task"
  8. Action = Send Power Action
  9. Payload = Restart the server
  10. Click "Create Task"

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

## Edit Game Files to tweak settings, configure mods and add player white list

### Files > ShooterGame\Saved\Config\LinuxServer\

  1. Copy contents from Games/Ark/Ark Server Files/1_Game INI/DefaultGameINI.txt and paste into /home/container/ShooterGame/Saved/Config/LinuxServer/Game.ini on the server
  2. Copy contents from Games/Ark/Ark Server Files/2_GameUserSettings INI/DefaultGameUserSettingsINI.txt and paste into /home/container/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini on the server
     - Add Mods settings to GameUserSettings.ini from Games/Ark/Ark Server Files/2_GameUserSettings INI/Mods/

### Files > ShooterGame/Binaries/Linux

  1. Upload "PlayersJoinNoCheckList.txt" from Z:\Documents\Games\Ark\Ark Server Files\Config\_SERVER SETUP

# Local Client Configuration:

1. Go to "\ARK\Engine\Config" then open "BaseEngine.ini" within notepad, CTRL+F and fine the line "AspectRatioAxisConstraint=AspectRatio_MaintainXFOV" and replace it to "AspectRatioAxisConstraint=AspectRatio_MaintainYFOV" 
2. Then ingame adjust the FOV slider to your liking, but beware, FOV is much wider now so setting the slider to 20-30% is enough.
3. In-game, Set graphics preset to "High", turn off motion blur and scale down new FOV slider
