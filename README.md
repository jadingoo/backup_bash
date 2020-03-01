# backup_bash
Make incremental backups using rsync.

Backup install:  bash 0-BACKUP_INSTALLER
__________________________________

backup()
Use rsync to make incremental backups
between local and/or remote files/directories.

Use: backup [OPTION] [SOURCE DESTINATION]

Compatible with Debian and Arch Linux based systems.
Make incremental backups between local and/or remote files/directories
using rsync.
Remote backups needs start sshd service on remote computerr
(sudo systemctl start sshd).

       # WITHOUT PARAMETERS:

       Files or directories used when execute backup without parameters
       will be stored in '/usr/local/bin/BACKUP.d/resources/backup.cfg',
       and will be remembered for future backups.

       Local directory backups take precedence over remote directory backups,
       regardless of their order in the 'backup.cfg' file.

       # WITH PARAMETERS:

       Allow to use options:
         -c,  --content
                 Sync content of SOURCE into DESTINATION.
                 Both parameters are directories.

         -h,  --help
                 Show help message and exit.

       Without options, sync SOURCE (file or directory) into DESTINATION.

       Running with parameters requires 2 parameters (3 if use --content option).

       These parameters corresponds respectively with
       SOURCE and DESTINATION, and can be a local/remote file/directory.

       It must be enclosed in single quotation marks if there are spaces in its name.

       These directories will not be stored in 'backup.cfg',
       so they will not be remembered in future backups.

          examples: backup 'SOURCE_DIR' 'DESTINATION_DIR'
                    backup --content 'SOURCE_DIR' 'DESTINATION_DIR'

                    backup 'LOCAL_SOURCE' 'remote_hostname@remote_IP:REMOTE_DESTINATION'
                    backup 'remote_hostname@remote_IP:SOURCE' 'LOCAL_DESTINATION'

       ____________________________________________________________________________

       ## Installation via '0-BACKUP_INSTALLER' script creates the following structure:

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
