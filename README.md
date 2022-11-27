# General documentation for Linux

## Samba

### smb.conf:
S: Applied individually
G: Applied globally

*admin users (S)*
eg: admin users = desktop

*browseable / browsable (S)*
Controls if the share is seen in the list of available shares in a net view (public or not)
eg : browseable = yes / browsable = yes

*force group (S)*
eg : force group = sudo

*force user (S)*
eg : force user = Nero

*public / guest ok (S)*
eg : public = no / guest ok = no

*hide files (S)*
Can hide files, but affects performance since SMB needs to check if files are asked to be hidden or not.
eg : hide files = /home/Nero/hiddenfolder

*max connections (S)*
If max connections are greater than 0, they will be refused. 0=unlimited
eg : max connections = 10

*null passwords (G)*
Allow or disallow access to accounts that have null passwords
NOTE: Needs to have a null password, refer to smbpasswd.
eg : null passwords = yes

*directory / path (S)*
Specifies directory where the user is given access
eg : path = /home/Nero

*writeable (S)*
If this parameter is set to yes, then users of a service may create or modify files in the service's directory
eg : writeable = yes

*read only (S)*
An inverted synonym is writeable.
If this parameter is set to yes, then users of a service may NOT create or modify files in the service's directory
eg : read only = yes

*root / root dir / root directory (G)*
Server will chroot to the directory on startup. Not needed, but adds a extra layer of security.
eg : root directory = /home/Nero

*username level (G)*
SMB tries to guess the real Unix username, as DOS clients send usually an all uppercase username. By default, it tries all lowercase, followed by the username with the first letter capitalized, then gives up. If the parameter is non-zero, the behavior changes. The higher the number selected, the more combinations will be tried, but the search will be slower, so it is needed only when UNIX systems have case sensitive usernames.
eg : username level = 0

*usershare allow guests (G)*
Controls whether user defined shares are allowed to be accesed by non-authenticated users. Equivalent of guest ok = yes.
eg : usershare allow guests = no

*usershare max shares (G)*
Specifies number of user defined shares that are allowed to be created by users belonging to the grup owning the usershare directory.
eg : usershare max shares = 0

*valid users (S)*
List of users that should be allowed login. If it is empty, then any user can log in.
eg : valid users = smbuser

*workgroup (G)*
Controls workgroup server name when queried by clients. 
eg : workgroup = WORKGROUP

*writable / write ok / writeable (S)*
Inverted synonym for read only.
eg : writeable = nore

### User management:
OPTIONS
smbpasswd -a: Available only as root, specifies that the username following will be added to the local smbpasswd file, then prompts to type the new password. Option is ignored if the username already exists inside the file, and treated as a regular password change.

smbpasswd -x: Avaliable only as root, deletes the user from the smbpasswd file.

smbpasswd -d: Available only as root, this disables the user instead of deleting it.

smbpasswd -e: Available only as root, this enables the user, must be previously disabled.

smbpasswd -n: Specifies that the user has the password set to null. The specific option must be selected on the smb.conf file (null passwords = yes) when used.

pdbedit -L -V: Lists all available users, V to be verbose.
