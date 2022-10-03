
# ResticBackup


## Installation
Version in OS Repository [ zu alt / too old ] - Download: https://github.com/restic/restic/releases (restic-0.9.6.tar.gz)  


``` bash
$ sudo cp -a ~/bigaex/Install/Linux/Backup/restic/0.9.6/restic_0.9.6_linux_amd64 /usr/local/bin/  # restic install
$ cd /usr/local/bin/ && sudo chmod +x restic_0.9.6_linux_amd64 && sudo ln -s restic_0.9.6_linux_amd64 restic && ls -ltra
```
## Syntax


``` bash
export RESTIC_PASSWORD=ganzarggeheim


restic init --repo /dev/shm/restic-test  # restic repository initialisieren
restic -r sftp:ok8cp5@lgnas:/mnt/disk/volume1/restic/ init  # restic repository ueber sftp initialisieren


restic -r /dev/shm/restic-test/ backup /home/ok8cp5/Dropbox/ --exclude-file=/tmp/restic-exclude.txt
restic -r /dev/shm/restic-test/ snapshots
restic -r /dev/shm/restic-test/ check
restic -r /dev/shm/restic-test/ stats
restic -r /dev/shm/restic-test/ list snapshots  # [blobs|packs|index|snapshots|keys|locks]
restic -r /dev/shm/restic-test/ ls 50557402  # List(e) files/Dateien in(m) snapshot
restic -r sftp:ok8cp5@lgnas:/mnt/disk/volume1/restic/ key add




```


## Beispiele






### latitude


``` bash
restic init -r sftp:ok8cp5@raspberrypi:/media/INTENSO2/backup/restic/repo01/ init


aexrestic.sh sftp:ok8cp5@raspberrypi:/media/INTENSO2/backup/restic/repo01/
  restic -r sftp:ok8cp5@raspberrypi:/media/INTENSO2/backup/restic/repo01/ check
  restic -r sftp:ok8cp5@raspberrypi:/media/INTENSO2/backup/restic/repo01 snapshots

aexrestic.sh sftp:ok8cp5@raspberrypi:/media/INTENSO2/backup/restic/repo01 ~
  restic -r $REPO --verbose backup ${SAVEPATH} --exclude-file=$EXCLUDEFILE

restic -r sftp:ok8cp5@raspberrypi:/media/INTENSO2/backup/restic/repo01 stats
restic -r sftp:ok8cp5@raspberrypi:/media/INTENSO2/backup/restic/repo01 ls a8044cab


# restore
restic -r sftp:ok8cp5@raspberrypi:/media/INTENSO2/backup/restic/repo01 restore d065e6ac --target /dev/shm/restoreretic/ --include /home/ok8cp5/test-Sync-02/DEBIAN/DebianGNU-LinuxBible.pdf


restic -r sftp:ok8cp5@raspberrypi:/media/INTENSO2/backup/restic/repo01 mount mnt/1
```


#### Suche nach einer Datei in allen Backups:


``` bash
restic -r sftp:ok8cp5@raspberrypi:/media/INTENSO2/backup/restic/repo01 ls d065e6ac |grep alex
restic -r sftp:ok8cp5@raspberrypi:/media/INTENSO2/backup/restic/repo01 find sinus154.txt


```










###### Ende       
