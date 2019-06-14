Zadanie 1
---------

![zadanie 1](zadanie-1.svg)

1. Zaprojektuj oraz przygotuj prototyp rozwiązania z wykorzystaniem oprogramowania ``VirtualBox`` lub podobnego. 
Zaproponuj rozwiązanie spełniające poniższe wymagania:
   * Usługodawca zapewnia domunikację z siecią internet poprzez interfejs ``eth0`` ``PC0``
   * Zapewnij komunikację z siecią internet na poziomie ``LAN1`` oraz ``LAN2``
   * Dokonaj takiego podziału sieci o adresie ``172.22.128.0/17`` aby w ``LAN1`` można było zaadresować ``500`` adresów natomiast w LAN2 ``5000`` adresów    
   * Przygotuj dokumentację powyższej architektury w formie graficznej w programie ``DIA``
   --------
 Rozwiązanie
 od providera 172.22.128.0/17
 adres sieci 172.22.128.0/17
 maska 255.255.128.0
 adres rozgłoszeniowy 172.22.255.255
 host min 172.22.128.1
 host max 172.22.255.254
 ile hostów? 32766

LAN1 500 hostów
maska /23 2^(32-23)-2 = 2^9 - 2 = 510 hostów
adres sieci 172.22.160.0/23
maska 255.255.254.0
adres rozgłoszeniowy 172.22.161.255
host min 172.22.160.1
host max 172.22.161.254
ile hostów? 510

LAN2 5000 hostów
maska /19 2^(32-19)-2 = 2^13 -2 = 8190 hostów
adres sieci 172.22.128.0/19
maska 255.255.224.0
adres rozgłoszeniowy 172.22.159.255
host min 172.22.128.1
host max 172.22.159.254
ile hostów? 8190

Komendy:

PC0:

ip addr flush enp0s3

ip addr add 172.22.160.1/23 dev enp0s3

ip addr add 172.22.128.1/19 dev enp0s8

echo 1 > /proc/sys/net/ipv4/ip_foward 

PC1:

ip addr flush enp0s3

ip addr add 172.22.160.10/23 dev enp0s3

ip route add default via 172.22.160.1

PC2:

ip addr flush enp0s3

ip addr add 172.22.128.10/19 dev enp0s3

ip route add default via 172.22.128.1

ping 172.22.160.10
