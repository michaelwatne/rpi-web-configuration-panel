# rpi-web-configuration-panel
This web configuration panel is designed for users to manage their Raspberry Pi on a web browser instead of a standard terminal client or the terminal itself! If you manage a ton of devices, sometimes having to access your pi from SSH can be a hassle, especially when you have to run multiple commands on different devices!
## PREREQUISTES
To be able to use this, you need to have the following:
- Apache2 Web Server!
- PHP 7
- Raspberry Pi with Raspbian (any distro should work)
- Node and NPM (to run XTerm JS)
- [XTerm JS (for Command Line Emulation)](https://xtermjs.org/)
- [Mod Auth External](https://packages.debian.org/sid/httpd/libapache2-mod-authnz-external)
## INSTALLATION
This is a simple installation! Follow these instructions carefully!
1. Move the folder *RPiConf* to the root of your Raspberry Pi. Contents MUST be in that folder! Your directory should look like this:
![root dir example](https://i.imgur.com/eqIbHqx.png)

2. Move the folder *RpiWeb* to your web server (for example: */var/www/html/RpiWeb*)
3. Add the following line to your **rc.local** file:
```/rpiConf/startup.sh```
4. Run the following commands:
```sh
sudo chmod -R 777 /rpiConf
sudo chmod -R 755 /var/www/RpiWeb
```
*Note: Change /var/www/RpiWeb to where you set your web files*

5. Add the following to either your defailt site configuration or to the configuration of the RpiWeb before the </Virtualhost> tag:
```conf
<Location /RpiWeb>
  AuthType Basic
  AuthName "Restricted"
  AuthBasicProvider external
  AuthExternal pwauth
  Require user pi
  #change pi to whatever you want to authenticate as
</Location>
```
6. Restart your Raspberry Pi

###PRO TIP: Create a new VirtualHost or edit your default.conf in your web server and direct it to your RpiWeb directory! This will save you from having to type in the directory all the time! If you create a new VirtualHost, create a .local domain and create a new DNS entry to access it! (For example: rpiconfig.local).

##USAGE
To use this, open up your web browser and type in the following:
http://your.rpi.server.address/RpiWeb
You can properly test out the configuration by trying out one of the system modules such as the UID light. If the lights flash when you enable it, you configured everything correctly!
