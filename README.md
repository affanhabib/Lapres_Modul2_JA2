
# Laporan Resmi Praktikum Modul 2

Soal Shift Modul 2 dapat dilihat [disini](Soal/Soal%20Shift%20Modul%202.pdf). Dalam laporan ini, kami ingin menjelaskan langkah-langkah yang kami gunakan untuk mengerjakan soal shift tersebut.

1. Langkah pertama kami menjalankan UML seperti pada [modul](https://github.com/afrchmdi/Jarkom-Modul-Pengenalan-UML).
2. Kemudian, masih mengikuti modul, membuat topologi sesuai permintaan soal. `nano topologi.sh`
![topologi](Gambar/Topologi.png)

```shell
# Switch
uml_switch -unix switch0 > /dev/null < /dev/null &
uml_switch -unix switch1 > /dev/null < /dev/null &

#Router
xterm -T PIKACHU -e linux ubd0=PIKACHU,jarkom umid=PIKACHU eth0=tuntap,,,10.151.72.17 eth1=daemon,,, switch1 eth2=daemon,,, switch0 mem=96M &

#DNS + Web Server
xterm -T ARTICUNO -e linux ubd0=ARTICUNO,jarkom umid=ARTICUNO eth0=daemon,,,switch1 mem=128M &
xterm -T MEWTWO -e linux ubd0=MEWTWO,jarkom umid=MEWTWO eth0=daemon,,,switch1 mem=128M &
xterm -T MOLTRES -e linux ubd0=MOLTRES,jarkom umid=MOLTRES eth0=daemon,,,switch1 mem=128M &

#Klien
xterm -T PSYDUCK -e linux ubd0=PSYDUCK,jarkom umid=PSYDUCK eth0=daemon,,,switch0 mem=96M &
xterm -T SNORLAX -e linux ubd0=SNORLAX,jarkom umid=SNOXLAX eth0=daemon,,,switch0 mem=96M &
```
lalu `bash topologi.sh`

3. Setelah login di masing-masing UML dan mengikuti langkah-langkah modul tersebut, setting IP pada tiap UML dengan mengetikkan `nano /etc/network/interfaces`. Setting IP seperti berikut

**PIKACHU (Sebagai Router)**
```
auto eth0
iface eth0 inet static
address 10.151.72.18
netmask 255.255.255.252
gateway 10.151.72.17

auto eth1
iface eth1 inet static
address 10.151.73.33
netmask 255.255.255.248

auto eth2
iface eth2 inet static
address 192.168.0.1
netmask 255.255.255.0
```

**ARTICUNO (Sebagai DNS Server)**
```
auto eth0
iface eth0 inet static
address 10.151.73.34
netmask 255.255.255.248
gateway 10.151.73.33
```

**MEWTWO (Sebagai Web Server)**
```
auto eth0
iface eth0 inet static
address 10.151.73.35
netmask 255.255.255.248
gateway 10.151.73.33
```

**MOLTRES (Sebagai DNS Slave)**
```
auto eth0
iface eth0 inet static
address 10.151.73.36
netmask 255.255.255.248
gateway 10.151.73.33
```

**PSYDUCK (Sebagai Klien)**
```
auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.255.0
gateway 192.168.0.1
```

**SNORLAX (Sebagai Klien)**
```
auto eth0
iface eth0 inet static
address 192.168.0.3
netmask 255.255.255.0
gateway 192.168.0.1
```
Restart network dengan `service networking restart` atau `/etc/init.d/networking restart` di setiap UML.

4. Kemudian lanjutkan sesuai dengan modul tersebut.
5.  