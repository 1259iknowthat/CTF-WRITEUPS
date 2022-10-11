# **U like Dat Packet_**

```
Ông nội của mình trong lúc học thực hành nhập môn mạng đã bắt được một số lượng lớn packet bất thường đến từ một người nào đó, có vẻ như họ đang cố gắng gửi thông điệp gì đó cho ông của mình. Bạn có thể giúp ông mình chứ?
```
![](https://user-images.githubusercontent.com/89141562/195092117-dc7eb5f5-994e-42fe-b27d-1198ced6d424.png)

Once again, just look at the title then we have the hint : UDP. I filtered out UDP packets and saw a suspicious content. 

![](https://user-images.githubusercontent.com/89141562/195092183-acc0949d-bb6f-4381-8f35-e849aa011b26.png)


As you can see, UDP packets with destination port is 25522 have data length, which is decimal values. I decided to dump out these contents by using `Export Packet Dissections`, then grep those data bytes out. But before doing that, I must use different filter. In wireshark sections, we can see ICMP packets, which repeat the previous packet's data length. It will be very sussy if you dump those shitty out so I used this filter: `udp.port == 25522 && !icmp`. 

![](https://user-images.githubusercontent.com/89141562/195092466-ab4801cd-1989-461b-a3f6-8cb0721deeff.png)


This is how I dumped out decimal values after using `Export Packet Dissections` (you can use `tshark` instead of doing this):

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

![](https://user-images.githubusercontent.com/89141562/195092549-60c11a7e-7702-44ee-b3c3-4a79d1e7a08d.png)


At this point, I did not realize that the dump had no 0 byte packets so that the PNG image was corrupted. I had to do the job again, added some 0 bytes into it. The final result :( 

![](https://user-images.githubusercontent.com/89141562/195092720-50d58943-57dc-44dc-a916-88190ab8fc7f.png)


Using [`Barcode Reader`](https://online-barcode-reader.inliteresearch.com/) website to scan the QR code.

![](https://user-images.githubusercontent.com/89141562/195092595-76586880-e17b-4a77-ad9d-6f0b01628b0e.png)


## FLAG: W1{s1mpl3_n3tw0rk}





