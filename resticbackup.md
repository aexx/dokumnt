
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

# mount
restic -r sftp:ok8cp5@raspberrypi:/media/INTENSO2/backup/restic/repo01 mount mnt/1
```


## Suche nach einer Datei in allen Backups:


``` bash
restic -r sftp:ok8cp5@raspberrypi:/media/INTENSO2/backup/restic/repo01 ls d065e6ac |grep alex
restic -r sftp:ok8cp5@raspberrypi:/media/INTENSO2/backup/restic/repo01 find sinus154.txt

```

## Backup / Sicherung Restic ueber RClone / rclone serve restic

``` bash
$ rclone serve restic -v durchaux-t-cloud:rr
2022/10/03 17:26:33 NOTICE: webdav root 'rr': Serving restic REST API on http://127.0.0.1:8080/
2022/10/03 17:27:33 INFO  : 
Transferred:             0 / 0 Bytes, -, 0 Bytes/s, ETA -
Elapsed time:       1m1.6s

2022/10/03 17:28:33 INFO  : 
Transferred:             0 / 0 Bytes, -, 0 Bytes/s, ETA -
Elapsed time:       2m1.6s
[...] 
2022/10/03 18:02:03 INFO  : : Creating repository
2022/10/03 18:02:33 INFO  : 
Transferred:           608 / 608 Bytes, 100%, 106 Bytes/s, ETA 0s
Transferred:            1 / 2, 50%
Elapsed time:      36m1.6s
Transferring:
 *                                        config:100% /155, 154/s, 0s

## DIREKT
restic --repo rclone:pcloud:rstc/direkt init

rclone lsd pcloud:rstc/direkt
[ -z $RESTIC_PASSWORD ] || for i in /aexdisk/bigaex/Aex/ ; do aexrestic.sh rclone:pcloud:rstc/direkt/ $i; done

```

**im anderen Terminal / other Terminal**

``` bash
$ export RESTIC_PASSWORD=Ganzarggeheim7b
$
$ restic -r rest:http://localhost:8080/ init
created restic repository 1d1xxxx767 at rest:http://localhost:8080/

Please note that knowledge of your password is required to access
the repository. Losing your password means that your data is
irrecoverably lost.
$ 
$ aexrestic.sh rest:http://localhost:8080/ /home/ok8cp5/xxx/TEMP/  ## script: aexrestic.sh

VERSION:         restic 0.9.6 compiled with go1.13.4 on linux/amd64
REPO:            rest:http://localhost:8080/   
RESTIC_PASSWORD: ....xxx....   
SAVEPATH:        /home/ok8cp5/xxx/TEMP/

Snapshots(letzte/last 3): ... restic -r rest:http://localhost:8080/ snapshots 
Create restic-Backup: ... restic -r rest:http://localhost:8080/ --verbose backup /home/ok8cp5/xxx/TEMP/ --exclude-file=/tmp/restic-exclude.txt 
open repository
repository 1d1xxx07 opened successfully, password is correct
lock repository
load index files
start scan on [/home/ok8cp5/xxx/TEMP/]
start backup on [/home/ok8cp5/xxx/TEMP/]
scan finished in ...
[...] 
snapshot ccxxx5b saved
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

$ restic -r rest:http://localhost:8080/ snapshots
repository 1dxxx07 opened successfully, password is correct
ID        Time                 Host        Tags        Paths
----------------------------------------------------------------------------
cc0bf15b  2022-10-03 18:10:38  aspxxxxx50              /home/ok8cp5/xxx/TEMP
a947507a  2022-10-03 18:14:27  aspxxxxx50              /home/ok8cp5/xxx/Adr
----------------------------------------------------------------------------
2 snapshots



```


###### Ende       
