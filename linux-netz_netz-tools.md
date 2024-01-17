_   


###### Textdatei NICHT bearbeiten | gdrive export readonly | Markdown http://markdown.de


##### Version 2019-02-11 










```bash
echo Markdown
echo Code
```






# Netz-Tools


## Daten-Transfer


### netcat


**Einzelne Datei/One file:**   
Zuerst auf **Ziel/Destination**-Host:  `# netcat -l -p 12344 > Compaq-615.C.ntfsclone.img.gz `   
Dann auf **Quelle/Source**-Host: `# netcat 192.168.174.10 12344 < Compaq-615.C.ntfsclone.img.gz `   


Windows ueber Netzwerk umziehen - **Linux-Live-System auf beiden PC** booten: Netz starten   
**Ziel**-PC: `netcat -l -p 9000 | dd of=/dev/hda1`    #Horcht auf Port 12344   
**Quell**-PC: `dd if=/dev/hda1 | netcat 192.168.0.11 12344 `    #Daten gehen rueber, KEINE Fortschrittsanzeige !!!!   
**Ziel**-PC: `install-mbr /dev/hda ` #Oder Windows-Reparatur mit Win-Inst-CD   


## ip


    ip addr add 192.168.11.44/25 dev eth0
    ip addr del 192.168.11.44 dev eth0
    ip route add default via 192.168.11.1 dev eth0
    ip route del default via 10.5.0.1 dev eth1
    ip neigh show 10.0.2.2


    ss -r  # Socket Show


## IPv6 inet6


    ping6 fe80::a00:27ff:fee1:7ef2%eth2 -c4












## usw






    iptables -vnL


    tcpdump -l -n -s 0 -X -v -i eth0 -w /DATEN/TCPDUMP.txt host 172.20.251.35


    unset http_proxy ftp_proxy no_proxy ; set|grep oxy


    read -p wakeonlan_aexbackpc && wakeonlan 00:30:48:80:C8:64  # wake on lan wol


    rdesktop -u aleschil -a 15 [-f/-g 90%] 172.27.xx.yyy &  # TS # zurueck/back fullscreen [Ctrl + Alt + Enter]
    rdesktop -a 16 -g 90% backuppc  # Bestes Ergebnis # Verbindung zu mrw backuppc => xrdp


    grep "http" /home/aleschil/aex/Aex/Adr/xmarks/Bookmarks.html.2013-05-08.txt |awk -F"<" '{print $2}'|awk -F">" '{print $1}' |wc  # url bookmark
    grep "http" /home/aleschil/aex/Aex/Adr/xmarks/Bookmarks.html.2013-05-08.txt |awk -F"<" '{print $2}'|awk -F">" '{print $1}' |grep -v "\/\/[0-9][0-9][0-9]\."|grep -v \/localhost  |while read a; do sleep 3; echo -e "\n\n__________________ $a     ________________________________________" ; w3m -dump $a|head -4 |grep -i erro ; done




``` bash


iperf -s  # auf einem system als server  ⇒  iperf -c 192.168.0.14  # mit anderem sys zu server verbinden    


```




## nmap


    nmap -p 80 192.168.71.0/25  #  nmap -sS backup2  #  nmap -sS localhost
    for i in `seq 240 254`;do echo -e "\n...::: sudo nmap 192.168.71.${i} :::...";sudo nmap 192.168.71.${i}|egrep -C 444 open --color=always;done
    sudo nmap -PR 192.168.111.0/24 -sn  ##Netz scan




















###### Ende       


_
