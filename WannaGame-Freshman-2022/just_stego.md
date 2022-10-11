# **just_stego**

```
Good Luck :)

#P/s: Wrap the result in W1{}

just_stego hint1: flag has two parts
just_stego hint2: (The given image)
just_stego hint3: i love RGB with LSB
```
~pic~

~pic~

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

Open it up in `paint.net` software, I noticed there were some color squares on top left conner.

~pic~

According to the third hint, I use a tool from cyberchef: `Extract LSB`. 

~pic~

I chose RGB pattern and Row order based on the colors line. That's the second part of the flag.

The first part is mentioned by the second hint. We need to "think" out of the box which means the JPG image has longer length than what we see. After doing some searching methods, I found this [site](https://blog.cyberhacktics.com/hiding-information-by-changing-an-images-height/).

From what the author said in the blog, we can come to the following conclusion: `01 8D 04 41` is the length and width hex values. Just simply change length values to something bigger like `06 90`, you can have the whole picture with flag in it.

~pic~

## FLAG: W1{see_you_in_Wanna.W^n1357}



