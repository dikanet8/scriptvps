#!/bin/bash
#
# Script Copyright www.yonatankanu.blogspot.co.id
# Mod by Yonatan Kanu as Thorn SSH
# ==================================================
# 

# initialisasi var
export DEBIAN_FRONTEND=noninteractive
OS=`uname -m`;
MYIP=$(wget -qO- ipv4.icanhazip.com);
MYIP2="s/xxxxxxxxx/$MYIP/g";

# go to root
cd

# disable ipv6
echo 1 > /proc/sys/net/ipv6/conf/all/disable_ipv6
sed -i '$ i\echo 1 > /proc/sys/net/ipv6/conf/all/disable_ipv6' /etc/rc.local

# install wget and curl
apt-get update;apt-get -y install wget curl;

# set time GMT +7
ln -fs /usr/share/zoneinfo/Asia/Jakarta /etc/localtime

# set locale
sed -i 's/AcceptEnv/#AcceptEnv/g' /etc/ssh/sshd_config
service ssh restart

# set repo
wget -O /etc/apt/sources.list "https://raw.githubusercontent.com/rizal180499/Auto-Installer-VPS/master/conf/sources.list.debian7"
wget "http://www.dotdeb.org/dotdeb.gpg"
cat dotdeb.gpg | apt-key add -;rm dotdeb.gpg


# update
apt-get update

# install webserver
apt-get -y install nginx

# install essential package
apt-get -y install bmon iftop htop nmap axel nano iptables traceroute sysv-rc-conf dnsutils bc nethogs openvpn vnstat less screen psmisc apt-file whois ptunnel ngrep mtr git zsh mrtg snmp snmpd snmp-mibs-downloader unzip unrar rsyslog debsums rkhunter
apt-get -y install build-essential

# disable exim
service exim4 stop
sysv-rc-conf exim4 off

# update apt-file
apt-file update

# setting vnstat
vnstat -u -i venet0
service vnstat restart

# install screenfetch
cd

#touch screenfetch-dev
cd
wget https://github.com/KittyKatt/screenFetch/archive/master.zip
apt-get install -y unzip
unzip master.zip
mv screenFetch-master/screenfetch-dev /usr/bin
cd /usr/bin
mv screenfetch-dev screenfetch
chmod +x /usr/bin/screenfetch
chmod 755 screenfetch
cd
echo "clear" >> .bash_profile
echo "screenfetch" >> .bash_profile
#wget -O screenfetch-dev "https://raw.githubusercontent.com/rizal180499/Auto-Installer-VPS/master/conf/screenfetch-dev"
#mv screenfetch-dev /usr/bin/screenfetch
#chmod +x /usr/bin/screenfetch
#echo "clear" >> .profile
#echo "screenfetch" >> .profile

# install webserver
cd
rm /etc/nginx/sites-enabled/default
rm /etc/nginx/sites-available/default
wget -O /etc/nginx/nginx.conf "https://raw.githubusercontent.com/yonatankanu/kanu/master/nginx.conf"
mkdir -p /home/vps/public_html
echo "<pre>Setup by Yonatan Kanu | WA : 085707136028</pre>" > /home/vps/public_html/index.html
wget -O /etc/nginx/conf.d/vps.conf "https://raw.githubusercontent.com/yonatankanu/kanu/master/vps.conf"
service nginx restart

# Konfigurasi Banner SSH
cd /etc/thornssh
<font color="blue"><b>==================================================<br></b></font>
<font color="red"><b>SELAMAT DATANG<br>
TERIMA KASIH TELAH MEMBELI SSH DARI KAMI</b></font>
<font color="blue"><b>==================================================<br>
BACA BAIK BAIK PERATURAN DI BAWAH INI:<br>
- NO MULTY LOGIN<br>
- DILARANG DDOS<br>
- DILARANG BERMAIN GAME PLAYSTATION<br>
- DILARANG CARDING/HACKING<br>
- DILARANG DOWNLOAD TORRENT FILE<br>
- DILARANG SPAM<br>
==================================================<br>
PELANGGARAN TERSEBUT AKAN MEMBUAT AKUN ANDA DIHAPUS PERMANEN<br>
==================================================<br>
TERIMA KASIH............!!!!!<br>
==================================================</b></font>
<font color="red"><b>SUPPORTED BY THORN SSH</font>
<font color="blue"><b>==================================================<br>

