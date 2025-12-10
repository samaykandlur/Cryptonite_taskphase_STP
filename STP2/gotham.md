# **Bi0sCTF**

# Digital Forensics / DIFR

## Challenge: Gotham Hustle

**Description:**
> Gotham’s underbelly trembles as whispers spread—The Riddler’s back, leaving cryptic puzzles across the city’s darkest corners. Every clue is a trap, every answer another step into madness. Think you can outsmart him? Step into Gotham’s shadows and prove it. Let the Batman's Hustle get its recognition!

---

## Approach

### Step 1: Identify OS Profile

Used Volatility to detect the operating system:

```python2 vol.py -f gotham.raw imageinfo```

![img](STP2/img/gotham/1.png)

I used the Win7SP1x64 profile for Volatility2
```OS: Windows 7 SP1 x64```

---

### Step 2: Enumerate Running Processes

```python2 vol.py -f gotham.raw –profile=Win7SP1x64 pslist```


![img](STP2/img/gotham/2.png)

Suspicious processes identified:

- `cmd.exe` (PID 3944)  
- `notepad.exe` (PID 2592)  
- `mspaint.exe` (PID 2516)  
- `DumpIt.exe` (PID 4960)  

These processes were investigated further.

---

### Step 3: Extract Console History

```python2 vol.py -f gotham.raw --profile=Win7SP1x64 consoles```

tried:

```python2 vol.py -f gotham.raw --profile=Win7SP1x64 cmdscan```

![img](STP2/img/gotham/s1.png)

I saw "did you find flag1" and the text in Cmd #4 at 0x12d690: "Ymkwc2N0Znt3M2xjMG0zXw==" looked like base64

so I decoded it 

![img](STP2/img/gotham/6.png)

and got 

Flag 1 : `biosctf{w3lc0m3_`

---

### Step 4: Dumped notepad.exe into a folder
```
mkdir dumps
python2 vol.py -f gotham.raw --profile=Win7SP1x64 memdump -p 2592 -D dumps/
```

![img](STP2/img/gotham/8.png)

then i searched for 'flag' and saw a lot of flag3 so i searched 'flag3' and copied the link I got and pasted it onto google 

[link](https://www.google.com/search?q=flag3+%3D+aDBwM190aDE1Xw%3D%3D&oq=flag3+%3D+aDBwM190aDE1Xw%3D%3D&aqs=chrome..69i57j0i512i546l2.321545j0j7&sourceid=chrome&ie=UTF-8)

![img](STP2/img/gotham/9.png)


I thought id search for 'flag' again hoping to find more flags 

```strings -el dump/2592.dmp | grep -i "flag"```

i found:
![img](STP2/img/gotham/11.png)

I both 
flag3: `aDBwM190aDE1Xw==`
flag4: `YjNuM2YxNzVfeTB1Xw==`

decoded:
flag3: `h0p3_th15_`
flag4: `b3n3f175_y0u_`

---
### Step 5: Recovering flag5.rar
I noticed multiple occurances of "flag5.rar" 

![img](STP2/img/gotham/13.png)

I found the location of it using 

```python2 vol.py -f gotham.raw --profile=Win7SP1x64 filescan | grep -i ".rar"```

![img](STP2/img/gotham/14.png)

I made a new folder, moved it there and renamed & added an extension to it:  flag5.rar

![img](STP2/img/gotham/s2.png)

---

### Step 6: Cracking the Archive Password

As you can see the rar contains flag.txt and is password protected. 

![img](STP2/img/gotham/s3.png)

The hint given is it's the computers password 


I tried using rar2john but it wasnt working so I thought Ill use hashcat.


To use hashcat I checked the user's profile's dump hashdump

```python2 vol.py -f gotham.raw --profile=Win7SP1x64 hashdump```

![img](STP2/img/gotham/15.png)

The format of the dump would be 

`username:RID:LMHASH:NTHASH:::`

By using NTLMHASH: b7265f8cc4f00b58f413076ead262720 

`echo "b7265f8cc4f00b58f413076ead262720" > bruce.hash`

and Hashcat

`hashcat -m 1000 bruce.hash ~/rockyou.txt --force`

![img](STP2/img/gotham/16.png)

I got the password as `batman`

then  `cat flag.txt` gave me `bTByM18xMzMzNzQzMX0=`

![img](STP2/img/gotham/17.png)


`echo "bTByM18xMzMzNzQzMX0=" | base64 -d` gave me `m0r3_13337431}`

Now I know that flag5 is the last part of the complete flag.

Until now we have:
flag 1 `biosctf{w3lc0m3_`
flag 2
flag 3 `h0p3_th15_`
flag 4 `b3n3f175_y0u_`
flag 5 `m0r3_13337431}`

---

### Step 7: Investigated Remaining Processes

We have checked
- `cmd.exe` (PID 3944)  
- `notepad.exe` (PID 2592)
  
Now I will be checking the other two:
- `mspaint.exe` (PID 2516)  
- `DumpIt.exe` (PID 4960)  


I dumped mspaint into a folder and used foremost to extract the images

`foremost -i out/2516.dmp -o extracted/`

I extracted images from mspaint n got all random logos and images

![img](STP2/img/gotham/18.png)

All of this was a waste.

then I tried to open the dump via GIMP

![img](STP2/img/gotham/s4.png)

---

### Step 8: Raw Memory String Search

I tried searching for 'bi0sctf' in the main gotham.raw to find anything interesting

`strings gotham.raw | grep -n "bi0sctf"`

![img](STP2/img/gotham/s5.png)

LOL I found `bi0sctf{H4Ha_N0w_Th4t_1s_Th3_Punchl1n3_0f_Th3_J0k3_1snt_1t?_2d9fe9}`

which is a flag for some other bi0s Ctf challenge

Im still trying to find flag 2.

Till now I have: `biosctf{w3lc0m3_<FLAG2>h0p3_th15_b3n3f175_y0u_m0r3_13337431}`
recovered **4 out of 5 flags**
