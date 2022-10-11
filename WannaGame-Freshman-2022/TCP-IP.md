# **TCP-IP**

```
My friend uploaded something to the internet. I got his packet...
```
~pic~

Let's jump to the given pcapng file in this challenge. According to the title (again), I filtered out those TCP packets. Here is the result.

~pic~

If you follow TCP stream, you will find something very interesting on the third stream.

~pic~

So there was a PNG image as we can see through data transmission in wireshark. I decided to dump out those data as hex values then use HxD to edit it because it was a corrupted PNG.

~pic~

Fix error hex values of the PNG header from `25 70 6E 67 2E 2E 2E 2E 2E 2E 2E 2E 69 68 64 72` to `89 50 4E 47 0D 0A 1A 0A 00 00 00 0D 49 48 44 52` then we will have the image that has flag in it.

~pic~

## FLAG: W1{y0u_kn0w_TCP?}