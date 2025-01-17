# Challenges Solved
## Reverse Engineering
-      VM0 (100 points)
-      Ready Gladiator 0 (100 points)
-      Ready Gladiator 1 (200 points)
-      Ready Gladiator 2 (400 points)
-      Reverse (100 points)
-      Safe Opener 2 (100 points)
-      timer (100 points)
-      No way out (200 points)


## Cryptography
-      Power analysis: warmup (200 points)
-      Power analysis: 1 (400 points)
-      Power analysis: 2 (500 points)
-      SRA (400 points)


# REVERSE ENGINEERING
## VM0 (100 points)
-----------------------------------------------------
The task involves a Colladae file, the first step I took was to open the file in Three.js, an online emulator for 3D designs. Upon loading the file,we got this 
-----------------------------------------------------
![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/vm0/image.png)

 I noticed that the box contained two gears, and I decided to change the view to wireframe to better understand the structure of the model.
 -----------------------------------------------------
 ![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/vm0/image2.png)

By switching to wireframe view, I was able to see the box's internal structure more clearly and identify the gears. I then proceeded to dismantle the box by removing each Lego piece in the body one by one until the gears were the only components remaining. This process allowed me to focus solely on the gears.

-----------------------------------------------------
![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/vm0/Studio_Project.gif)


To go into further detail, a Collada file is a type of 3D model file format that is used to represent 3D graphics in a variety of applications. Three.js is a JavaScript library that provides a simple way to create and display 3D graphics on the web. By using Three.js to load the Collada file, I was able to easily manipulate and explore the 3D model, including changing the view to wireframe mode to see the model's internal structure.

After dismantling the box by removing each Lego piece by piece we arrived at this.
-----------------------------------------------------
![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/vm0/image3.png)

The driver gear (the bigger one) has 40 teeths, while the driven gear (the smaller one) has 8 teeths. So, if the driver gear makes 1 rotation, the driven gear will make 5 rotations. If you recall we have an input we got from the file we downloaded from the task description.

```
┌──(bl4ck4non㉿bl4ck4non)-[~/Downloads/CTF/picoCTF_2023/rev_eng]
└─$ ls
input.txt
                                                                                                                                                                                                
┌──(bl4ck4non㉿bl4ck4non)-[~/Downloads/CTF/picoCTF_2023/rev_eng]
└─$ cat input.txt 
39722847074734820757600524178581224432297292490103996086521425478666370329 
```
So, if the input is the number of rotations the driver gear this means the driven gear will make 5 times the rotation of the driver gear. This means the driven gear will make ```198614235373674103788002620892906122161486462450519980432607127393331851645``` number of rotations. This number of rotations for the driven gear is actually encoded. Interesting right?😎

Lets decode this from Decimal to Hex

