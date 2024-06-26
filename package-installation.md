
# Packages & Install


### Linux Version ?

Debain/Ubuntu/Mint: `cat /etc/issue ; lsb_release -a  ; cat /etc/lsb-release`     
RedHat/CentOS: `cat /etc/redhat-release`

---

## apt & dpkg & aptitude 


    apt-file search ForkManager.pm  # Suchen nach Paketen /search packages
    psuche () {  apt-cache search "$1" |grep -i "$1"; } ; psuche midnight

    sudo add-apt-repository ppa:user/ppa-name
    
    # nala
    sudo apt install -t nala nala
    nala show falkon  ; nala list falkon
    sudo nala update ;countdown 4; nala list --upgradable
    psuche () {  nala search "$1" |grep -v "──"|grep -i "$1"; } ; psuche dillo
    


### Pakete nach Groesse sortiert / sort packages by size

    time (pkgl=/dev/shm/dpkg-groessen.txt ;dpkg -l|grep "ii"|awk '{print $2}' |while read a;do echo "$(dpkg -s $a|grep Installed-Size|cut -c17-)  $a ";done|tee $pkgl ;sort -n $pkgl )
    # **Besser:** 
    time (pkgl=/dev/shm/dpkg-groessen_2.txt ;dpkg-query -W -f='${Installed-Size} ${Package} \t\t\t\t\t ${Status} \n'|grep -v deinstall|tee $pkgl ; sort -n $pkgl ) # Pakete nach Groesse sortiert /sort packages by size , gross brummer 
    aptitude -O installsize -F'%p %I' search '~i'  #Pakete nach Groesse sortiert / sort packages by size

### Zeitpunkt, dpkg, apt, datum, date, install

    ( PKG="linux-image" ; zegrep -i $PKG /var/log/dpkg.log* ; egrep -Ri $PKG /var/log/dpkg.log* ) # |egrep -i "upgrad|instal"    # dpkg apt zeitpunkt datum date install

    find /var/lib/dpkg/info -name "*.list" -exec stat -c $'%n\t%y' {} \; | sed -e 's,/var/lib/dpkg/info/,,' -e 's,\.list\t,\t,' | sort > ~/dpkglist.dates
    
    01 dpkg --get-selections | sed -ne '/\tinstall$/{s/[[:space:]].*//;p}' | sort > ~/dpkglist.selections
    02 join -1 1 -2 1 -t $'\t' ~/dpkglist.selections ~/dpkglist.dates > ~/dpkglist.selectiondates
    03 find /var/lib/dpkg/info -name "*.list" -mtime -4 | sed -e 's,/var/lib/dpkg/info/,,' -e 's,\.list$,,' | sort > ~/dpkglist.recent
    04 join -1 1 -2 1 -t $'\t' ~/dpkglist.selections ~/dpkglist.recent > ~/dpkglist.recentselections
    
list, search/suche, find

    $ dpkg -c paket.deb  # list files / Dateien

    $ export DIR=/var/cache/apt/archives ;ls $DIR ;du -ms $DIR ;psg apt;read -p" ==> WEITER ???? " ; countdown 14; df -am ; export CMD="sudo apt-get" ; $CMD autoclean ; countdown 2 ;$CMD autoremove ; countdown 2 ;df -am ;ls $DIR ;du -ms $DIR ; \
    ODER
    $ platz () { df -m / ;ls /var/cache/apt/archives/|wc -l ; } ;platz ;sudo apt clean;sudo apt autoremove ;platz
    ODER
    $ platz () { df -m / ;ls /var/cache/apt/archives/|wc -l ; } ;platz >/dev/shm/platz1 ;sudo apt clean;sudo apt autoremove ;platz >/dev/shm/platz2 ; sdiff /dev/shm/platz1 /dev/shm/platz2  # neu


    $ dpkg -S resolv.conf  # search/suche find/finde Dateien/files 

**Proxy** - Eintraege in `/etc/apt/apt.conf`  o.  `/etc/apt/apt.conf.d/00proxy`   

    Acquire::http::Proxy "http://www-m1.dienste.telxxxx.de:8080";
    Acquire::http::proxy "http://192.168.1.112:3128";
    Acquire::http::Proxy "http://lgnas01:3128";

export

    $ dpkg --get-selections > Dateiname  #  sudo dpkg --set-selections < Dateiname  #  sudo dpkg --yet-to-unpack  #  sudo apt-get dselect-upgrade   ## Listen / lists - export / import

    
### Alte Kernel , old kernel

    $ dpkg -l|grep ii |grep linux
    $ pliste="" ; for i in 3.2.0-60 3.2.0-61 ; do sleep 0.3 ; pliste="linux-headers-${i} linux-headers-${i}-generic linux-headers-${i}-generic-pae linux-image-${i}-generic linux-image-${i}-generic-pae $pliste " ; echo "_____  $pliste"  ; done ; echo  -e "\n\n\nsudo apt-get remove --purge $pliste \n"
    # ____ ODER:____ 
    $ dpkg -l|grep ii |grep linux ; dpkg --get-selections | sed -ne '/\tinstall$/{s/[[:space:]].*//;p}'  |egrep "3.16.0-70|3.16.0-69"
    $ sudo apt-get remove --purge `dpkg --get-selections | sed -ne '/\tinstall$/{s/[[:space:]].*//;p}'  |egrep "3.16.0-70|3.16.0-69"`
    # ____ ODER:____ 
    $ dpkg -l 'linux-[ihs]*' | sed '/^ii/!d;/'"$(uname -r | sed "s/\([-0-9]*\)-\([^0-9]\+\)/\1/")"'/d;s/^[^ ]* [^ ]* \([^ ]*\).*/\1/;/[0-9]/!d' | tee zu_entfernende_Kernel
    $ vi zu_entfernende_Kernel  # evtl. die beiden letzten Kernel zum Aufheben aus Liste entfernen.
    $ cat zu_entfernende_Kernel | xargs sudo apt-get -y purge  
    $ rm zu_entfernende_Kernel 


