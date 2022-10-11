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

I think this is the hardest challenge in Forensics LMAO. "Clueless" - That just kept repeating in my head for few days xD

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

Open it up in `paint.net` software



