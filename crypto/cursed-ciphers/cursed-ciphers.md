# cursed-ciphers
Category: **Crypto**<br>
Points: **388**<br>
Original Challenge Author: **timetravelingcat (cat)**<br>
Writeup Author: **MoonCaller27**
## Problem Description
i love ciphers  
link: [https://docs.google.com/document/d/1EZZUHKMm6EIub0skuCa0a4IvETzbmNaM1wogRm-8Fj4/edit?usp=sharing](https://docs.google.com/document/d/1EZZUHKMm6EIub0skuCa0a4IvETzbmNaM1wogRm-8Fj4/edit?usp=sharing)
## Writeup
To find what the Google Doc contains, check the file `doc`. <br>
When we open it up, we find one section for `keys`, and the other for `encrypted flags`. We have no clue what cipher this could be, so we can plug the very first encrypted flag into a [cipher identifier](https://www.dcode.fr/cipher-identifier) to see if we can find which cipher this might be. Looking at the left side, we can see:
![im](https://i.ibb.co/vkD0Yb8/image.png)<br>
We can try decoding the very first cipher, the [Jefferson Wheel Cipher](https://www.dcode.fr/jefferson-wheel-cipher). 
![im2](https://i.ibb.co/P4rP7Z3/image.png)
Hmm, it doesn't seem like we can gain anything useful by using the `Jefferson Wheel Cipher`. Let's try the next cipher on the list, which is the [Affine Cipher](https://www.dcode.fr/affine-cipher). 
![im3](https://i.ibb.co/G01ST6D/image.png)
Aha! We see the characters `litctf{` in the first entry of the results and we now know that we are on the right track. <br>
### ⚠️⚠️⚠️⚠️⚠️WARNING!!!⚠️⚠️⚠️⚠️⚠️⚠️⚠️
**It is crucial not to start off going for the wrong cipher in the first place. If you immediately start going for the `Jefferson Wheel Cipher`, it is impossible to find the answer.**
### ⚠️⚠️⚠️⚠️⚠️WARNING!!!⚠️⚠️⚠️⚠️⚠️⚠️⚠️

Now we know which cipher to use for decoding, we can proceed with the next information that we have: keys. We can look at the first few keys and their respective flags to get some information.
```
Keys:
17 22 | 0 |
21 17 | 1 | 1
11 1 | 2 | 12 18
23 16 | 3 | 0 10 12
21 7 | 1 | 18
```
```
Ciphers:
bchehd{wDDcJM_SO_nMCapMv}
omaHAS{RsSOEx_JB_mXdZqxc}
lSCxCE{BEEloi_DF_MilZYtI}
nslKlb{QBBndh_gw_NeSAfeH}
eEqxQi{hIieuN_Zr_CsTPgNs}
```
As seen from the previous image, it seems like that the first 2 values to the left of the first `|` are the values of A and B for decoding, respectively. After, we can see that the number in the middle represents the number of values to the left of the second `|`. However, since the middle value of the very first cipher is 0, let's analyze the second flag.
![im4](https://i.ibb.co/HTM3mNv/image.png)
As a confirmation of our hypothesis, we can see that the A and B values for the first entry are 21 and 17, just like it says in the keys.      However, the flag we obtain doesn't seem quite right:
<br>`lbtCTF{AfFLNe_MY_bEiOved}`<br>
The first thing that we notice is that in the first part, there should be a `i` instead of a `b` at position 1.  (Note: In computer science, it is typical to use indices that start at 0 instead of 1). Let's shift back to the key for this: `21 17 | 1 | 1`. It is at position 1! Hmm, we may be on to something here!

### ❗❗❗❗❗❗IMPORTANT❗❗❗❗❗❗
**In order to solve the question, we need to realize that the indices of the cursed characters are given in the key section.**
### ❗❗❗❗❗❗IMPORTANT❗❗❗❗❗❗
Let's look at the third flag. By analysis, we also realize that the words inside the curly braces (`{}`) should spell out to be `affine_my_beloved` (with varying capitalization). So, we note down the index of the characters that are wrong, or **cursed** (🤔🤔🤔).  First decoding the `Affine Cipher` gives `iLTcTF{AFFind_MY_BdiOVeD}`.  The third row of the keys gives `11 1 | 2 | 12 18`.  The characters at positions `12` and `18` are both `d`. Now we are pretty sure of our pattern.<br><br>

The flag format for LITCTF is `LITCTF{`, so we need to find a ciphertext with all capital letters in the first 6 characters. Doing so  across all ciphers only yields 3 possible ciphers.
```
XXCZCY{rYyiEH_nj_ihirkHq}
MBYFYQ{pQqkCv_Hz_KampoaA}
YYCNCI{ZIIgmB_fl_gbDtQuu}
```
Plugging these flags into the Affine Cipher decoder gives:
```
IITCTF{aFfbNE_my_bebavEd}
LITCTF{aFfbNe_My_BdlavdD}
LLTCTF{AFFbnE_my_beIoVdd}
```
Of these 3, only the 2nd one is in the flag format, so we assume this is the one we have to solve. After counting, we see that `MBYFYQ{pQqkCv_Hz_KampoaA}` is the 31st entry in the list, so we find the 31st key: `21 15 | 4 | 10 18 20 22`. We can now fix the cursed characters:
```
The character at position 10 is b and should be i
The character at position 18 is d and should be e
The character at position 20 is a and should be o
The character at position 22 is d and should be e
```
After doing this we get the flag `LITCTF{aFfiNe_My_BeloveD}`. However, this flag doesn't work! However, most flags include numbers to make the flag complicated, so we can replace the cursed characters with numbers representing the character, and this flag works.
<br>
Flag: `LITCTF{aFf1Ne_My_B3l0v3D}`
