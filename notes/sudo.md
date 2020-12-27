But what does adding a user to the sudo group in Ubuntu mean? By default, Ubuntu allows sudo users to execute any program as root with their password. There are a few ways we can check this information. The first way is as Nick with sudo -l .

The important information are in the last lines. This is saying that Nick (as part of the sudo group) may run all commands as any user on any machine.  

There's another way to view this information and that's with visudo. This opens the sudo policy file. The sudo policy file is stored in /etc/sudoers. We can do it here as Nick, but we would need to use sudo if we want to edit it since it can only be edited by the root user (using just visudo as Nick actually gives a permission denied).

This gives the same information as sudo -l but it has one difference; the "%sudo" indicates that it's for the group, sudo. There are other groups in this file such 
as "admin". This is where administrators can set what programs a user in a certain group can perform and whether or not they need a password. You may have seen 
sometimes %sudo ALL=(ALL:ALL) ALL NOPASSWD: ALL. That NOPASSWD part says that the user that is part of the sudo group does not need to enter their local password 
to use sudo privileges. Generally, this is not recommended - even for home use.