install

    $ apt-get install bliblablub:i386




### Problem[e/s]


**Update LMDE** autokey probleme:  `$ sudo apt-get install gir1.2-notif ; sudo dpkg -i autokey-gtk_0.90.1-1.1_all.deb`


#### Key Probleme

GPG error debian.org **=> public key is not available**   

    $ apt-get update
    [...] W: GPG error: http://ftp.de.debian.org etch Release: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 9AA38DCD55BE302B [...] 

**Aktuellen Debian-Key holen **     
http://ftp-master.debian.org/keys.html => **Archive Keys** => **Active Signing Keys** => The current (2009/lenny) key can be downloaded here ...    

    $ export http_proxy=http://172.27.40.100:3128
    $ wget http://ftp-master.debian.org/ziyi_key_2006.asc -O new_key
    $ apt-key add new_key
    OK
    

**AUCH:**   

    ok8cp5@mint ~ $ gpg --keyserver keyserver.ubuntu.com --recv 5D654504F1A41D5E
    [...]
    gpg: Schlüssel F1A41D5E: Öffentlicher Schlüssel "SpiderOak Apt Repository <apt@spideroak.com>" importiert
    [...]
    ok8cp5@mint ~ $ gpg --export --armor 5D654504F1A41D5E | sudo apt-key add -
    OK

**Nochmal:**   

    W: Während der Überprüfung der Signatur trat ein Fehler auf. Das Repository wurde nicht aktualisiert und die vorherigen Indexdateien werden verwendet. GPG-Fehler: http://repository.spotify.com stable Release: Die folgenden Signaturen konnten nicht überprüft werden, weil ihr öffentlicher Schlüssel nicht verfügbar ist: NO_PUBKEY 13B00F1FD2C19886
    
    W: Fehlschlag beim Holen von http://repository.spotify.com/dists/stable/Release  
    
    W: Einige Indexdateien konnten nicht heruntergeladen werden. Sie wurden ignoriert oder alte an ihrer Stelle benutzt.
    [...] 

**Info v. spotify:**   

    $ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys D2C19886
    Executing: gpg --ignore-time-conflict --no-options --no-default-keyring --secret-keyring /tmp/tmp.0Bpg0SmN5P --trustdb-name /etc/apt/trustdb.gpg --keyring /etc/apt/trusted.gpg --primary-keyring /etc/apt/trusted.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys D2C19886
    gpg: Schlüssel D2C19886 von hkp-Server keyserver.ubuntu.com anfordern
    gpg: Schlüssel D2C19886: Öffentlicher Schlüssel "Spotify Public Repository Signing Key <operations@spotify.com>" importiert



Tages Zaehler **GUI Update Manager** zaehlt nicht hoch    

    $ sudo apt-get update 
    OK   http://de.archive.ubuntu.com precise Release.gpg
    OK   http://archive. [...] 
    W: Fehlschlag beim Holen von http://apt.spideroak.com/ubuntu-spideroak-hardy/dists/release/Release  
    [...] 
    
**Browser** => http://apt.spideroak.com  =>  `wget http://apt.spideroak.com/spideroak-apt-pubkey.asc -O new_key  => sudo apt-key add new_key  =>  sudo apt-get update`  


---


## rpm

**Beobachten/watch Update (background-process) => **  '' # watch -d -n 4 'df -am ; ps aux |grep rpm |grep -v grep' # '' 


    $ sudo zypper in gcc make kernel-source kernel-syms Xalan-c Xerces-c   # SuSE rpm packages pakete kompilieren

    $ # 2020-12-26 opensuse-tumbleweed
    $ sudo zypper addlock unison  # paket sperren, wird nicht aktualisiert, bei unison evtl. wichtig 
    $ sudo zypper patch-check
    $ sudo zypper list-patches
    $ sudo zypper patch -g security
      
    $ rpm -qa --last | head -20 #letzten 20 installationen
    $ rpm -i[-F]hv[v] --test blablabla.rpm
    $ for i in $(rpm -ql sane); do du -ms $i; done ## "Brummer" in Paketen suchen
    $ rpm -qa --queryformat "%{SIZE}\t%{NAME}\n" |sort -n ## Alle Pakete nach Groesse sortiert
    $ for i in --basedon --provides --requires; do echo -e "\n\t $i ----\t\n" ; rpm -q $i xfce  ; done |more
    $ ## FTP-Web-Seite speichern --> grep patch ftp.uni-bremen.de.txt|awk '{print $2}'|awk -F"=" '{print $2}'|awk -F">" '{print $1}' >/patch.txt
    $ for i in $(rpm -qa); do rpm -qi $i|grep -qi Packman && echo "$i";done  #install. Packman-Pakete finden
    $ cd /var/lib/YaST2/you/mnt/i386/update/9.1/rpm/i586 ; ls |awk -F"." '{print $1}'|uniq -d|while read dat; do echo $dat;ls -ltr $dat*;echo;done  #unnoetige Patches finden
    $ rpm -qf /etc/passwd  # zu welchem paket gehoert datei xy # query/find package owning file xy
    $ rpm -q --queryformat "%{SIZE}\t%{NAME}\t%{VERSION}-%{RELEASE}\t\"%{INSTALLTIME:date}\"\n" varnish


---


## Andere/Other

### Gentoo

    $ layman -S ; emerge --sync ; emerge --search vim  # gentoo
    



