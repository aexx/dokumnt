
# Linux Allgemein
## Befehle



```bash

#
# Analyse -> aex-make-md5diffs.sh
nur-md5-aus-diff () { cat ${1} |grep -v __ > ${1}_nur-md5; }  # nur-md5-aus-diff loeschmi_0427_OptiP_bigaex_DIFF 
nur-basename-md5-aus-diff () { rm -fv ${1}_nur-basename-md5 ; cat ${1} |while read line; do echo $line|egrep -v " __ "|awk 'BEGIN{FS="/"}{print $NF}' >> ${1}_nur-basename-md5 ;done }  # nur-basename-md5-aus-diff XXXX_ok8cp5_bigaex_DIFF
cat md5list2024-06-12_1147_aspiX3950_home_ok8cp5_bigaex_sort_md5|while read line; do nurmd5=$(echo $line|cut -c-32); grep -q $nurmd5 md5list2024-06-12_1148_aspiX3950_media_ok8cp5_Intenso7B_bigaex_sort_md5 || printf "\n\n $line NICHT GEFUNDEN\n\n"  ; printf ":" ; done
#
in .i3/config add line:  # workspace_layout <default|stacking|tabbed> 
#
cat /path/to/your/image_part$n.0* | gzip -dc | partclone.chkimg -s - -L check$n.log  # check redo backup image 
#
AKD=~/.config/autokey/data ; [ -d $AKD ] && cd $AKD && tar -zcvf /home/ok8cp5/bigaex/Aex/Linux/config/autokey/data.$(uname -n).$(date +%F).tgz ../data  
#
ssdeep -rp -t94 *  # rekursiv nach aehnlichen Dateien suchen, sie sich zu 94 % aehneln     
#
chattr +i /mountpoint  ## Schreibschutz fuer leeren Mountpoint 




## lgnas
ok8cp5@LG-NAS:~$ alias aexmesg='dmesg |perl -ne "BEGIN{\$a= time()- qx!cat /proc/uptime!}; s/\[\s*(\d+)\.\d+\]/localtime(\$1 + \$a)/e; print \$_;"'
ok8cp5@LG-NAS:~$ echo ;aexmesg |egrep -i "initialised|hd|boot"


```


## Links


http://dynebolic.org/ #Audio Video Live-CD  
http://www.avasys.jp/english/index_e.html  #Druckertreiber Cups  
http://www.instalinux.com #netz install iso erzeugen  
http://www.heise.de/demobilise-me/?r=/  


## Hardware