![image](https://user-images.githubusercontent.com/67879936/228673512-1c6a412a-7838-4d18-88df-fc41272abd3e.png)

Then we convert from Hexadecimal to Text

![image](https://user-images.githubusercontent.com/67879936/228673766-6d7ab372-bc06-4bba-b48b-8c4ba3ae38ee.png)

cool, we got our flag

------------------------------

## Ready Gladiator 0 (100 points)
---------------------------------------------------

![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/RG0/RG0.png)


This challange is about the CodeWars warriror, in this task they need us to make a warrior that always loses with not ties

Simple solution was to send `end` to the terminal after connecting to the instance throws us back our flag!! (<_>)


![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/RG0/Flag_RG0.png)


## Ready Gladiator 2 (400 points)
--------------------------------------------


This challenge focuses on wining every round in a CoreWars game, So the plan is to find a suitable strategy to make our warrior win every round in the game

One of the ways is the use a Bomber script. A bomber randomly drops complex bombs designed to damage or stun the opponent. So i found this blog online that has multiple strategies of wining an imp game

Link: https://corewar.co.uk/strategy.htm

![image](https://user-images.githubusercontent.com/67879936/228682023-04c75e21-43cf-49bd-a57a-e3159446845f.png)

tips for winning every round in an imp game

So i tried this particular bomber to test if i can win all the rounds, because the script looks simple and short. Here is the link below 

Link: https://corewar.co.uk/heremscimitar.htm

Copy the code from the site and paste it into your imp.red file. 

```
┌──(bl4ck4non㉿bl4ck4non)-[~/Downloads/CTF/picoCTF_2023/rev_eng]
└─$ nano imp.red
                                                                                                                                                                                                
┌──(bl4ck4non㉿bl4ck4non)-[~/Downloads/CTF/picoCTF_2023/rev_eng]
└─$ cat imp.red  
;redcode-94
;name Herem/Scimitar
;author A.Ivner,P.Kline
;strategy bomber
;macro
step     equ   27
count    equ   1470

         jmp   clr
start    mov   sb,@st
st       mov   {100,cnt-(2count*step)-1
         add   bmb,st
cnt      djn   start,#count-1
sb       spl   #step,0
clr      mov   bmb,>-13
         djn.f clr,{-14
  for 22
         dat   0,0
  rof
         dat   <4,step+step
bmb      dat   <4,step+step
            start
end
```


Run the imp file against the server using the nc listener provided by PicoCTF

>command:```nc saturn.picoctf.net 64120 < imp.red```



```
┌──(bl4ck4non㉿bl4ck4non)-[~/Downloads/CTF/picoCTF_2023/rev_eng]
└─$ nc saturn.picoctf.net 64120 < imp.red
;redcode-94
;name Herem/Scimitar
;author A.Ivner,P.Kline
;strategy bomber
;macro
step     equ   27
count    equ   1470

         jmp   clr
start    mov   sb,@st
st       mov   {100,cnt-(2count*step)-1
         add   bmb,st
cnt      djn   start,#count-1
sb       spl   #step,0
clr      mov   bmb,>-13
         djn.f clr,{-14
  for 22
         dat   0,0
  rof
         dat   <4,step+step
bmb      dat   <4,step+step
            start
end
Submit your warrior: (enter 'end' when done)

Warrior1:
;redcode-94
;name Herem/Scimitar
;author A.Ivner,P.Kline
;strategy bomber
;macro
step     equ   27
count    equ   1470

         jmp   clr
start    mov   sb,@st
st       mov   {100,cnt-(2count*step)-1
         add   bmb,st
cnt      djn   start,#count-1
sb       spl   #step,0
clr      mov   bmb,>-13
         djn.f clr,{-14
  for 22
         dat   0,0
  rof
         dat   <4,step+step
bmb      dat   <4,step+step
            start
end

Warning in line 22: '            start'
        Ignored, redefinition of label 'start'
Warning:
        Missing ';assert'. Warrior may not work with the current setting
Number of warnings: 2

Rounds: 100
Warrior 1 wins: 100
Warrior 2 wins: 0
Ties: 0
You did it!
picoCTF{d3m0n_3xpung3r_ed173f56}
```


cool, we got our flag


## Ready Gladiator 1 (200 points)
-----------------------------------------------------




We use thesame code as ready gladiator 2 to solve this challenge since the solution need's it to get atleast one win which the code has

## Reverse (100 points)
----------------------------------------------------

![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/reverse/reverse.png)

This was a basic reverse engineering challenge, as usual runing strings on the file and greping for keyword `pico` gave us the flag!! (<_>)

![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/reverse/reverse_flag.png)

## Safe Opener 2 (100 points)
---------------------------------------------------

![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/safeopener/SafeOpener2.png)

Doing the same operation as the previous challenge we got our flag

![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/safeopener/safeopener_Flag.png)

## timer (100 points)
-----------------------------------------------------



![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/timer/timer.png)

This an andriod challenge, looks simillar to the apk series in the picoGym, first thing was to unpack the apk file downloaded with 

## No way out (200 points)
-----------------------------------------------------



![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/NoWayOut/nowayout.png)

Finaly!!, some 3D action game for reversing, this a 3D game made with Unity, downloading the file from [here](https://artifacts.picoctf.net/c/285/win.zip) and running it we have

![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/NoWayOut/nowayout1.png)

the goal of the challenge is to Escape and get the flag

 Upon launching the game and engaging in gameplay, I discovered that the game had limitations within its virtual walls. Despite being able to climb the ladder and view the visually mounted flag, it was unattainable. However, through the use of some tutorials and cheat engine, I was able to manipulate the character's position in both time and space. To achieve this, I initially attached the running game process to the cheat engine. Prior to running the game, it is advisable to follow all tutorials in the cheat engine as it is immensely helpful in identifying and changing parameters during gameplay. Next, I proceeded to locate the player's coordinates, which proved to be a cumbersome task. My technique involved finding the player's y-axis by differentiating between movement levels of high and low altitude values. After several minutes of searching, I was able to determine the player's y-axis. The x, y, and z coordinates are 4 bytes apart in the address register, thus by adding 4 bytes to the y-coordinate, we were able to determine the remaining coordinates, thereby allowing for teleportation to the flag destination without any constraints.After doing so we were greeted with a screen of our flag. 

This is a more similar challenge to what [liveoverflow](https://www.youtube.com/watch?v=yAl_6qg6ZnA) once solved



# Cryptography

## Power analysis: warmup (200 points)
-----------------------------------------------------



![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/power_analysis/power_warmup.png)

This challenge is one of the famous side channel attacks out there, but this has to do with AES, starting the instance of the challenge, we see a file, downloading it and on opening we get

```
#!/usr/bin/env python3
import random, sys, time

with open("key.txt", "r") as f:
    SECRET_KEY = bytes.fromhex(f.read().strip())

Sbox = (
    0x63, 0x7C, 0x77, 0x7B, 0xF2, 0x6B, 0x6F, 0xC5, 0x30, 0x01, 0x67, 0x2B, 0xFE, 0xD7, 0xAB, 0x76,
    0xCA, 0x82, 0xC9, 0x7D, 0xFA, 0x59, 0x47, 0xF0, 0xAD, 0xD4, 0xA2, 0xAF, 0x9C, 0xA4, 0x72, 0xC0,
    0xB7, 0xFD, 0x93, 0x26, 0x36, 0x3F, 0xF7, 0xCC, 0x34, 0xA5, 0xE5, 0xF1, 0x71, 0xD8, 0x31, 0x15,
    0x04, 0xC7, 0x23, 0xC3, 0x18, 0x96, 0x05, 0x9A, 0x07, 0x12, 0x80, 0xE2, 0xEB, 0x27, 0xB2, 0x75,
    0x09, 0x83, 0x2C, 0x1A, 0x1B, 0x6E, 0x5A, 0xA0, 0x52, 0x3B, 0xD6, 0xB3, 0x29, 0xE3, 0x2F, 0x84,
    0x53, 0xD1, 0x00, 0xED, 0x20, 0xFC, 0xB1, 0x5B, 0x6A, 0xCB, 0xBE, 0x39, 0x4A, 0x4C, 0x58, 0xCF,
    0xD0, 0xEF, 0xAA, 0xFB, 0x43, 0x4D, 0x33, 0x85, 0x45, 0xF9, 0x02, 0x7F, 0x50, 0x3C, 0x9F, 0xA8,
    0x51, 0xA3, 0x40, 0x8F, 0x92, 0x9D, 0x38, 0xF5, 0xBC, 0xB6, 0xDA, 0x21, 0x10, 0xFF, 0xF3, 0xD2,
    0xCD, 0x0C, 0x13, 0xEC, 0x5F, 0x97, 0x44, 0x17, 0xC4, 0xA7, 0x7E, 0x3D, 0x64, 0x5D, 0x19, 0x73,
    0x60, 0x81, 0x4F, 0xDC, 0x22, 0x2A, 0x90, 0x88, 0x46, 0xEE, 0xB8, 0x14, 0xDE, 0x5E, 0x0B, 0xDB,
    0xE0, 0x32, 0x3A, 0x0A, 0x49, 0x06, 0x24, 0x5C, 0xC2, 0xD3, 0xAC, 0x62, 0x91, 0x95, 0xE4, 0x79,
    0xE7, 0xC8, 0x37, 0x6D, 0x8D, 0xD5, 0x4E, 0xA9, 0x6C, 0x56, 0xF4, 0xEA, 0x65, 0x7A, 0xAE, 0x08,
    0xBA, 0x78, 0x25, 0x2E, 0x1C, 0xA6, 0xB4, 0xC6, 0xE8, 0xDD, 0x74, 0x1F, 0x4B, 0xBD, 0x8B, 0x8A,
    0x70, 0x3E, 0xB5, 0x66, 0x48, 0x03, 0xF6, 0x0E, 0x61, 0x35, 0x57, 0xB9, 0x86, 0xC1, 0x1D, 0x9E,
    0xE1, 0xF8, 0x98, 0x11, 0x69, 0xD9, 0x8E, 0x94, 0x9B, 0x1E, 0x87, 0xE9, 0xCE, 0x55, 0x28, 0xDF,
    0x8C, 0xA1, 0x89, 0x0D, 0xBF, 0xE6, 0x42, 0x68, 0x41, 0x99, 0x2D, 0x0F, 0xB0, 0x54, 0xBB, 0x16,
)

# Leaks one bit of information every operation
leak_buf = []
def leaky_aes_secret(data_byte, key_byte):
    out = Sbox[data_byte ^ key_byte]
    leak_buf.append(out & 0x01)
    return out

# Simplified version of AES with only a single encryption stage
def encrypt(plaintext, key):
    global leak_buf
    leak_buf = []
    ciphertext = [leaky_aes_secret(plaintext[i], key[i]) for i in range(16)]
    return ciphertext

# Leak the number of 1 bits in the lowest bit of every SBox output
def encrypt_and_leak(plaintext):
    ciphertext = encrypt(plaintext, SECRET_KEY)
    ciphertext = None # throw away result
    time.sleep(0.01)
    return leak_buf.count(1)

pt = input("Please provide 16 bytes of plaintext encoded as hex: ")
if len(pt) != 32:
    print("Invalid length")
    sys.exit(0)

pt = bytes.fromhex(pt)
print("leakage result:", encrypt_and_leak(pt))

```

This code is written in Python3 and involves reading a secret key from a text file and using it to encrypt data. The Sbox is a substitution table used for encryption. The "with open" statement reads the contents of the "key.txt" file, stripping any white space and converting the resulting string into bytes using the fromhex method. The Sbox is a list of hexadecimal values that will be used for encryption. The code returns the numbers of the last bit obtained from the result of xorring the key with our supplied plaintext which returns a content from the SBOX and print it to us.

![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/power_analysis/power_warmup1.png)

connecting to the server using netcat we got similar output as our assertion was correct, we could see that the output of our lekage result is 6 after supplying 16-byte of zero's. Taking a peak at the hint it mentioned ```The "encryption" algorithm is simple and the correlation between the leakage and the key can be very easily modeled```

using this method i was able to write a [script](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/power_analysis/warmup_sol.py) to find the possible key used

```

leak_buf = []
out = []
full = []

flag = ''

for k in range(0, 16):
    out = []
    first,start = True, False
    checkk = False
    teach = True
    third = False
    prev = 0
    h = 0
    j = 0
    try:
        for i in range(0, 256+1):
            pt = hex(bytes_to_long(f"{chr(i)}".encode()))[2:]
            pt = pt + "00"*(15 - k)
            pt = pt.zfill(32)
            val = encryp(pt)
            if val > h:
                h = val
            if first:
                prev = val
            elif (start and teach):
                if val == prev:
                    c = hex(bytes_to_long('c'.encode()))[2:]
                    c = c + '00'*13
                    
 <--snip>
  
print(flag)
assert len(flag) == 32, "not done"
print("Flag bruteforced!!!!!!!!!!!!!!!!!!!!!!!!")
```

  The code uses a for loop to iterate through 16 possible values of k. Within the loop, the code initializes several variables to their initial values, and then attempts to generate a string of binary digits that represents the output of an encryption function. 
 The code first generates a hex representation of the integer i, which ranges from 0 to 256. It then pads this hex representation with zeros so that it has a length of 32 characters. The resulting string is passed as input to the encryp function, which generates an output value.

 The code then checks the output value against several variables, including h, prev, start, teach, and first, to determine how to update the output binary string out. Depending on the values of these variables and the relationship between the current output value and the previous output value, the code appends either a 0 or a 1 to out.

 Once the loop over i completes, the code tries to match the binary string out to a pre-defined dictionary called mapping. If a match is found, the corresponding key value is added to the flag string. If a match is not found, the code appends a "-" character to the flag string and continues to the next iteration of the loop over k.

 After all 16 iterations over k complete, the final value of the flag string is printed to the console. If the length of the flag is not exactly 32 characters, an assertion error is raised. Otherwise, a success message is printed to the console.





## Power analysis: 1 (400 points)
-----------------------------------------------------------------------------------------


![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/power_analysis/power_1.png)

This is the same concept as warmup, but this time around instead of the number of leaked bits, it returns a list for power trace of about 2600K variables, which each differ for the same plaintext, my first approach was to write a script to send alot of plaintext and store the relation of plaintext and traces as a json file
this is the sample script which sends about 300 plaintext and store the content in a json file

```
import numpy as np
from pwn import *
from Crypto.Util.number import *
import os
import sys
import json


ind = 0
with open('tryout.json', 'w') as f:

    outt = {}
    count = 0
    for tnum in range(0, 50000):
        try:
            conn = remote("saturn.picoctf.net", sys.argv[1])
            pt = hex(bytes_to_long(os.urandom(16)))[2:]
            conn.sendlineafter("hex: ", pt)
            out = conn.recvuntil("]")
            conn.close()
            traces = re.findall('\d+', out.decode())
            traces = list(map(lambda x: int(x), traces))
            outt[tnum] = traces
            count += 1
            print(count, len(outt))
            if len(outt) > 301:
                f.write(json.dumps(outt))
                print("done")
                break
        except Exception as e:
            conn.close()
            print(e)
            continue

```
after doing so, the traces was plotted and we have this

![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/power_analysis/power_1_plot.png)

performing some analysis on this image we realized that the 10 peaks represents the end of each rounds, AES has a total of 10, 12, or 14 rounds (depending on the key size, in this case is 10 as indicated from the key size in the challenge description), each consisting of four main operations: SubBytes, ShiftRows, MixColumns, and AddRoundKey. These operations are performed on the data and the round key to create a new block of ciphertext.

This are the opreations

![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/power_analysis/opreations.png)

what we are interested in is the SubBytes of the first opeartion where the orginal plaintext and the key is first xorred, extracting the first operation and limiting our search space to the SubBytes operation, i wrote a [script](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/power_analysis/pa1.py) to accomplish that

```

hw = [bin(i).count("1") for i in range(0, 256)]
for bnum in range(14, 16):
    avg_point = leakage_point[bnum]
    mean_diffs = np.zeros(256)
    maxx = 0
    arr = {}
    for key in range(0, 256):
        m1 = []
        m0 = []
        for tnum in range(len(conrr)):
            # pt = hex(bytes_to_long(os.urandom(16)))[2:]
            # conn = remote("saturn.picoctf.net", sys.argv[1])
            # conn.sendlineafter("hex: ", pt)
            # out = conn.recvuntil("]")
            # conn.close()len()
            # traces = re.findall('\d+', out.decode())
            # traces = list(map(lambda x: int(x), traces))
            pt = conrr[tnum][0]
            trace = conrr[tnum][1][avg_point]
            # trace = np.asarray(trace)
            hyp = Sbox[int(pt[bnum*2:bnum*2 + 2], 16) ^ key]
            hyp = hw[hyp]
            #if target bit 1 or or 07
            if (hyp < threshold):
                m1.append(trace)
            else:
                m0.append(trace)
            # print(num1, num0)
        m1_avg = np.asarray(m1).mean(axis=0)
        m0_avg = np.asarray(m0).mean(axis=0)
        mean_diffs[key] = np.max(abs(m1_avg - m0_avg))
        # find the differences btw two means
        if mean_diffs[key] > maxx:
            maxx = mean_diffs[key]
            best_key = key
    flag += hex(best_key)[2:].zfill(2)
    for i in range(10):
        cont = sorted(mean_diffs,reverse=True)[i]
        print("KEY: ", hex(list(mean_diffs).index(cont))[2:], "Vaule: ", cont)
    print(flag, "found somoething !!! ______+++++++++!_____%2x"% best_key)

```




Explanation of the script

 The script reads in a JSON file containing the power traces and extracts a subset of the traces. It then performs a loop for each byte of the AES key, using the S-Box and the power traces to try to determine the byte of the key. The script calculates the differences between the means of the power traces for plaintexts that have the same byte in that position and the hypothesized byte value. The byte value with the maximum mean difference is chosen as the likely byte value of the key. The script then outputs the hex representation of the recovered key bytes. The script includes comments that provide some additional context and indicate some code that may have been used in previous iterations but has been commented out in the current version.

 ## Power analysis: 2 (500 points)
---------------------------------------------------------------------------------------

![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/power_analysis/power_2.png)

This is a similar challenge to the previous one but the only constraint here is less number of trace's which in these challenge is limited to 100, i used the same previous script to solve this challenge but i had to vary the threshold and compare the frequency of most occuring keys before we could get the passowrd, after doing that we got our complete flag.!!!!!!!!!! updated [script](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/power_analysis/pa2.py)


## SRA (400 points)
-----------------------------------------------------


![](/https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/sra/sra.png)

Downloading the provided script in the challenge descriptin we found out that it's a classic RSA challenge, but this time around we are given our key `d` (envy) and public exponent `e`(sloth), this the script:

```
pride = "".join(choice(ascii_letters + digits) for _ in range(16))

gluttony = getPrime(128) #p
greed = getPrime(128)   #q
lust = gluttony * greed # n
sloth = 65537 # e
phi = (gluttony - 1) * (greed - 1)
envy = inverse(sloth, phi)

)
print(envy * sloth % phi)

anger = pow(bytes_to_long(pride.encode()), sloth, lust)

print(lust)
print(f"{anger = }")
print(f"{envy = }")



print("vainglory?")
vainglory = input("> ").strip()

if vainglory == pride:
    print("Conquered!")
    with open("/challenge/flag.txt") as f:
        print(f.read())
else:
    print("Hubris!")

```
let's break down the code

-    The first line generates a random string of 16 characters called "pride" by selecting a random character from the set of ASCII letters and digits 16 times.
-   The next three lines generate two random prime numbers of 128 bits each and store them in variables "gluttony" and "greed". The product of these two primes is stored in a variable called "lust".
-    The variable "sloth" is set to the value 65537, which is a commonly used value for the encryption exponent in RSA.
-    The variable "phi" is set to the value (gluttony-1) * (greed-1), which is used to calculate the decryption exponent.
-    The variable "envy" is set to the modular inverse of sloth modulo phi, which is the decryption exponent.
-    The next line prints the value of sloth times envy modulo phi, which should be equal to 1 if the calculation of the decryption exponent was correct.
-    The variable "anger" is set to the result of raising the encoded bytes of the "pride" string to the power of sloth modulo lust, which is the ciphertext.
-    The next three lines print the value of the prime number lust, the ciphertext anger, and the decryption exponent envy.
-    The program then prompts the user to input a string called "vainglory" and compares it to the "pride" string generated at the beginning.
-    If the input string matches "pride", the program prints "Conquered!" and reads and prints the contents of a flag file.
-    If the input string does not match "pride", the program prints "Hubris!".

### **Finding our `N`**
------------------------------------

our method of finding the possible vaule of `N` is by finding all the factors of ```d*e-1``` then compute all possible combinations such that the product of all this combination summed with 1 would give us our `N`, this our attack script:

```

fac = [a for a, b in list(factor(d*e-1)) for _ in range(b)]
for r in range(2, len(ffac)):
    for i in combinations(fac, r):
        p = product(i) + 1
        if p.nbits() != 128 or not is_prime(p):
            continue
        m = long_to_bytes(int(pow(c, d, int(p))))
```

full script [here](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/sra/sra_sol.py)
Note:  to run this script you need [Sage Math](https://doc.sagemath.org/html/en/installation/index.html)

The script iterates through all possible combinations of factors in "fac" and checks if the resulting number is a prime of 128 bits. If it is not, the script continues with the next combination. If it is a 128-bit prime, the script derives the plaintext message by raising the ciphertext "c" to the power of "d" modulo "p" and converting the resulting integer to bytes using the "long_to_bytes" function from the "Crypto.Util.number" library.

opening our dockerized sage math 
![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/sra/sage_docker.png)

running the script for some secs (it's really fast,about 2 secs), sage throws us back our flag

![](https://raw.githubusercontent.com/Cyberguru1/nokkers/master/posts/files/sra/sage_result.png)



## Remarks and Cretdits
-------------------------------------


I wanted to express my appreciation to PicoCTF team for the challenges you designed for the recent CTF event. They were incredibly well-crafted and challenging, and they helped me improve my reasoning and technical skills. Your challenges pushed me out of my comfort zone and forced me to think creatively and critically, which I believe is the essence of a good CTF challenge. I found the variety of topics and difficulty levels to be well-balanced, and the hints provided were helpful without giving too much away. Overall, I thoroughly enjoyed the experience and felt like I learned a lot from the challenges. Thank you for your hard work and dedication to creating such an excellent event.


## Remainning Solutions
-----------------------------



My amazing team mates [blackAnon](https://github.com/BlackAnon22)  solved the other categories of the challenges
take a look [here](https://github.com/BlackAnon22/BlackAnon22.github.io/blob/main/posts/CTF%20Competitions/picoCTF_2023.md)
and [CyberMMA](https://medium.com/@cybermma0/ctf-writeup-picoctf-2023-99ea5d0e28bc)