cd
# install openvpn
wget -O /etc/openvpn/openvpn.tar "https://raw.github.com/arieonline/autoscript/master/conf/openvpn-debian.tar"
cd /etc/openvpn/
tar xf openvpn.tar
wget -O /etc/openvpn/1194.conf "https://raw.githubusercontent.com/rizal180499/Auto-Installer-VPS/master/conf/1194.conf"
service openvpn restart
sysctl -w net.ipv4.ip_forward=1
sed -i 's/#net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/g' /etc/sysctl.conf
iptables -t nat -I POSTROUTING -s 192.168.100.0/24 -o eth0 -j MASQUERADE
iptables-save > /etc/iptables_yg_baru_dibikin.conf
wget -O /etc/network/if-up.d/iptables "https://raw.githubusercontent.com/nifira123/debian7_32bit/master/iptables"
chmod +x /etc/network/if-up.d/iptables
service openvpn restart

#konfigurasi openvpn
cd /etc/openvpn/
wget -O /etc/openvpn/client.ovpn "https://raw.githubusercontent.com/nifira123/debian7_32bit/master/client-1194.conf"
sed -i $MYIP2 /etc/openvpn/client.ovpn;
cp client.ovpn /home/vps/public_html/

cd
# install badvpn
wget -O /usr/bin/badvpn-udpgw "https://github.com/ForNesiaFreak/FNS/raw/master/sett/badvpn-udpgw"
if [ "$OS" == "x86_64" ]; then
  wget -O /usr/bin/badvpn-udpgw "https://github.com/ForNesiaFreak/FNS/raw/master/sett/badvpn-udpgw64"
fi
sed -i '$ i\screen -AmdS badvpn badvpn-udpgw --listen-addr 127.0.0.1:7300' /etc/rc.local
chmod +x /usr/bin/badvpn-udpgw
screen -AmdS badvpn badvpn-udpgw --listen-addr 127.0.0.1:7300

# install mrtg
wget -O /etc/snmp/snmpd.conf "https://raw.githubusercontent.com/rizal180499/Auto-Installer-VPS/master/conf/snmpd.conf"
wget -O /root/mrtg-mem.sh "https://raw.githubusercontent.com/rizal180499/Auto-Installer-VPS/master/conf/mrtg-mem.sh"
chmod +x /root/mrtg-mem.sh
cd /etc/snmp/
sed -i 's/TRAPDRUN=no/TRAPDRUN=yes/g' /etc/default/snmpd
service snmpd restart
snmpwalk -v 1 -c public localhost 1.3.6.1.4.1.2021.10.1.3.1
mkdir -p /home/vps/public_html/mrtg
cfgmaker --zero-speed 100000000 --global 'WorkDir: /home/vps/public_html/mrtg' --output /etc/mrtg.cfg public@localhost
curl "https://raw.githubusercontent.com/rizal180499/Auto-Installer-VPS/master/conf/mrtg.conf" >> /etc/mrtg.cfg
sed -i 's/WorkDir: \/var\/www\/mrtg/# WorkDir: \/var\/www\/mrtg/g' /etc/mrtg.cfg
sed -i 's/# Options\[_\]: growright, bits/Options\[_\]: growright/g' /etc/mrtg.cfg
indexmaker --output=/home/vps/public_html/mrtg/index.html /etc/mrtg.cfg
if [ -x /usr/bin/mrtg ] && [ -r /etc/mrtg.cfg ]; then mkdir -p /var/log/mrtg ; env LANG=C /usr/bin/mrtg /etc/mrtg.cfg 2>&1 | tee -a /var/log/mrtg/mrtg.log ; fi
if [ -x /usr/bin/mrtg ] && [ -r /etc/mrtg.cfg ]; then mkdir -p /var/log/mrtg ; env LANG=C /usr/bin/mrtg /etc/mrtg.cfg 2>&1 | tee -a /var/log/mrtg/mrtg.log ; fi
if [ -x /usr/bin/mrtg ] && [ -r /etc/mrtg.cfg ]; then mkdir -p /var/log/mrtg ; env LANG=C /usr/bin/mrtg /etc/mrtg.cfg 2>&1 | tee -a /var/log/mrtg/mrtg.log ; fi
cd

# setting port ssh
sed -i '/Port 22/a Port 143' /etc/ssh/sshd_config
sed -i 's/Port 22/Port  22/g' /etc/ssh/sshd_config
service ssh restart

# install dropbear
apt-get -y install dropbear
sed -i 's/NO_START=1/NO_START=0/g' /etc/default/dropbear
sed -i 's/DROPBEAR_PORT=22/DROPBEAR_PORT=443/g' /etc/default/dropbear
sed -i 's/DROPBEAR_EXTRA_ARGS=/DROPBEAR_EXTRA_ARGS="-p 80 -p 109 -p 110"/g' /etc/default/dropbear
sed -i 's/DROPBEAR_BANNER="etc/thornssh"/g' /etc/default/dropbear
echo "/bin/false" >> /etc/shells
echo "/usr/sbin/nologin" >> /etc/shells
service ssh restart
service dropbear restart

