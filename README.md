# backup_bash
BACKUP


## WHAT IS BACKUP?
"backup" is a set of scripts written in bash that are used to make
incremental backups of your files.

The program revolves around the rsync tool.
You can back up files and / or directories:
 - in local mode (between external hard drives, for example)
 - in remote mode (backups between the local and a remote computer).


## INSTALLATION
The most recommended way to run 'backup' is by installing it through
the script "0-BACKUP_INSTALLER":
 - $ bash 0-BACKUP_INSTALLER
 
After this user only must write "backup" in a terminal.

It is also possible to run 'backup' without installing it, opening a terminal
and executing "bash backup" from the directory where the script is located.

Installing 'backup' also creates a shortcut in the directory
"$ HOME/.user_scripts/desktop_links".

This allows user to run "backup" with a single click.
In the event that user use xfce4 as desktop environment,
can easily add this shortcut to the xfce4-panel.

I don't know how to do this in other desktop environments.

Installation via '0-BACKUP_INSTALLER' script creates the following structure:

       [link]  /usr/local/bin/backup -> /usr/local/bin/BACKUP.d/backup_starter
       /usr/local/bin/BACKUP.d/
              ├── backup
              ├── backup_starter
              └── resources
                     ├── backup.cfg
                     ├── backup.png
                     └── scripts
                            ├── aux_script
                            ├── errors_modder
                            ├── log_modder
                            └── remote_script


## EXECUTION
"backup" can be executed with or without arguments.

####Without Arguments
If "backup" is executed without arguments, the files or directories
to be backed up will be added to 'backup.cfg' file.
Next time that 'backup' runs, it will ask to user if he wants to back up
the files / directories saved in 'backup.cfg'.

####With Arguments
The arguments must correspond to SOURCE and DESTINATION.
  - $ backup SOURCE DESTINATION
  - $ bash backup SOURCE DESTINATION

If "backup" is executed with arguments, the program won't remember them
in future executions.

"backup" supports options
 - **'_-c_' or '_--content_' (Only with ORIGIN / DESTINATION arguments)**
 - **'_-h_' or '_--help_'**

The '-c' or '--content' option will back up the SOURCE content to DESTINATION
(instead of copying the ORIGIN folder in DESTINATION).
  - $ backup -c SOURCE DESTINATION
  - $ bash backup -c SOURCE DESTINATION 

In any case, when "backup" is executed with SOURCE and DESTINATION arguments
and without '-c' or '--content' options, if SOURCE is a LOCAL directory the
program will ask to user if must back up the SOURCE folder or only its content.

The '-h' or '--help' option displays 'backup' usage options.
For a more detailed explanation, you can read the manual:
  - $ man backup


## REMOTE BACKUPS
It is possible to make backups between 2 computers
(local->remote or remote->local).

The remote machine must have the rsync package installed:
  - In Debian systems based:     $ sudo apt install rsync
  - In Arch Linux systems based: $ sudo pacman -S rsync
  
In addition, the sshd daemon must be active on the remote machine:
  - $ sudo systemctl start sshd

The syntax, in case you want to run "backup" with parameters
between computers should be the following:
  - $ backup LOCAL_SOURCE remote_user@remote_IP:REMOTE_DESTINATION
  - $ backup remote_user@remote_IP:REMOTE_SOURCE LOCAL_DESTINATION
  

Examples:
  - $ backup /home/pedro/Documents jose@192.168.0.10:/home/jose/Documents
  - $ backup jose@192.168.0.10:/home/jose/Documents /home/pedro/Documents
  
