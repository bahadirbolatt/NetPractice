# NetPractice
Bu proje sistem yönetimi ile ilgili bir tür alıştırmadır.
====================

<div id="top"></div>

## İçerik
- [Bilinmesi Gerekenler](#bilinmesi-gerekenler)
  - [TCP](#tcp-taşıma-katmanı)
  - [IP address](#ip-address-network-layer)
  - [Subnet mask](#subnet-mask)
  - [Switch](#switch)
  - [Router](#router)
- [Seviyeler](#seviyeler)

## Bilinmesi Gerekenler

### TCP: Taşıma Katmanı

TCP, **Transmission Control Protocol (İletim Kontrol Protokolü)**'nün kısaltmasıdır. Uygulama programlarının ve cihazların bir ağ üzerinden mesaj alışverişi yapmasına olanak sağlayan bir iletişim standardıdır. İnternet üzerinden paket göndermek için kullanılır.

TCP, bir ağ üzerinden iletilmekte olan verilerin bütünlüğünü garanti eder. Verileri iletmeden önce TCP, kaynak ile hedef arasında iletişim başlayana kadar aktif kalan bir bağlantı kurar. Ardından, herhangi bir veri kaybı olmadan uçtan uca teslimatı sağlarken, büyük miktarda veriyi daha küçük paketlere böler.

<div align="right">
  <b><a href="#top">↥ başa dön</a></b>
</div>
</br>

---

### IP Address: Network Layer

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/ip1.png?raw=true" height=250 alt="mask"></kbd>
</p>
</br>

IP, iletim kontrol protokolünü de içeren bir internet protokol paketinin parçasıdır. Birlikte, bu ikisi TCP/IP olarak bilinir. İnternet protokol paketi, ağlar üzerinden veri paketleme, adresleme, iletme, yönlendirme ve alma kurallarını yönetir..

IP adresleme, bir ağdaki cihazlara adres atamanın mantıksal bir yoludur. İnternete bağlı her cihaz benzersiz bir IP adresi gerektirir.

Bir IP adresi iki kısımdan oluşur; bir parça, bilgisayar veya başka bir cihaz gibi ana bilgisayarı tanımlar ve diğer bölüm, ait olduğu ağı tanımlar. TCP/IP bunları ayırmak için [subnet mask](#subnet-mask) kullanır.
</br>
</br>

#### Public Adres vs. Private Adres

Genel IP adresi, doğrudan internet üzerinden erişilebilen ve internet servis sağlayıcınız (ISP) tarafından ağ yönlendiricinize atanan bir IP adresidir. Genel (veya harici) bir IP adresi, internete ağınızın içinden ağınızın dışına bağlanmanıza yardımcı olur.

Özel bir IP adresi, ağ yönlendiricinizin cihazınıza atadığı bir adrestir. Aynı ağ içindeki her cihaza benzersiz bir özel IP adresi atanır (bazen özel ağ adresi olarak adlandırılır) — bu, aynı dahili ağdaki cihazların birbirleriyle bu şekilde konuşmasıdır.

Bir ağ internete bağlandığında, ayrılmış özel IP adreslerinden bir IP adresi kullanamaz. Aşağıdaki aralıklar özel IP adresleri için ayrılmıştır:
```
192.168.0.0 – 192.168.255.255 (65,536 IP addresleri)
172.16.0.0 – 172.31.255.255   (1,048,576 IP addresleri)
10.0.0.0 – 10.255.255.255     (16,777,216 IP addresleri)
```

<div align="right">
  <b><a href="#top">↥ başa dön</a></b>
</div>
</br>

---

### Subnet Mask

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/mask1.png?raw=true" height=250 alt="mask"></kbd>
</p>
</br>

Alt ağ maskesi (subnet mask), IP adresindeki bir ağ adresi ile bir ana bilgisayar adresini birbirinden ayırmak için kullanılan 32 bitlik (4 bayt) bir adrestir. Bir ağ veya alt ağ içinde kullanılabilecek IP adresleri aralığını tanımlar.
</br>
</br>

#### Network Adresini Bulmak

Yukarıdaki *Interface A1* şu özelliklere sahiptir:
```
IP adres | 104.198.241.125
Mask       | 255.255.255.128  
```

IP adresinin hangi kısmının ağ adresi olduğunu belirlemek için, maskeyi IP adresine uygulamamız gerekir. Önce maskeyi ikili biçimine dönüştürelim:
```
Mask | 11111111.11111111.11111111.10000000
```

Bir maskenin 1 olan bitleri ağ adresini temsil ederken, bir maskenin 0 olan kalan bitleri ana bilgisayar adresini temsil eder. Şimdi IP adresini ikili biçimine çevirelim:
```
IP address | 01101000.11000110.11110001.01111101
Mask       | 11111111.11111111.11111111.10000000
```

Artık IP'nin ağ adresini bulmak için maskeyi IP adresine [bitwise AND](https://en.wikipedia.org/wiki/Bitwise_operation#AND) yoluyla uygulayabiliriz:
```
Network address | 01101000.11000110.11110001.00000000
```

Bu da ``104.198.241.0`` ağ adresine karşılık gelir.
</br>
</br>

#### Host adresleri aralığını bulma

Ağımızda hangi ana bilgisayar adreslerini kullanabileceğimizi belirlemek için IP adresimizin ana bilgisayar adresine ayrılmış bitlerini kullanmamız gerekir. Önceki IP adresimizi ve maskemizi kullanalım:
```
IP address | 01101000.11000110.11110001.01111101
Mask       | 11111111.11111111.11111111.10000000
```

Host adreslerimizin olası aralığı, maskenin tümü 0 olan son 7 biti ile ifade edilir. Bu nedenle, host adreslerinin aralığı şöyledir:
```
BINARY  | 0000000 - 1111111
DECIMAL | 0 - 127
```

Ağımız için olası IP adresleri aralığını elde etmek için, ana bilgisayar adresleri aralığını ağ adresine ekleriz. Olası IP adresleri aralığımız ``104.198.241.0 - 104.198.241.127`` olur.

<ins>ANCAK </ins>, aralığın uç kısımları özel kullanımlar için ayrılmıştır ve bir arayüze verilemez:
104.198.241.0   | Reserved to represent the network address.
104.198.241.127 | Reserved as the broadcast address; used to send packets to all hosts of a network.
```

Therefore, our real IP range becomes ``104.198.241.1 - 104.198.241.126``, which could have been found using an [IP calculator](https://www.calculator.net/ip-subnet-calculator.html).
</br>
</br>

#### CIDR Notation (/24)

The mask can also be represented with the Classless Inter-Domain Routing (CIDR). This form represents the mask as a slash "/", followed by the number of bits that serve as the network address.

Therefore, the mask in the example above of ``255.255.255.128``, is equivalent to a mask of ``/25`` using the CIDR notation, since 25 bits out of 32 bits represent the network address.


<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

---

### Switch

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/switch1.png?raw=true" height=150 alt="switch"></kbd>
</p>
</br>

A switch connects multiple devices together in a single network. Unlike a router, the switch does not have any interfaces since it only distributes packets to its local network, and cannot talk directly to a network outside of its own.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

---

### Router

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/route1.png?raw=true" height=200 alt="router"></kbd>
</p>
</br>

Just as the switch connects multiple devices on a single network, the router connects multiple networks together. The router has an interface for each network it connects to.

Since the router separates different networks, the range of possible IP addresses on one of its interfaces must not overlap with the range of its other interfaces. An overlap in the IP address range would imply that the interfaces are on the same network.
</br>
</br>

#### Routing Table

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/routing_table1.png?raw=true" height=150 alt="routing_table"></kbd>
</p>
</br>

A routing table is a data table stored in a router or a network host that lists the routes to particular network destinations. In NetPractice, the routing table consists of 2 elements:

- **Destination**: The destination specifies a network address on which a host is the end target of the packets. The route of ``default`` or ``0.0.0.0/0``, is the route that takes effect when no other route is available for an IP destination address. The default route will use the next-hop address to send the packets on their way without giving a specific destination. The default route will match any network.

- **Next hop**: The next hop refers to the next closest router a packet can go through. It is the IP address of the next router on the packet's way. Every single router maintains its routing table with a next hop address.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

## Seviyeler
<details>
  <summary>Level 1</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level1_paint.png?raw=true" alt="level1">  
  <br>
  <br>


**1.** Since *Client A* and *Client B* are on the same network, their IP address must represent the same network in accordance with the subnet mask.
<br>
The subnet mask is *255.255.255.0*, which means that the first 3 bytes of the IP address represent the network, and the 4th byte represents the host. Since we are on the same network, only the host can change. 
<br>
The solution will be anything in the range of **104.96.23.0 - 104.96.23.255** excluding the following 3:
* **104.96.23.0:** The first number in the range of hosts (0 in this case) represents the network and cannot be used by a host.
* **104.96.23.255:** The last number in the range of hosts (255 in this case) represents the broadcast address.
* **104.96.23.12:** This address is already used by the host *Client B*.

**2.** The same reasoning as *1.*, however the subnet mask is *255.255.0.0* in this case. The first 2 bytes of the IP address will represent the network; and the last 2 bytes, the host address.
<br>
The solution will be anything in the range of **211.191.0.0 - 211.191.255.255**, excluding:
* **211.191.0.0:** Represents the network address.
* **211.191.255.255:** Represents the broadcast address.
* **211.191.89.75:** Already taken by host *Client C*.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 2</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level2_paint.png?raw=true" alt="level2">
  <br>
  <br>

**1.** Since *Client B* is on the same private network as *Client A*, they should have the exact same subnet mask.
<br>
The solution can only be **255.255.255.224**.

**2.** To understand the subnet mask of *255.255.255.224*, let's look at it in binary form, along with the IP *192.168.20.222* of *Client B*:

<center>

```
MASK: 11111111.11111111.11111111.11100000
IP:   11000000.10101000.00010100.11011101
```
</center>
As we can see, the first 27 bits represent the IP address, while only the last 5 bits represent the host address.
<br>
All these 27 bits representing the network must stay the same in the IP addresses of hosts on the same network. To get the answer, we can only change the last 5 bits.
<br>
<br>
The answer is in the range of:

```
BIN:  11000000.10101000.00010100.11000000 - 11000000.10101000.00010100.11011111
or
DEC:  192.168.20.192 - 192.168.20.223
```
Excluding:
<br>
* **11000000.10101000.00010100.11000000:** Represents the network address (notice all 0 in the last 5 bits).
* **11000000.10101000.00010100.11011111:** Represents the broadcast address (notice all 1 in the last 5 bits).
* **11000000.10101000.00010100.11011110:** *Client B* already has that address.

**3.** Here we are introduced the slash "/" notation for the subnet mask on *Interface D1*. A subnet mask of */30* means that the first 30 bits of the IP address represent the network address, and the remaining 2 bits represent the host address:
<center>

```
Mask /30: 11111111.11111111.11111111.11111100
```
</center>

We can see that this binary number corresponds to the decimal *255.255.255.252*, therefore it is identical to the mask found on *Interface C1*.
<br>
<br>
The answers can then be any address, as long as they meet the following conditions:
* The network address (first 30 bits) must be identical for *Client D* and *Client C*.
* The host bits (last 2 bits) cannot be all 1, nor all 0.
* *Client D* and *Client C* do not have identical IP addresses.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 3</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level3_paint.png?raw=true" alt="level3">
  <br>
  <br>

  This exercise introduces the use of the **switch** (*Switch S* in this example). The switch links multiple hosts of the same network together.
  <br>
  <br>

  **1.** *Client A*, *Client B*, and *Client C* are all on the same network. Therefore, they must all have the same subnet mask. Since *Client C* already has the mask *255.255.255.128*, the mask for *Interface B1* and for *Interface A1* will also be *255.255.255.128* (or in slash notation: */25*).
  <br>
  <br>
  The IP address of *Interface B1* and *Interface C1* must be on the same network range as the IP of *Client A*. This range is:
  <center>

  ```
  104.198.241.0 - 104.198.241.128 
  ```
  </center>
  Excluding of course the network address and the broadcast address.

  <div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 4</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level4_paint.png?raw=true" alt="level4">
  <br>
  <br>

  This exercise introduces the **router**. The router is used to link multiple networks together. It does so with the use of multiple interfaces (*Interface R1*, *Interface R2*, and *Interface R3* in this example).
  <br>
  <br>

  **1.** Since none of the masks on *Interface B1*, *Interface A1*, and *Interface R1* are entered, we are free to choose our own subnet mask. A mask of **/24** is ideal as it leaves us with the entire 4th byte for the host address, and does not require binary calculations to find the range of possible host addresses.
  <br>
  <br>
  The IP address of *Interface B1* and *Interface R1* must have the same network address as the IP address of *Interface A1*. With a subnet of */24*, the possible range is:
  <center>

  ```
  85.17.5.0 - 85.17.5.255
  ```
  </center>
  Excluding the network address and the broadcast address.
  <br>
  <br>

  Note that we did not interact with the router *Interface R2* and *Interface R3*, since none of our communications had to reach these sides of the router.

  <div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 5</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level5_paint.png?raw=true" alt="level5">
  <br>
  <br>

  This level introduces **routes**. A route contains 2 fields, the first one is the **destination** of outbound packets, the second one is the **next hop** of the packets.
  <br>

  The **destination** *default* is equivalent to *0.0.0.0/0*, which will send the packets indiscriminately to the first network address it encounters. A destination address of *122.3.5.3/24* would send the packets to the network *122.3.5.0*.

  <br>
  The **next hop** is the IP address of the next  router (or internet) interface to which the interface of the current machine must send its packets. 
  <br>
  <br>

  **1.** *Client A* only has 1 route through which it can send its packets. There is no use specifying a numbered destination. The destination *default* will send the packets to the only path available.
  <br>
  <br>
  The next hop address must be the IP address of the next router's interface on the packets' way. The next interface is *Interface R1*, with the IP address of *54.117.30.126*. Note that the next interface is not *Interface A1*, since this is the sender's own interface.

  <div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 6</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level6_paint.png?raw=true" alt="level6">
  <br>
  <br>

  This level introduces the **internet**. The internet behaves like a router. However, if an interface is connected directly or indirectly to the internet, it **cannot** have an IP address in the following reserved private IP ranges:


  ```
  192.168.0.0 - 192.168.255.255 (65,536 IP addresses)
  172.16.0.0 - 172.31.255.255   (1,048,576 IP addresses)
  10.0.0.0 - 10.255.255.255     (16,777,216 IP addresses)
  ```
  **1.** The **next hop** of the internet is already entered, and matches the IP address of the *Interface R2*. Therefore we only need to bother with the destination of the internet.
  <br>
  <br>
  The internet must send its packets to *Client A*. To do so, the internet's destination must match the network address of *Client A*. Let's find the network address of *Client A*:
  <br>
  *Client A*'s mask is *255.255.255.128*, which is equivalent to */25*. This means that the first 25 bits of its IP address are its network address. We know then that the first 3 bytes (24 bits) of its IP address make part of its network address:
  <center>

  ```
  40.178.145.?
  ```
  </center>

  We now only need to find out if the 25th bit is a 1 or a 0.
  <br>
  If we convert the number 227 to binary, we get ``11100011``. The first digit, which corresponds to the 25th bit, is a 1. Since only the 25th bit is part of the network address and not the remaining 7 bits, we get ``10000000`` for the last byte of the network address, which is 128 in decimal.
  <br>
  <br>
  The full network address is:
  <center>

  ```
  40.178.145.128
  ```
  </center>

  With a range of *40.178.145.129 - 40.178.145.254* for its host addresses.
  <br>
  <br>
  We can now put this address of **40.178.145.128** in the Internet destination. The **/25** following the destination address represents the mask applied to its address.
  <br>
  <br>
  A destination of *40.178.145.227/25* is equivalent to the destination address *40.178.145.128/25*, since the mask of */25* will turn all the bits after the 25th to 0 to get the destination's network address.

  <div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 7</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level7_paint.png?raw=true" alt="level7">
  <br>
  <br>

  This level introduces the concept of **overlaps**. The range of IP addresses of a network must not overlap the range of IP addresses of a separate network. Networks are separated by routers.
  <br>
  <br>

  **1.** We have 3 separate networks:
  <br>

  1. Between *Client A* and *Router R1*.
  2. Between *Router R1* and *Router R2*.
  3. Between *Router R2* and *Client C*.

  For *Interface A1*, we cannot choose our IP address freely since the IP of *Interface R11* is already entered. Also, if we give it a mask of */24*, the IP address range will overlap with the range of *Interface R12*, which is already entered. They would both be in the range of *93.198.14.0 - 93.198.14.255*.
  <br>
  <br>

  Since we need addresses for 3 separate networks, it is convenient to split the last bytes of the address into 4 or more address ranges. We do this by using a mask of */26* or higher. The mask of */28* for example will give us 16 ranges, from which we use the following 3:

  ```
  93.198.14.1 - 93.198.14.14    (Client A to Router R1)
  93.198.14.65 - 93.198.14.78   (Router R1 to Router R2)
  93.198.14.241 - 93.198.14.254 (Router R2 to Client C)
  ```

  To calculate the possible ranges of a mask:
  <br>
  https://www.calculator.net/ip-subnet-calculator.html?cclass=any&csubnet=28&cip=93.198.14.2&ctype=ipv4&printit=0&x=97&y=13

  <div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 8</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level8_paint.png?raw=true" alt="level8">
  <br>
  <br>

  **1.** The hosts *Client C* and *Client D* will send packets to the internet, then the internet will respond by sending packets all the way back to the initial sender. To send these packets, the internet uses the destination *49.175.13.0/26* to send the packets to the networks in the range of ``49.175.13.0 - 49.175.13.63``.
  <br>
  <br>
  All the receiving networks must be in this range, without overlapping each other.
  <br>
  <br>

  **2.** On *Interface R23* and *Interface R22* we use the mask *255.255.255.240* (or */28*), to conveniently split the range of */26* from the destination address, into 4 separate ranges. This separation of 4 is necessary since we have the following 3 networks that must not overlap:
  <br>

  1. *Router R1* to *Router R2*.
  2. *Router R2* to *Client C*.
  3. *Router R2* to *Client D*.

  Each of these networks can then be attributed one of the following IP ranges with a mask of */28*:
  ```
  49.175.13.0 - 49.175.13.15
  49.175.13.16 - 49.175.13.31
  49.175.13.32 - 49.175.13.47
  49.175.13.48 - 49.175.13.63
  ```
  Note that the network address (first) and the broadcast address (last) must be excluded from each range.
  <br>
  <br>

**3.** The destination and next hop for the internet are already entered. We only need to enter the next hop for the *Router R2*, which is the IP on the *Interface R21*.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 9</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level9_paint.png?raw=true" alt="level9">
  <br>
  <br>

  This level is quite straightforward since the internet does not initially send its packets to a specific network. Therefore, the separate networks do not need to share a common address range. I would suggest simply following the 6 goals of the level one by one until the level is completed.
  <br>
  <br>
  Remember not to use the network addresses from the reserved private IP ranges.
  <br>
  <br>

  **1.** **Goal 3** states that we must connect *meson* with the *internet*. The *internet* will then have to respond to *meson*, so we enter *meson's* network address in the *internet's* destination.
  <br>
  <br>
  **Goal 6** states that we must connect *cation* with the *internet*, so we enter *cation's* network address in the *internet's* destination.
  <br>
  <br>
  It is normal to have an empty field for the 3rd destination of the *internet*, and in *Router R1's* destination. Not all fields of the routing tables need to be filled.

  <div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 10</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level10_paint.png?raw=true" alt="level10">
  <br>
  <br>

  At this level, there are 4 different networks:
  <br>

  1. *Router R1* to *Switch S1*
  2. *Router R1* to *Router R2*
  3. *Router R2* to *Client H4*
  4. *Router R2* to *Client H3*
  <br>

  **1.** The internet must be able to send its packets to all the hosts, so its destination must cover the range of networks of all the hosts.
  <br>
  <br>

  *Interface R11* and *Interface R13* already have an IP address entered. This IP address only differs in its last byte. *Interface R11* has for last byte **1**, and *Interface R13* has for last byte **254**. To cover this wide range to IP addresses, we take a mask of **/24** for the *internet's* destination. This destination will cover a range of ``70.101.30.0 - 70.101.30.255``.

  <br>
  <br>

  **2.** When choosing the IP addresses, we must make sure of 2 things:
  <br>

  1. The IP address is covered by the *internet* destination.
  2. The IP address range of the various networks does not overlap.
  <br>
  
  With the IP addresses already entered (greyed out), let's examine the ranges covered by the various networks:
  <br>

  1. *Router R1* to *Switch S1* - Covers the range **70.101.30.0 - 70.101.30.127** (mask /25).
  2. *Router R2* to *Client H4* - Covers the range **70.101.30.128 - 70.101.30.191** (mask /26).
  3. *Router R1* to *Router R2* - Covers the range **70.101.30.252 - 70.101.30.255** (mask /30).
  4. *Router R2* to *Client H3* - ??? (mask ???).

  The only IP addresses left for the network "Router R2 to Client H3" are **70.101.30.192 - 70.101.30.251**. We can pick any mask that will let us take 2 IP addresses from that range to put in *Interface R22* and *Interface R31*.

  <div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>
