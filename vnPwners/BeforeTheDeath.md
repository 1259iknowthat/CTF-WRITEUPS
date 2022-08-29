# **BEFORE THE DEATH**
```
I find playing guessing game interesting so I took one on google. After finishing the first round, my computer suddenly shown errors got crashed. Luckily, I was able to dump memory before the crash happened. Could you analyze what was happening in my computer at that time?

P/s: The file guessing_game is not a real virus, it just executes nc and binds at port 30002 in LAN so your antivirus may misunderstand the file as virus. Turn of your antivirus and you can run that file without any worry =)))

P/s2: There will have a netcat connection for you to login and get flag so don't try to find flag in the memory dump because there is no flag in it.

Challenge: https://drive.google.com/file/d/1UQ8TA_dOKLJ7eKPChMCaYgYsoYTsAhjK/view?usp=sharing

(We will get the ssh server login information after applying the username and password to the author)
```
First of all, I downloaded the file given in the description. Turns out, it was a memory dump. So, I decided to use Volatility to solve.

`./vol imageinfo -f /mnt/d/WSL_LAB memory.raw`

I used this command to get a basic look about the system which later is WinXPSP2x86.

Then I use `./vol -f /mnt/d/WSL_LAB/memory.raw --profile=WinXPSP2x86 pstree` to get a list of running process, because the description told us that there was a program call guessing_game

![](20220829200926.png)  

So we will notice that there's a program called guessing_game.e has the PID 1504.

I decided to extract it by using `dumpfiles` (if you try to dump process, it will be a bad idea because it causes losing datas/bytes)

![](20220829201352.png)  

If you look carefully, there's a line "Documents and Settings\Louis\Desktop\guessing_game.exe". So we have known the username of this machine is `Louis`.

Next, following the order of the list, I rename the exe file from .img to .exe by `mv file.1504.0x81c5b008.img guessing_game.exe` and run it from Windows. We got the result below.

![](20220829202038.png)  

After a few tries, finally, I got the password: `23ssqn_9qtHuSqLUbTTWSNC8P9rw_sLX`

![](20220829201955.png)  

Final step, I logged into the server to get the flag. Run "auth" program to get to root then you are done!

![](20220829202453.png)  

## FLAG: ForSpirit{y0U_sh0uLD_b4Ck_Up_d4T4_r3Gul4RlY_572348aa19eaa992110006276f43e397} 

~ **_H4PPY H4CK1NG_** ~