# install vnstat gui
cd /home/vps/public_html/
wget http://www.sqweek.com/sqweek/files/vnstat_php_frontend-1.5.1.tar.gz
tar xf vnstat_php_frontend-1.5.1.tar.gz
rm vnstat_php_frontend-1.5.1.tar.gz
mv vnstat_php_frontend-1.5.1 vnstat
cd vnstat
sed -i 's/eth0/venet0/g' config.php
sed -i "s/\$iface_list = array('venet0', 'sixxs');/\$iface_list = array('venet0');/g" config.php
sed -i "s/\$language = 'nl';/\$language = 'en';/g" config.php
sed -i 's/Internal/Internet/g' config.php
sed -i '/SixXS IPv6/d' config.php
cd

# install fail2ban
apt-get -y install fail2ban;service fail2ban restart

# Instal DDOS Flate
if [ -d '/usr/local/ddos' ]; then
	echo; echo; echo "Please un-install the previous version first"
	exit 0
else
	mkdir /usr/local/ddos
fi
clear
echo; echo 'Installing DOS-Deflate 0.6'; echo
echo; echo -n 'Downloading source files...'
wget -q -O /usr/local/ddos/ddos.conf http://www.inetbase.com/scripts/ddos/ddos.conf
echo -n '.'
wget -q -O /usr/local/ddos/LICENSE http://www.inetbase.com/scripts/ddos/LICENSE
echo -n '.'
wget -q -O /usr/local/ddos/ignore.ip.list http://www.inetbase.com/scripts/ddos/ignore.ip.list
echo -n '.'
wget -q -O /usr/local/ddos/ddos.sh http://www.inetbase.com/scripts/ddos/ddos.sh
chmod 0755 /usr/local/ddos/ddos.sh
cp -s /usr/local/ddos/ddos.sh /usr/local/sbin/ddos
echo '...done'
echo; echo -n 'Creating cron to run script every minute.....(Default setting)'
/usr/local/ddos/ddos.sh --cron > /dev/null 2>&1
echo '.....done'
echo; echo 'Installation has completed.'
echo 'Config file is at /usr/local/ddos/ddos.conf'
echo 'Please send in your comments and/or suggestions to zaf@vsnl.com'

# install squid3
apt-get -y install squid3
wget -O /etc/squid3/squid.conf "https://raw.githubusercontent.com/yonatankanu/debian7_32bit/master/squid3.conf"
sed -i $MYIP2 /etc/squid3/squid.conf;
service squid3 restart

# install webmin
cd
wget -O webmin-current.deb "http://www.webmin.com/download/deb/webmin-current.deb"
dpkg -i --force-all webmin-current.deb;
apt-get -y -f install;
rm /root/webmin-current.deb
service webmin restart

# download script
cd /usr/bin
wget -O menu "https://raw.githubusercontent.com/yonatankanu/debian7_32bit/master/menu.sh"
wget -O usernew "https://raw.githubusercontent.com/yonatankanu/debian7_32bit/master/usernew.sh"
wget -O trial "https://raw.githubusercontent.com/yonatankanu/debian7_32bit/master/trial.sh"
wget -O hapus "https://raw.githubusercontent.com/yonatankanu/debian7_32bit/master/hapus.sh"
wget -O login "https://raw.githubusercontent.com/yonatankanu/debian7_32bit/master/user-login.sh"
wget -O dropmon "https://raw.githubusercontent.com/yonatankanu/debian7_32bit/master/dropmon.sh"
wget -O user-expired "https://raw.githubusercontent.com/ForNesiaFreak/FNS_Debian7/fornesia.com/freak/user-expired.sh"
wget -O member "https://raw.githubusercontent.com/yonatankanu/debian7_32bit/master/user-list.sh"
wget -O restart "https://raw.githubusercontent.com/yonatankanu/debian7_32bit/master/resvis.sh"
wget -O speedtest "https://raw.githubusercontent.com/ForNesiaFreak/FNS_Debian7/fornesia.com/null/speedtest_cli.py"
wget -O bench-network "https://raw.githubusercontent.com/ForNesiaFreak/FNS_Debian7/fornesia.com/null/bench-network.sh"
wget -O ps-mem "https://raw.githubusercontent.com/ForNesiaFreak/FNS_Debian7/fornesia.com/null/ps_mem.py"
wget -O about "https://raw.githubusercontent.com/yonatankanu/debian7_32bit/master/about.sh"
echo "0 0 * * * root /usr/bin/reboot" > /etc/cron.d/reboot
echo "* * * * * service dropbear restart" > /etc/cron.d/dropbear
chmod +x menu
chmod +x usernew
chmod +x trial
chmod +x hapus
chmod +x login
chmod +x dropmon
chmod +x user-expired
chmod +x member
chmod +x restart
chmod +x speedtest
chmod +x bench-network
chmod +x ps-mem
chmod +x about

