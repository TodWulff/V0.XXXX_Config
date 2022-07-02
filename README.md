# Skippy_Config
Repo for the Klipper Config directory of Voron 0.1 SN XXXX.  These works are largely drawn from, and customized for the v0.1 with a Pi 4 + BTT SKR Pico, based on previous works https://github.com/TodWulff/V2.2526_Config/, name3ly a Voron 2.4 350^3 model built in 4Q21 that is also running klipper.

Useful Links:
- https://jinja.palletsprojects.com/en/2.10.x/templates/
- https://www.klipper3d.org/Overview.html
- https://github.com/Klipper3d/klipper
- https://github.com/VoronDesign/Voron-2/raw/Voron2.4/Manual/Assembly_Manual_2.4r2.pdf
- https://docs.vorondesign.com/
- https://klipper.discourse.group/
- Nice Klipper macro tutorial from Mental: https://klipper.discourse.group/t/macro-creation-tutorial/30
- Current Wiring: is a todo...

Summer 2022 Build:  Order placed from Mellow3D via AliExpress on 28 May 2022.  Received Kit 12 Jun 2022.  First print 21 Jun 2022.

Voron Kit Feedback Server Invite:  
 - https://bit.ly/3igPTpJ (resolves to https://discord.com/invite/RyAGnb9y3G)
 - My Mellow 3D printer kit feedback ch: https://discord.com/channels/877549316913365083/980201614906368020
 - My Formbot printer kit feedback ch: https://discord.com/channels/877549316913365083/885942140012744744
 - My ERCF DFH Kit feedback ch: https://discord.com/channels/877549316913365083/928716501480009768

FYSA, as is the case with my other printer, be advised that these configs are a big Work In Process (WIP).  The printer is a new
build in June 2022.  Just so y'all know about same...  Usual disclaimers apply.  YMMV.  blah blah blah.

DISCLAIMER:  I am not at fault if your use of these info/data/code/macros/configs result in injury/damage/issues/etc.
Your use of these info/data/code/macros/configs acknowledges these risks and indicates a full imdemnification
of myself from any potential outcomes of your decision to use the info/data/code/macros/configs presented herein.

Printer Details, for those who may be interested:
- to do
 
>>> LOOK >>> Also, be advised that this set of configs requires manual installation of some components on top of a fresh install of the host OS and Klipper/Moonraker/Mainsail:

A) Kiauh's 'shell_commands' [an unofficial extension], 
  - github repo tools:  Shell_Commands is used herein to facilitate execution of config_blah.sh scripts which enables the automagic push and pull of these config files, as well as my nozzle cam v4l2 settings, and some other UI goodness such as macro buttons to kick off curl commands to control external devices such as my Wyze Cam day/night modes and smart outlets for the printer and the external enclosure I have.
  - sms comms tools:  Shell_Commands is used to aid in the programmatic sending of SMS messages from the printer, in the event of a filament sensor event or other programmatically detectable events.

B) (Might go here, but with the size of the v0.1 and due to it having manual bed screws, I am hesitant to do so) Klicky & the related 'z_calibration',

C) I'll likely eventually add LED and make use of LED_Effects by Hagbard (originallly penned by Mental).

D) Git (done at host's OS level)

Also, with Alex's help (Discord @ALEX#8260, THANK YOU!), I was able to get an automated construct setup such that:

1) On every boot, the config_pull.sh script runs (see _startup_autoexec.cfg) and pulls down changes from the git repo.
  - in case I make changes that are pushed directly to the repo from elsewhere other than the printer config_push.sh script.
  - If config changes are indeed downloaded as a result of the check, upon completion of the download, Klipper service restarts.
  
2) On print_end event, the config_push.sh script runs to push a snapshot of the printer's current config out to the git repo.
  - I am still cogitating on what other, if any, events to use to trigger a config backup.
  
3) Macro buttons on Mainsail enables manual initiation of either a push or pull from Klipper's Mainsail UI.
  
These activities are codified in those scripts and the associated backups of the various .cfgs they impute a backup of, as evidenced in the contents herein.

Of note, there are a couple of .cfgs/.confs I have overtly nix'd from herein - Moonraker's Telegram Bot's config (has the bot API key therein) and Twilio's config (it too has an API key therein).  If an example is desired to look at, take a peek at the initial commit's history and you'll see it therein.  The token has since been revoked, so don't spin yer wheels. ;)
https://github.com/TodWulff/V2.2526_Config/blob/8ac0f96c20a67e028ace10987d7467840370a18f/telegram.conf
and 
https://github.com/TodWulff/V0.XXXX_Config/blob/f90551cdc37836612b2d163e66131581d5c0a3d2/.twiliorc

I've also elected to ignore the save_variables file that houses configuration data for the ERCF, etc. so that old config data doesn't overwright current data.

Of possible interest, I am also making use of the User Interactions module I pulled together and published earlier this month (June 2022) to ping the user to keep heaters on or not when a print completes, is canceled, or otherwise terminates in a programmatic manner.  For additional details, see: https://github.com/TodWulff/Klipper_UserInteraction

Enjoy and Happy Printing!

~MHz

Also, https://i.imgur.com/IHALDMd.png  Making use of Mainsail's console filtering to quiet the noise... ;)

Useful Tidbits:

	NPP Regex to fix copy/pastes from Mailsail Console:

    Win Find:  ^([0-9][0-9]:[0-9][0-9]:[0-9][0-9])\r\n(.*)$
		Replace:   \1 \2
		
		*nix Find:  ^([0-9][0-9]:[0-9][0-9]:[0-9][0-9])\n(.*)$
		Replace:    \1 \2

		
