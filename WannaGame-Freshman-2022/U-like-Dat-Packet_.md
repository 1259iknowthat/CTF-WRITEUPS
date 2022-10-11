# **U like Dat Packet_**

```
Ông nội của mình trong lúc học thực hành nhập môn mạng đã bắt được một số lượng lớn packet bất thường đến từ một người nào đó, có vẻ như họ đang cố gắng gửi thông điệp gì đó cho ông của mình. Bạn có thể giúp ông mình chứ?
```
~pic~

Once again, just look at the title then we have the hint : UDP. I filtered out UDP packets and saw a suspicious content. 

~pic~

As you can see, UDP packets with destination port is 25522 have data length, which is decimal values. I decided to dump out these contents by using `Export Packet Dissections`, then grep those data bytes out. But before doing that, I must use different filter. In wireshark sections, we can see ICMP packets, which repeat the previous's data length. It will be very sussy if you dump those shitty out so I used this filter: `udp.port == 25522 && !icmp`. 

~pic~

The dumped data:

```
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

Delete unnecessary strings, put it on cyberchef to transfer to readable text. Here is the result UwU

~pic~

At this point, I did not realize that the dumped out had no 0 byte packets so that the PNG image was corrupted. I had to do the job again, added some 0 bytes to it. The final result :( 

~pic~ 

Using [`Barcode Reader`](https://online-barcode-reader.inliteresearch.com/) website to scan the QR code.

~pic~

## FLAG: W1{s1mpl3_n3tw0rk}