#Blockir Torrent
iptables -A OUTPUT -p tcp --dport 6881:6889 -j DROP
iptables -A OUTPUT -p udp --dport 1024:65534 -j DROP
iptables -A FORWARD -m string --string "get_peers" --algo bm -j DROP
iptables -A FORWARD -m string --string "announce_peer" --algo bm -j DROP
iptables -A FORWARD -m string --string "find_node" --algo bm -j DROP
iptables -A FORWARD -m string --algo bm --string "BitTorrent" -j DROP
iptables -A FORWARD -m string --algo bm --string "BitTorrent protocol" -j DROP
iptables -A FORWARD -m string --algo bm --string "peer_id=" -j DROP
iptables -A FORWARD -m string --algo bm --string ".torrent" -j DROP
iptables -A FORWARD -m string --algo bm --string "announce.php?passkey=" -j DROP
iptables -A FORWARD -m string --algo bm --string "torrent" -j DROP
iptables -A FORWARD -m string --algo bm --string "announce" -j DROP
iptables -A FORWARD -m string --algo bm --string "info_hash" -j DROP

# finishing
cd
chown -R www-data:www-data /home/vps/public_html
service nginx start
service php-fpm start
service vnstat restart
service openvpn restart
service snmpd restart
service cron restart
service ssh restart
service dropbear restart
service fail2ban restart
service squid3 restart
service webmin restart
rm -rf ~/.bash_history && history -c
echo "unset HISTFILE" >> /etc/profile

# info
clear
echo "Autoscript Include:" | tee log-install.txt
echo "===========================================" | tee -a log-install.txt
echo ""  | tee -a log-install.txt
echo "Service"  | tee -a log-install.txt
echo "-------"  | tee -a log-install.txt
echo "OpenSSH  : 22, 143"  | tee -a log-install.txt
echo "Dropbear : 443, 80"  | tee -a log-install.txt
echo "Squid3   : 8080, 3128 (limit to IP SSH)"  | tee -a log-install.txt
echo "OpenVPN  : TCP 1194 (client config : http://$MYIP:81/client.ovpn)"  | tee -a log-install.txt
echo "badvpn   : badvpn-udpgw port 7300"  | tee -a log-install.txt
echo "nginx    : 28"  | tee -a log-install.txt
echo ""  | tee -a log-install.txt
echo "Script"  | tee -a log-install.txt
echo "------"  | tee -a log-install.txt
echo "menu (Menampilkan daftar perintah yang tersedia)"  | tee -a log-install.txt
echo "usernew (Membuat Akun SSH)"  | tee -a log-install.txt
echo "trial (Membuat Akun Trial)"  | tee -a log-install.txt
echo "hapus (Menghapus Akun SSH)"  | tee -a log-install.txt
echo "login (Cek User Login)"  | tee -a log-install.tx
echo "user-expired (Auto Lock User Expire tiap jam 00:00)"  | tee -a log-install.txt
echo "member (Cek Member SSH)"  | tee -a log-install.txt
echo "restart (Restart Service dropbear, webmin, squid3, openvpn dan ssh)"  | tee -a log-install.txt
echo "reboot (Reboot VPS)"  | tee -a log-install.txt
echo "speedtest (Speedtest VPS)"  | tee -a log-install.txt
echo "bench-network (Cek Kualitas VPS)"  | tee -a log-install.txt
echo "ps-mem (Cek RAM)"  | tee -a log-install.txt
echo "about (Informasi tentang script auto install)"  | tee -a log-install.txt
echo ""  | tee -a log-install.txt
echo "Fitur lain"  | tee -a log-install.txt
echo "----------"  | tee -a log-install.txt
echo "Webmin   : http://$MYIP:10000/"  | tee -a log-install.txt
echo "vnstat   : http://$MYIP/vnstat/"  | tee -a log-install.txt
echo "MRTG     : http://$MYIP/mrtg/"  | tee -a log-install.txt
echo "Timezone : Asia/Jakarta (GMT +7)"  | tee -a log-install.txt
echo "Fail2Ban : [on]"  | tee -a log-install.txt
echo "IPv6     : [off]"  | tee -a log-install.txt
echo ""  | tee -a log-install.txt
echo "http://yonatankanu.blogspot.co.id atau http://yonatankanu.wordpress.com"  | tee -a log-install.txt
echo "Modified by Yonatan Kanu as THORN SSH"  | tee -a log-install.txt
echo ""  | tee -a log-install.txt
echo "Log Instalasi --> /root/log-install.txt"  | tee -a log-install.txt
echo ""  | tee -a log-install.txt
echo "VPS AUTO REBOOT TIAP 12 JAM"  | tee -a log-install.txt
echo ""  | tee -a log-install.txt
echo "==========================================="  | tee -a log-install.txt
cd
rm -f /root/debian7.sh
