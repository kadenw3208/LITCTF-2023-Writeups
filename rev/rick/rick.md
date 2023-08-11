# Rick
Category: **Reverse Engineering**
<br> Points: **116**
<br>Original Challenge Author: **eyangch**
<br> Writeup Author: **MoonCaller27**
## Problem Description
i lost my flag in this thing :(<br>
### downloads
[rick](http://34.29.19.233/dl/?rev/rick/rick)
## Writeup
When we open the file up, we can see this:
```
(Verse 1)
UwU, we're on an owo adventure tonight
In this uwu world, love takes flight
A bond so uwu, it'll never fade away
In this owo journey, together we'll stay

(Pre-Chorus)
UwU just wanna owo you forever
Gotta make you understand

(Chorus)
UwU's never gonna give you owo
UwU's never gonna let you uwu
UwU's never gonna say goodbye
And owo you, never gonna make you cry
UwU's never gonna say goodbye
UwU's never gonna tell a lie and hurt owo

(Verse 2)
Through uwu ups and owo downs we'll go
In this uwu maze, love will grow
With every uwu step, our hearts align
In this owo dance, our souls entwine

(Pre-Chorus)
UwU just wanna owo you forever
Gotta make you understand

(Chorus)
UwU's never gonna give you owo
UwU's never gonna let you uwu
UwU's never gonna say goodbye
And owo you, never gonna make you cry
UwU's never gonna say goodbye
UwU's never gonna tell a lie and hurt owo
```
This is only part of the file, the rest is in `file.md`.<br>
With such a long line of text, it is not clear how to approach the problem. However, knowing that the flag format of LITCTF has a `{` symbol in it, we can try to search it using the `Ctrl+F` keys. <br>
### ❗❗❗❗❗❗**IMPORTANT**❗❗❗❗❗❗❗❗
**You must make sure that you search for the right characters. Typically, the flag format of LITCTF is of the form `LITCTF{`, we must keep in mind that that may not be the case. Instead, we should copy the special characters that might appear in typical LITCTF flags, such as `{` or `_`. <br>**
### ❗❗❗❗❗❗**IMPORTANT**❗❗❗❗❗❗❗❗

After doing a search for the character `{` and shifting around the different occurrences the command found, we come to: 
```
(Ver}1l0rkc1r_7xen_3ht_3k4m_4nn0g_7pgt4hc{FTCTILse 7)
UwU and owo, a love so true
In this never-ending tale, me and you
Through uwu laughter and owo tears
Our love will echo for endless years
```
Huh, it seems like this line in the verse wasn't meant to be put here. 
`}1l0rkc1r_7xen_3ht_3k4m_4nn0g_7pgt4hc{FTCTIL`<br>
Seeing the characters `FTCTIL`, we realize that this is `LITCTF` backwards! We now think of using a [line reverser](https://onlinetexttools.com/reverse-text) to find the flag. 
<br>Flag: `LITCTF{ch4tgp7_g0nn4_m4k3_th3_nex7_r1ckr0l1}`
