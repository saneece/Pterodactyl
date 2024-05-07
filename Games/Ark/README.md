# Pterodactyl Server Setup

## Create the server in Ptero Admin

### Admin Panel in Ptero: https://ptero.nevanstech.com/admin

  1. Create server with Egg (if needed to download, follow https://github.com/saneece/Pterodactyl)
  2. Allocate Game Port, Query Port and RCON Port during setup
  3. Set Port Foward in Firewall to forward to the query port (27015) and add to steam favorites with publicIP:27015

## Configure the server in Ptero

### Game Server in Ptero: https://ptero.nevanstech.com/

  1. Choose server
  2. Go to the "Startup" tab of the server in Ptero
  3. Set Server Name to "Kingdom - MAP NAME"
  4. Add mods from Games/Ark/Ark Server Files/2_GameUserSettings INI/Mods/DefaultMods.txt
    - (If doing a mod map, make sure it's the first MOD to be loaded)

## Subscribe to chosen mods from step 4 of the previous section

### Ark: SE Workshop Collections:

  1. All Collections "Ark > Workstop > Your Files (Drop down on the right side menu) > Your Favorites > Show: By Trep (on the top of the page) > Collections"
   - OR: https://steamcommunity.com/profiles/76561198001411306/myworkshopfiles/?section=collections&appid=346110
  2. Create new collection or choose existing (Kingdom Default)
  3. Subscribe to Collection to begin pre-downloading mods

## Edit Game Files to tweak settings, configure mods and add player white list

### Files > ShooterGame\Saved\Config\LinuxServer\

  1. Add Game.ini from Games/Ark/Ark Server Files/1_Game INI/DefaultGameINI.txt
  2. Add GameUserSettings.ini from Games/Ark/Ark Server Files/2_GameUserSettings INI/DefaultGameUserSettingsINI.txt
    - Add Mods settings to GameUserSettings.ini from Games/Ark/Ark Server Files/2_GameUserSettings INI/Mods/

### Files > ShooterGame/Binaries/Linux

  1. Upload "PlayersJoinNoCheckList.txt" from Z:\Documents\Games\Ark\Ark Server Files\Config\_SERVER SETUP
