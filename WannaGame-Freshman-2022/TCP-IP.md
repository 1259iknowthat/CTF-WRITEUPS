# **TCP-IP**

```
My friend uploaded something to the internet. I got his packet...
```
![](https://user-images.githubusercontent.com/89141562/195091394-fd36d3c1-652b-40d1-8ec0-77063cda7aa4.png)

Let's jump to the given pcapng file in this challenge. According to the title (again), I filtered out those TCP packets. Here is the result.

![](https://user-images.githubusercontent.com/89141562/195091455-e474b2b1-8e36-4985-84d5-d2f917a29c0b.png)

If you follow TCP stream, you will find something very interesting on the third stream.

![](https://user-images.githubusercontent.com/89141562/195091521-53d5eada-d256-435e-abe5-8c99c131db30.png)

So there was a PNG image as we can see through data transmission in wireshark. I decided to dump out those data as hex values then use HxD to edit it because it was a corrupted PNG.

![](https://user-images.githubusercontent.com/89141562/195091563-815a24b3-cbce-4097-a2a0-e3a6952dcdba.png)

Fix error hex values of the PNG header from `25 70 6E 67 2E 2E 2E 2E 2E 2E 2E 2E 69 68 64 72` to `89 50 4E 47 0D 0A 1A 0A 00 00 00 0D 49 48 44 52` then we will have the image that has flag in it.

<img width="797" alt="" src="https://user-images.githubusercontent.com/89141562/195091785-1f3483a9-e018-42ca-82de-1ef31875cf12.png">

## FLAG: W1{y0u_kn0w_TCP?}
