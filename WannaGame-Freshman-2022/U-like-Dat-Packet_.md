# **U like Dat Packet_**

```
Ông nội của mình trong lúc học thực hành nhập môn mạng đã bắt được một số lượng lớn packet bất thường đến từ một người nào đó, có vẻ như họ đang cố gắng gửi thông điệp gì đó cho ông của mình. Bạn có thể giúp ông mình chứ?
```
~pic~

Once again, just look at the title then we have the hint : UDP. I filtered out UDP packets and saw a suspicious content. 

~pic~

As you can see, UDP packets with destination port is 25522 have data length, which is decimal values. I decided to dump out these contents by using `Export Packet Dissections`, then grep those data bytes out. But before doing that, I must use different filter. In wireshark sections, we can see ICMP packets, which repeat the previous's data length. It will be very sussy if you dump those shitty out so I used this filter: `udp.port == 25522 && !icmp`. 

~pic~

This is how I dumped out decimal values after using `Export Packet Dissections`:

```
┌──(kali㉿devilmachine)-[/mnt/d/WSL_LAB/Workplace/uit]
└─$ cat test.txt | head
No.     Time           Source                Destination           Protocol Length Info
      1 0.000000000    192.168.219.130       192.168.219.128       UDP      179    25135 → 25522 Len=137

Frame 1: 179 bytes on wire (1432 bits), 179 bytes captured (1432 bits) on interface eth0, id 0
Ethernet II, Src: VMware_48:ea:bb (00:0c:29:48:ea:bb), Dst: VMware_7c:7c:f0 (00:0c:29:7c:7c:f0)
Internet Protocol Version 4, Src: 192.168.219.130, Dst: 192.168.219.128
User Datagram Protocol, Src Port: 25135, Dst Port: 25522
Data (137 bytes)

0000  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00   ................

┌──(kali㉿devilmachine)-[/mnt/d/WSL_LAB/Workplace/uit]
└─$ cat test.txt | head | grep "Data ("
Data (137 bytes)

┌──(kali㉿devilmachine)-[/mnt/d/WSL_LAB/Workplace/uit]
└─$ cat test.txt | grep "Data (" > bruh.txt

┌──(kali㉿devilmachine)-[/mnt/d/WSL_LAB/Workplace/uit]
└─$ cat bruh.txt
Data (137 bytes)
Data (80 bytes)
Data (78 bytes)
Data (71 bytes)
Data (13 bytes)
Data (10 bytes)
Data (26 bytes)
Data (10 bytes)
Data (13 bytes)
Data (73 bytes)
Data (72 bytes)
Data (68 bytes)
...
```

We need to delete unnecessary strings, put it on cyberchef to transfer to readable text. Here is the result UwU

~pic~

At this point, I did not realize that the dump had no 0 byte packets so that the PNG image was corrupted. I had to do the job again, added some 0 bytes into it. The final result :( 

~pic~ 

Using [`Barcode Reader`](https://online-barcode-reader.inliteresearch.com/) website to scan the QR code.

~pic~

## FLAG: W1{s1mpl3_n3tw0rk}





