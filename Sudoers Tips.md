##Prompt for password always
defaults timestamp_timeout=0 //System wide setting
defaults:username timestamp_timeout=0 //user specific setting

#Allow user to only one commands
username ALL=(root) /sbin/ # can run any commands under sbin

##Allow user to run command without argument

username ALL=(root) /sbin/fdisk ""

##Allow users to start /stop some services
username ALL=(root) /etc/init.d/http restart /etc/init.d/httpd status

##what permissions i have
sudo -l

##Notes
https://www.sudo.ws/man/1.8.15/sudoers.man.html#SUDOERS_FILE_FORMAT
The sudoers file is composed of two types of entries: aliases (basically variables) and user specifications (which specify who may run what).
When multiple entries match for a user, they are applied in order. Where there are multiple matches, the last match is used (which is not necessarily the most specific match).
There are four kinds of aliases: User_Alias, Runas_Alias, Host_Alias and Cmnd_Alias.