**Acer Aspire One A110** http://www.aaowiki.de , **Acer Revo RL70** (ct 2012.21)  
**ThinkPad X121e** https://answers.launchpad.net/ubuntu/+source/gnome-nettool/+question/132667 http://www.heise.de/ct/11/22/links/072.shtml  
**Shuttle SZ68R5** (ct 2012.11) , ** Fujitsu Esprimo Q510** (ct 2012.15) MegaMount DA-74003 (http://www.digitus.info)  
Linux PCs: https://www.tuxedocomputers.com  



### Hardware Probleme


**Hardwareschalter oder Taste(nkombination) wirkt nicht**   
-  Einige Hardwareschalter funktionieren nur während des Systemstarts bevor Ubuntu (Linux) gestartet ist (z.B. beim Acer Aspire 1825PTZ).   
-  Beim Acer Aspire One entfernt man "Hard blocked" durch einmaliges Betätigen der Hardwaretaste während sich das Netbook im BIOS-Setup befindet. 

        dmesg | egrep 'radio|kill|switch'
        lsmod | egrep '_acpi|_bluetooth|intel_oaktrail|_laptop|_rfkill|_wmi'   # Kernelmodul ist nicht geladen  


#### Android

- **ADB Android Device Unauthorized / USB Debugging aktiviert - Autorisierungs-Dialog erscheint nicht**   

        $ adb shell
        error: device unauthorized.
        ## Loesung/Solution: Exist. Keys umbenennen/move
        $ mv /home/ok8cp5/.android/adbkey /home/ok8cp5/.android/adbkey_Tablee
        ## Kabel Aus,- Anstecken


#### Chromebook R11

Touchpad config in bunsenlabs linux (Beryllium based on debian)   
https://wiki.debian.org/SynapticsTouchpad#Enable_tapping_on_touchpad

Enable tapping on touchpad:

```bash
$ egrep -i 'synap|alps|etps|elan' /proc/bus/input/devices

$ mkdir -p /etc/X11/xorg.conf.d
$ echo 'Section "InputClass"
        Identifier "libinput touchpad catchall"
        MatchIsTouchpad "on"
        MatchDevicePath "/dev/input/event*"
        Driver "libinput"
        Option "Tapping" "on"
EndSection' > /etc/X11/xorg.conf.d/40-libinput.conf
$ systemctl restart lightdm

```




### USB-Stick SD-Card Inhalt

**ACHTUNG: Neues Tool:** https://www.ventoy.net/en/index.html   

 
|     **USB Stick** | Groesse |   MB/sec | Inhalt - Beschreibung                                                                              |
|------------------:|:-------:|---------:|----------------------------------------------------------------------------------------------------|
|                   |         |          |                                                                                                    |
|     **t-systems** |  246 MB |    7.07  | puppy linux slacko_5.7                                                                             |
|         **krenn** |    2 GB |   --.--  | VENTOY , clonezilla-live-2.7.0 , linuxmint-21 (persistence)                                        |
|        **apacer** |    2 GB |   17.57  | VENTOY , porteus_5 (persist.), supergrub                                                           |
|      **cruzer** 4 |    4 GB |   --.--  | puppy linux fossapup64 (persist.)                                                                  |
|       **toshiba** |   32 GB |   30.14  | VENTOY, ubuntu-20.04, linuxmint-21 (persist.), redorescue-4.0.0, grml_2022, slax_12.2, porteus_5   |
|      **cruzer** 8 |    8 GB |   --.--  | unraid OS                                                                                          |
|  **Sandisk Rund** |    8 GB |   36.70  | chromeOS flex 2023                                                                                 |
|      **DataT102** |   32 GB |   --.--  | puppy linux fossapup64 (persist.), porteus_5 (IN ARBEIT, persist.)                                 |
|      **platinum** |   14 GB |   --.--  | VENTOY , bunsen-linux , peppermint-10-i386 . .                   *(stick evtl probleme u linux!)*  |
|  **Kingston vmx** |   16 GB |   --.--  | DEFEKT                                                                                             |
|      **Paradies** |   64 GB |   98.22  | VENTOY , Desinfect-2023 , bunsen-linux , fossapup64 , tuxedo ,                                     |
| **sdcard chromi** |   16 GB |   14.21  | VENTOY , linuxmint-21 (persist.)    data Partition                                                 |
|                   |    1 GB |   --.--  |                                                                                                    |
|                   |    1 GB |   --.--  |                                                                                                    |
|                   |         |          |                                                                                                    |
|                   |         |          |                                                                                                    |
|                   |         |          |                                                                                                    |


Installation __Multisystem__ auf apt-System

```bash
echo 'deb http://liveusb.info/multisystem/depot all main' | sudo tee /etc/apt/sources.list.d/multisystem.list
wget -q -O "-" http://liveusb.info/multisystem/depot/multisystem.asc | sudo apt-key add - 
sudo apt update && sudo apt install multisystem
```


## Tools 
### apt*Distributionen:  


    # sudo apt-get install ssh mdadm parcellite autokey-common vim unison-gtk colordiff meld pdftk rpl dwdiff inxi vim
    # sudo apt-get install poppler-utils handbrake-cli keepassx gxmessage gnome-tweak-tool nethogs gnome-encfs-manager
    # sudo apt-get install network-manager-kde ksshaskpass krename autokey-qt fonts-droid kcm-gtk kde-config-gtk gtk-theme-switch gtk2-engines-oxygen gtk3-engines-oxygen gtk-chtheme kde-style-qtcurve apper  # kubuntu-desktop oder kde-plasma-desktop plasma-desktop  # kde 
    ## INFO: vim war noetig, da Autokey beim vorinstallierten vi nicht richtig funktioniert hat!! 


### tools,packages,pakete,installieren,install


* kdeaddons3-konqueror , kdeaddons _(fish)_  , nmap , lynis , firestarter , nmon_x86_rhel4 , unetbootin , dstat , fldiff
* meld _(diff-gui)_  , inotify-tools , cups-pdf , parcellite _(clipboard,zwischenablage)_  , fusedav _(mount a WebDAV)_  
* asunder , miro , handbrake _(Filme f Mobilgeraete)_  , autokey _(hotstrings,tastatur-kuerzel)_  , phatch _(Photo Batch)_  
* rpmerizor _(Perlskript,Dateien als RPM)_ , translate , xVideoServiceThief _(xVST, video download)_  , minitube , speedometer 
* units , passwordstore , tomb _(Ordner verschluesseln)_ , PAC , Whohas , bagside.com , playonlinux , jripper , conduit 
* datacrow.net , imgseek , Gnac , EtherApe , jbackpack , CCFE , Sentinella , Droopy _(Dateiaustausch)_  , Hugin _(Panoramabilder)_  
* Heldenviewer_ClipGrab _(youtube)_  , Termit _(xterm)_  , qtube.de , transcoder _(Video konvert.)_  , XtreemFS _(RaidFS)_  , atunes _(Musik)_   
* apt-cacher-ng _(apt proxy)_  , mp3diags , duff,rdfind _(doppelte Dateien)_  , debian-goodies _(checkrestart)_  
* HTTrack _(Webseiten herunterladen,Offline-Reader)_  , DeVeDe _(DVD)_  , Movgrab _(youtube-Download)_  , csvdb _(CSV mit SQL)_  
* sslh _(Port-Wrapper,protocol demultiplexer)_  , bum _(Boot Up Manager,Services,daemons)_  , gsmartcontrol _(smartctl GUI)_  , pdfcrop 
* reptyr _(moving running programs between ptys)_ , spek _(acoustic spectrum analyser)_  , ncdu _(disk usage cli)_  
* bleachbit _(aufraeumen,clean disk)_  , jmtpfs _(Handy mounten)_ , inxi _(tool hw hardware cpu memory weather wetter)_  
* stacer _(ubuntu optimieren, auf github)_ , csplit _(zB aus einer vcard mehrere machen)_ , lsat _(security,sicherheit,check,auditing)_ 
* mupdf _(grosse,big,pdfs,schnell)_ , broot _(Dateimanager fuer Kommandozeile)_ 
* devilspie2 _(manipuliert autom. Fenster unter Linux - Position und Groesse festlegen)_ , pywal _(Linux Terminals passend einfaerben)_  
* TOOL_XY _(Beschreibung Beschreibung Beschreibung)_ , TOOL_XY _(Beschreibung Beschreibung Beschreibung)_


### netztools network tools,packages,pakete,installieren,install 


* iptraf _(Interaktiver farbiger LAN Monitor)_  ethstatus _(console-based ethernet statistics monitor)_ ifstat _(InterFace STATistics Monitoring)_ 
* iftop _(Anzeige der genutzten Bandbreite einer Netzwerkschnittstelle)_ nethogs _(Net top tool grouping bandwidth per process)_ 
   nload _(realtime console network usage monitor)_ 
* ntop _(display network usage in web browser)_ darkstat _(network traffic analyzer)_ 


### systemd 


**systemd** Dienst **stop und disable** am Beispiel teamviewer:


```bash

ok8cp5@okcp-Lati-E6330:~$ sudo teamviewer daemon stop
systemctl stop teamviewerd.service

ok8cp5@okcp-Lati-E6330:~$ sudo systemctl stop teamviewerd.service
ok8cp5@okcp-Lati-E6330:~$ sudo teamviewer daemon disable
Sa 15. Dez 12:19:27 CET 2018
Action: Removing ...
systemctl stop teamviewerd.service
Removed symlink /etc/systemd/system/multi-user.target.wants/teamviewerd.service.

```


### Linux-User Easy-Linux 


**LU**


Lu.2011.06 ImageMagick, Magick Scripting Language _(MSL)_ | Lu.2011.09 apache mod_security   
Lu.2011.10 transcoder | Lu.2011.11 arkose _(sandbox)_   
Lu.2011.12 kiwix, ssvnc, Tunnel-Android-pc dupeguru, CLI-Tools:readline,vi-modus-bash...ffox... | Lu.2012.01 mixxx ImageMagick   
Lu.2012.04 Xen | Lu.2012.05 Patent-Falle, ssh-Tunnel, Vim Touch, Hacker’s Keyboard | Lu.2012.06 cURL | Lu.2012.07 pgrep   
Lu.2012.08 HTML5, ImageMagick   
Lu-2012-09 LaTeX-Klasse Moderncv, firewalld _(Fedora Firewall)_   
Lu-2012-10 Powertop, CPAN _(Perl)_   
Lu-2012-11 Rpmorphan,Rpmrestore _(Pakete aufraeumen)_   
Lu-2012-12 PDF Ebenen bearbeiten | Lu-2013-01 IPTV, Grive _(Client f. Google Drive)_ , top,atop,htop,sntop,dnstop   
Lu-2013-02 iftop, glogg _(Log Dateien)_ | Lu-2013-03 Filemonitor _(lsof)_ , phpvirtualbox   
Lu-2013-04 any-dl _(Download aus Mediatheken)_ , Diodon _(Zwischenablage)_ , Apt-get und  Aptitude _(Teil 1)_   
Lu-2013-05 shelr _(Screencasts von Terminal)_ , Audio-Codec Opus   
Lu-2013-06 dosage _(Comic download)_ , kshutdown, Lucidor _(epub)_ , ImageMagick _(import)_ , AeroFS   
Lu-2013-07 Debian 7 Wheezy , NST _(Network Security Toolkit)_ , Editor Tilde   
Lu-2013-10 chrony _(ntp)_ bashstyle-ng _(Konf-Tool Bash)_ downtimed   
Lu-2013-11 cvechecker _(Sicherheitsluecken check)_ lnav _(Log Tool)_ Raspberry_Pi _(Qemu)_ | Lu-2013-12 Wifislax _(WLan-Check-Distri)_   
Lu-2014-01 DVB LaTeX _(bunt,color)_   
Lu-2014-02 Droopy _(Netz-Copy)_ Monitorix AppArmor Youtube-Videos LAN-Monitoring _(Netz-Tools:Vnstat,Ntop,Darkstat)_   
Lu-2014-03 Rpmerizor _(RPMs bauen)_ Giada _(Musik,Loops)_ | Lu-2014-04 Cryptcat _(wie netcat)_ USB-Multiboot Tripwire Socat _(Relay-Tool)_   
Lu-2014-05 Linkchecker Owncloud PAC netrw _(netread,netwrite)_ | Lu-2014-06 fwknop _(ssh anklopfen)_ BitwigStudio _(Audio-Workstation)_   
Lu-2014-07 Wifi Guard _(wlan check)_ Pipe Viewer _(sehen ob Datenfluss in Pipe stockt)_  Rlwrap _(History samt Suche sowie Autovervollständigung)_    
Lu-2015-10 Systemd und SysVinit | Lu-2016-05 ssdeep _(recursive piecewise hashing tool, aehnliche Dateien suchen/finden)_       



**EL**


El-2011-03 Hugin: Perfekte Panoramabilder erstellen | EL-2012-01 KDE-Tipps | EL-2012-04 Gnome-Tipps   
EL-2013-01 OCR-Prog:Tesseract,Cuneiform   
EL-2013-02 VBox Win8  LibreOffice-Tipps  Gimp  GPT _(Platten Partitionstabellen)_   
EL-2013-03 Dillo _(Browser)_ DVDstyler QjackCtl KDE-Tipps Gimp DigiKam   
EL-2013-04 goosh.org _(google shell)_ explainshell.com KDE-Tipps | EL-2014-01 Gimp TV-Browser KDE-Tipps   
EL-2014-02 EasyTAG LibreOffice _(Normbrief-Vorlagen)_ Dateisysteme | EL-2014-03 mp3 und ogg taggen   
EL-2015-01  Gimp _(Anwendertipps)_ | EL-2016-01 Sigil _(WYSIWYG E-Book Editor)_ Calibre _(E-Book Verwaltung)_     


### ct


**ct.Jahr.Ausgabe (Seite) Thema** | (**P**):PDF in Bigaex | (**F**): Foto in Bigaex   

* ct.2018.02 :  (72) Personenwaage mit ESP32 und OLED Bauanleitung (**F**)
* ct.2013.10 :  (146) Linux UEFI Secure Boot , (148) Android Launcher   
* ct.2018.15 :  (72) Windows absichern 
* ct.2018.21 :  (80) Fritzbox Monitoring mit Munin , (122) Linux fuer alte Rechner, alte Hardware HW , (138) Android Apps mit Texterkennung, Text Fairy , (158) Tipps zum Arbeiten mit GitHub, GitHub Gist, Git Erweiterung LFS 
* ct.2019.01 :  (87) GSConnect , Linux mit Android verbinden 
* ct.2019.14 :  (142) Netzwerkmitschnitte mit tshark geschickter analysieren 
* ct.2019.18 :  (64) userinyerface.com , (148) Windows Leistungsfresser finden und HW-Flaschenhaelse suchen mit Taskmanager, Windows Internet Engpaesse , (156) Docker, Container Orchestrator Kubernetes 
* ct.2019.26 :  (152) Linux-Tool OCRmyPDF macht aus eingescannten Schriftstücken durchsuchbare PDFDokumente 
* ct.2020.05 :  (97) broot (Dateimanager fuer Kommandozeile) , (166) topgrade (Aktualisiert mehrere Quellen) 
* ct.2020.10 :  (16) Familien Backup PC mit Sync (Resilio Sync) , (76) Mobil-App LateBack (Bahnfahrern,Zug,Verspätung, Papierkram,Fahrtkostenerstattung) , (124) Mobilfunk-Notruf 110 112 Notfall Standort Dienst , (136) USB-C Anschluss Raspberry Pi 4 , (142) Android Apps Firewall 


### Firefox Chrome add-ons plugins


Firefox add ons plugins: classic compact, gTranslate, Evernote _(Clearly,Web Clipper)_ , Stealthy _(Geblockte YouTube-Videos)_ , 
imacro _(Klicks u. Eingaben automatisieren)_ , 


---


## Neues Linux System

### Ubuntu


* Aufpassen beim Setup bei der **Verschluesselung, Partition oder HOME**, beides macht keinen Sinn !
* Firefox:  **``browser.sessionstore.interval = 300000 , browser.cache.disk.enable to false``**
* Chrome: **``ok8cp5@E6330:~$ sudo grep -i exec /usr/share/applications/google-chrome.desktop``**  #  (Unity Starter)    
   ```bash
   Exec=/usr/bin/google-chrome-stable --disk-cache-dir=/dev/shm/ --disk-cache-size=14000000 %U
   Exec=/usr/bin/google-chrome-stable --disk-cache-dir=/dev/shm/ --disk-cache-size=14000000 
   Exec=/usr/bin/google-chrome-stable --disk-cache-dir=/dev/shm/ --disk-cache-size=14000000 --incognito
   ```
* abcdefg   
* abcdefg   
* abcdefg   


```bash


sudo apt install ssh parcellite autokey-gtk unison-gtk colordiff meld pdftk rpl dwdiff inxi keepassx gxmessage gnome-tweak-tool 
sudo apt install krusader kate plasma-workspace encfs kdiff3 unity-tweak-tool gnome-tweak-tool vim


sudo dpkg -i dropbox_2015.10.28_amd64.deb
sudo apt install -f


cp -v .bashrc{,.ori}
ok8cp5@Opti7010:~$ sdiff .bashrc .bashrc.ori |egrep '<'
HISTCONTROL=erasedups:ignoredups                              <
export HISTCONTROL                                            <
HISTSIZE=9944                                                 <
HISTFILESIZE=14944                                            <
HISTTIMEFORMAT='%F %T '                                       <
# aexx                                                        <
#PS1="\[\033[32m\]\j \u@\h\[\033[37m\]:\w/ \D{%Y-%m-%d} \t \n <
ok8cp5@Opti7010:~$


```


Bei Sync (unison) evtl.  **”excluden”**  (aus md5_bigaex_DIFF)   


    ./.gd/credentials.json 5e57dd2dcf5b506db39a0a37db34caf3
    ./.gd/drivedb 77fe7072b2d42793868afd1191e36d74
    ./Dropbox/Public/.dropbox 7b391a78c4bc82205be8686f6fcbaa2f


Test  →   ⇒  Pfeile :-) 


