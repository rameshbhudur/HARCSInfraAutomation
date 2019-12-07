Linux VM : ADDEMO/Rameshbellampalli*11
Windows VM : WINADAdmin/Rameshbellampalli*11
bellamra@rameshbhudurgmail.onmicrosoft.com /Ramesh*11
chris@rameshbhudurgmail.onmicrosoft.com/JoanC*11

ssh ADDEMO@13.77.58.154

   #Network Config
 /etc/sysconfig/network-scripts/ifcfg-etho
 #Host Name
 /etc/sysconfig/network
 #local address  resolver
 /etc/hosts
#Restart
/etc/init.d/network restart

#Domain Join
sudo realm join -v -U username domainname
e.g. sudo realm join -v -U bellamra harcs.onmicrosoft.com

check
id bellamra@harcs.onmicrosoft.com

Enable remote administration via SSH 

SSH Policy
Sudo Policy

 #SSH configuration
 vim /etc/ssh/sshd_config
 ## Allow AD groups to login
 AllowGroups ADGroupName@domainname
 e.g. AllowGroups domain-users@lab.local

 #sudoers file
 sudo visudo
 %ADGroupName@domainname ALL=(ALL:ALL) ALL

 ##Optimistic mapping of AD SID-RID into Linux uid
 1. UID and GID number space creates range 100k
 2. SID and hash into UID + AD user's RID   



 My Work
https://docs.microsoft.com/en-us/azure/active-directory-domain-services/active-directory-ds-join-rhel-linux-vm

#WIndows AD Join 
https://docs.microsoft.com/en-us/azure/active-directory-domain-services/active-directory-ds-admin-guide-join-windows-vm-portal

#Manage AD and Policies
https://docs.microsoft.com/en-us/azure/active-directory-domain-services/active-directory-ds-admin-guide-administer-group-policy

 sudo vi /etc/hosts

 127.0.0.1 harcs-rhel.harcs.onmicrosoft.com harcs-rhel

 sudo yum install realmd sssd krb5-workstation krb5-libs samba-common-tools

 sudo realm discover HARCS.ONMICROSOFT.COM

 kinit bellamra@HARCS.ONMICROSOFT.COM

 sudo realm join --verbose HARCS.ONMICROSOFT.COM -U 'bellamra@HARCS.ONMICROSOFT.COM'
##
 Outcome
  Resolving: _ldap._tcp.harcs.onmicrosoft.com
 * Performing LDAP DSE lookup on: 10.1.0.5
 * Performing LDAP DSE lookup on: 10.1.0.4
 * Successfully discovered: harcs.onmicrosoft.com
Password for bellamra@HARCS.ONMICROSOFT.COM:
 * Required files: /usr/sbin/oddjobd, /usr/libexec/oddjob/mkhomedir, /usr/sbin/sssd, /usr/bin/net
 * LANG=C LOGNAME=root /usr/bin/net -s /var/cache/realmd/realmd-smb-conf.TANHYZ -U bellamra@HARCS.ONMICROSOFT.COM ads join harcs.onmicrosoft.com
Enter bellamra@HARCS.ONMICROSOFT.COM's password:DNS update failed: NT_STATUS_INVALID_PARAMETER

Using short domain name -- HARCS
Joined 'HARCSADDEMO' to dns domain 'harcs.onmicrosoft.com'
No DNS domain configured for harcsaddemo. Unable to perform DNS Update.
 * LANG=C LOGNAME=root /usr/bin/net -s /var/cache/realmd/realmd-smb-conf.TANHYZ -U bellamra@HARCS.ONMICROSOFT.COM ads keytab create
Enter bellamra@HARCS.ONMICROSOFT.COM's password:
 * /usr/bin/systemctl enable sssd.service
Created symlink from /etc/systemd/system/multi-user.target.wants/sssd.service to /usr/lib/systemd/system/sssd.service.
 * /usr/bin/systemctl restart sssd.service
 * /usr/bin/sh -c /usr/sbin/authconfig --update --enablesssd --enablesssdauth --enablemkhomedir --nostart && /usr/bin/systemctl enable oddjobd.service && /usr/bin/systemctl start oddjobd.service
 * Successfully enrolled machine in realm
 ##

#Login as Local user
ssh ADDEMO@13.73.118.206
#Login as AD
ssh -l bellamra@HARCS.ONMICROSOFT.COM 13.73.118.206
#id
uid=377601110(bellamra@harcs.onmicrosoft.com) gid=377600513(domain users@harcs.onmicrosoft.com) groups=377600513(domain users@harcs.onmicrosoft.com),377600520(group policy creator owners@harcs.onmicrosoft.com),377600572(denied rodc password replication group@harcs.onmicrosoft.com),377601102(dnsadmins@harcs.onmicrosoft.com),377601104(aad dc administrators@harcs.onmicrosoft.com),377601107(sudoroot@harcs.onmicrosoft.com) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
## Non SudoRoot User
ssh -l chris@HARCS.ONMICROSOFT.COM 13.73.118.206
#id
uid=377601112(chris@harcs.onmicrosoft.com) gid=377600513(domain users@harcs.onmicrosoft.com) groups=377600513(domain users@harcs.onmicrosoft.com),377601108(serviceaccounts@harcs.onmicrosoft.com) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023

#List users with password
less /etc/passwd
#List users
users
#List Groups
groups
vi /etc/group
#Get group name id
[root@HarcsADDemo sssd]# getent group ADDEMO
ADDEMO:x:1000:

#Add SudoRoot users 
%sudoroot@harcs.onmicrosoft.com ALL=(ALL:ALL) ALL

# Sudo to specific user account
sudo -i -u ADDEMO
sudo -i -u chris@HARCS.ONMICROSOFT.COM

#Add ServiceAccount Users
%serviceaccounts@harcs.onmicrosoft.com ALL=(ADDEMO) ALL

