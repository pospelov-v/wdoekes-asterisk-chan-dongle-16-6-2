# wdoekes-asterisk-chan-dongle-16-6-2

Готовый собраный мною модуль chan-dongle для asterisk16 с репозитория https://github.com/wdoekes/asterisk-chan-dongle

Сборка производилась вот так:
<pre>
rm /usr/lib64/asterisk/modules/chan_dongle.so
mkdir -p /root/wdoekes-asterisk-chan-dongle/
cd /root/wdoekes-asterisk-chan-dongle/
yum install epel-release -y
yum install dnf -y
dnf install epel-release
dnf groupinstall "Development Tools"
yum install git -y
yum install sqlite sqlite-devel -y
yum install asterisk16-devel -y

git clone https://github.com/wdoekes/asterisk-chan-dongle.git
cd asterisk-chan-dongle
./bootstrap
./configure --with-astversion=16.6.2 # Заменить на свою версию астериск
make
make install
</pre>


Установка:
<pre>
nano /etc/udev/rules.d/92-dongle.rules
KERNEL=="ttyUSB*", MODE="0666", OWNER="asterisk", GROUP="dialout"

yum install git -y
git clone https://github.com/pospelov-v/wdoekes-asterisk-chan-dongle-16-6-2
cd wdoekes-asterisk-chan-dongle-16-6-2/
cp -n etc/dongle.conf /etc/asterisk/dongle.conf
chown asterisk:asterisk /etc/asterisk/dongle.conf
chmod u=rwX,g=rX,o= /etc/asterisk/dongle.conf

cp -n chan_dongle.so /usr/lib64/asterisk/modules/chan_dongle.so

shutdown -r now
</pre>
