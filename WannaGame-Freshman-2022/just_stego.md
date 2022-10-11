# **just_stego**

```
Good Luck :)

#P/s: Wrap the result in W1{}

just_stego hint1: flag has two parts
just_stego hint2: (The given image)
just_stego hint3: i love RGB with LSB
```
![](https://user-images.githubusercontent.com/89141562/195093225-e4c6f7e2-0108-4382-91d9-774465cc6150.png)

![hint3](https://user-images.githubusercontent.com/89141562/195093297-55c098be-ab94-40e1-9c24-e45949776c3e.png)

I think this is the hardest challenge in Forensics (in my opinion) LMAO. "Clueless" - That had just kept repeating in my head for few days xD. I had stuck for many hours. I'm so noob, sadge :(

First of all, I used `binwalk` to extract some contents in the image. There was actually 1 PNG file in it.

```
┌──(kali㉿devilmachine)-[/mnt/d/WSL_LAB/Workplace/uit/data]
└─$ binwalk challenge.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
30            0x1E            TIFF image data, big-endian, offset of first image directory: 8
869376        0xD4400         PNG image, 1089 x 397, 8-bit/color RGBA, non-interlaced
869430        0xD4436         Zlib compressed data, compressed
```

You can use `binwalk --dd='.*'` or `foremost`. I decided to use foremost (binwalk -e won't extract anything). 

```
┌──(kali㉿devilmachine)-[/mnt/d/WSL_LAB/Workplace/uit/data]
└─$ foremost challenge.jpg
Processing: challenge.jpg
|*|
```

![steg4](https://user-images.githubusercontent.com/89141562/195093542-ba33b55b-73a6-45e8-a059-13600a5635e0.png)

Open it up in `paint.net` software, I noticed there were some color squares on top left conner.

![](https://user-images.githubusercontent.com/89141562/195093574-a9c8c860-60ea-4c19-9ae6-580fcecef3ac.png)


According to the third hint, I use a tool from cyberchef: `Extract LSB`. 

![](https://user-images.githubusercontent.com/89141562/195093595-3eb64605-d967-4732-a420-a3c8a1ba8fca.png)

I chose RGB pattern and Row order based on the colors line. That's the second part of the flag.

The first part is mentioned by the second hint. We need to "think" out of the box which means the JPG image has longer length than what we see. After doing some searching methods, I found this [site](https://blog.cyberhacktics.com/hiding-information-by-changing-an-images-height/).

![](https://user-images.githubusercontent.com/89141562/195093736-eae4b654-4dda-4dfc-9ac6-e2049a973684.png)

From what the author said in the blog, we can come to the following conclusion: `01 8D 04 41` is the length and width hex values. Just simply change length values to something bigger like `06 90`, you can have the whole picture with flag in it.

![](https://user-images.githubusercontent.com/89141562/195093828-d02aac54-2148-4058-a5af-aeea1a9d8638.jpg)

## FLAG: W1{see_you_in_Wanna.W^n1357}



