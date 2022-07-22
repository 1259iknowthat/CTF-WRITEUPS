# FORENCIS
_những thử thách có WU-ed có nghĩa là mình đã đọc WU rồi mới giải_
___
**_unpuzzled4_**
```
Description

THIS IS AN **OSINT** CHALLENGE

It looks like unpuzzler7 has been getting into photography recently. 
His pictures aren't very good though, you can't even tell what the location of the pictures are! 
(To access this challenge you must join our discord server at https://discord.gg/ctf)
```

Đề bài yêu cầu chúng ta truy cập server discord theo đường dẫn. Sau khi mình đã vào được server thì mình đi tìm user unpuzzled7 và thấy được profile như sau:


![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/profile.png "profile")

Truy cập theo URL được gắn ở profile, mình đã được dẫn đến một trang web Flickr của user Melvin Wu:

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/flickr.png "flickr")

Với bức ảnh đầu chỉ là rickroll :)))))) nên mình sang bức ảnh thứ hai và tìm thấy điều thú vị:

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/flickr2.png "flickr2")


Mình nhấp phần thông tin EXIF và thấy 
- FLAG: ictf{1mgur_d03sn't_cl3ar_3xif}

___

**_journey_**
```
 Description

This is an **OSINT** challenge.

Max49 went on a trip... can you figure out where? 
The flag is ictf{latitude_longitude}, where both are rounded to three decimal places. 
For example, ictf{-95.334_53.234}
Attachments

https://imaginaryctf.org/r/06FSz#IMG_2901.jpg
```

Đến với thử thách tiếp theo, đề bài đã cho mình một bức ảnh như sau:

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/journey.jpg "journey")

Mình sử dụng yandex để tìm thông tin liên quan đến bức ảnh này và thấy vài điều thú vị.
Như trang web này đã hiển thị chính xác địa điểm của bức ảnh đề bài cho:

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/web.png "web")

Do trang web sử dụng tiếng Nga, vì thế mình copy title và dịch ra được đoạn này: "Through the streets of Orvieto with details".

"Orvieto" có lẽ đây chính là nơi mà bức ảnh đã được chụp, để thu gọn phạm vị hơn nữa, mình tìm thông tin "La Pergola" đã xuất hiện trên tấm biển trong bức ảnh. Tadaaaa ~ 

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/search.png "search")

Từ đây mình lên googlemap và search thông tin liên quan, sau đó bắt đầu street view

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/streetview.png "streetview")


Sau khi đến điểm này, mình nhận ra đây chính là địa điểm trong bức ảnh.

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/place.png "place")

Vì thế mình ra ngoài điểm ghim trên bản đồ để lấy tọa độ, đồng thời làm tròn đến số thập phân thứ ba theo đề. Có thể thấy, địa điểm "flag" khá gần với địa điểm nhà hàng mình tra lúc nãy :>>>

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/toado.png "place")

- FLAG: ictf{42.717_12.112}

___


**_unpuzzled3_**
```
Description

THIS IS AN **OSINT** CHALLENGE

unpuzzler7#6451 is back! I've heard that he's been listening to a lot of music lately. 
Think that you might be able to find something? 
(To access this challenge you must join our discord server at https://discord.gg/ctf)
```

Hmmm, lại là một thử thách nữa liên quan tới user unpuzzled7 này. Mình vừa nhớ lại thử thách đầu tiên, ở profile của unpuzzled7 không chỉ có đường dẫn Flickr mà còn có cả Spotify. Vì thế mình quyết định quay lại điều tra:

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/profile2.png "profile2")

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/music.png "music playlists")

Sau khi nhấp vào đường dẫn thì mình đã tới được playlist của anh chàng này. Thoạt nhìn có vẻ không có gì mờ ám cả nên mình thử vào xem cả hai playlist có gì thứ vị.

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/rickroll.png "rickroll")

Ở playlist đầu tiên chỉ là rickroll :))))))

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/flag.png "music2")

Ở playlist thứ hai, hình như cũng chả có gì đặc biệt. Mình đã kẹt ở đây khá lâu, mò đi mò lại cái playlists, rồi mò sang cả follower nhưng cũng chả thấy gì. Cho đến khi mình ăn cơm xong và quay lại thì thấy một điều khá là thú vị :>> các chữ cái đầu của các bài hát bỗng dưng ghép lại thành ICTF{. Hohohoo

- FLAG: ictf{SPOTIFY_jAMMMMMM_78D5B4}
____

**_Orge_**
```
Description

What are you doing in my swamp?!

Attachments

docker pull ghcr.io/iciaran/ogre:ctf
```
Okay giờ chúng ta sẽ đến với thử thách tiếp theo - docker. Đề bài yêu cầu mình pull docker về nên mình pull về thử và dùng lệnh ```docker images``` để xem có image gì ở trỏng

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/dockercmd.png "docker")

Sau đó mình dùng lệnh ``` docker inspect``` để xuất các thông tin liên quan đến các objects như containers, volumes, network gì gì đó...

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/docker.png "docker")

Mình tiếp tục xem thử coi có gì hấp dẫn hong và có thứ hấp dẫn thiệt :)))))))

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/secretcipher.png "secretcipher")

Đây có lẽ là đoạn mã base64 khá là mờ ám, đã vậy còn có gì đó /secret. Vì thế mình quyết định giải mã base64 bằng công cụ [cyberchef](https://cyberchef.org/) khá là nổi tiếng.

- FLAG: ictf{onions_have_layers_images_have_layers}

___

**_improbus_** _WU-ed_

```
Description

Did Caesar like PNG files?

Attachments

https://imaginaryctf.org/r/tTkud#corrupted.png
```
Thử thách này cho chúng ta một file có lẽ là file png nhưng đã bị lỗi gì đó. Mình cho thử raw data của file này lên công cụ render của cyberchef thì ra hẳn đáp án

![pic](https://github.com/1259iknowthat/CTF-WRITEUPS/blob/main/Pictures/ictf2022/improbus.png "improbus")

- FLAG: ictf{fixed!_3f5ce751}

*thử thách khá là bủh bủh lmao**






