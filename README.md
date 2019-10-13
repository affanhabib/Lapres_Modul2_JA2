# Laporan Resmi Praktikum Modul 2

Soal Shift Modul 2 dapat dilihat [disini](Soal/Soal%20Shift%20Modul%202.pdf). Dalam laporan ini, kami ingin menjelaskan langkah-langkah yang kami gunakan untuk mengerjakan soal shift tersebut.

1. Langkah pertama kami menjalankan UML seperti pada [modul](https://github.com/afrchmdi/Jarkom-Modul-Pengenalan-UML).
2. Kemudian membuat topologi sesuai permintaan soal.

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

3. 
4.  