---
## Android
### android-sdk emulator:


    /aexdisk/iso-tmp/android/android-sdk-linux_x86/tools/emulator -avd galaxe -no-boot-anim -scale 0.55 -memory 256
    
    cp ../android-sdk-linux_x86/platforms/android-8/images/system.img avd/galaxe-markt.avd/
    RESTART  # ./tools/emulator -avd galaxe-markt -no-boot-anim -scale 0.7 -shell -memory 512 -partition-size 96
    adb shell  #  mount -o remount rw /system [adb remount]  #  rm /system/app/SdkSetup.apk  
    ./android-sdk-linux_x86/platform-tools/adb push  [Vending.apk / GoogleServicesFramework.apk] /system/app/
    
    multisystem: dd if=/dev/zero of=/media/PLATINUM/android2/data.img bs=1M count=999



**Android trotz MTP Mode als USB Device / Geraet anschliessen _(ungetestet)_**  


Just wanted to share some tips to those who wanted to re-enable the **Mass Storage Mode on their Android 4.2.2**  
1. Connect your phone to a computer _(The device will be connected in MTP mode as default)_  
2. Reboot your phone while connected to the computer  
3. Wait until you see the USB icon on your Notification Bar  
4. You will *now* have an option __to__ select Mass Storage henceforth  


### android apps


save my attach , prismads , Bandicoot , galaxy on fire , AngryBackup _(91308670576 id)_ , busuu _(sprachen)_ , 
komoot  _(Outdoor Fahrrad Routenplaner)_ , airdroid , webkey , Hacker’s Keyboard , Vim Touch ,  
FreeOffice Mobile _(SoftMaker, gut bei heise)_ , AppExtract, Internet Security Light _(G Data)_ ,  
Python-Skript adb-sync _(auf GitHub, Sync zu PC aehnlich rsync)_ , t-ui Linux-CLI-Launcher ,   


###### Ende       

