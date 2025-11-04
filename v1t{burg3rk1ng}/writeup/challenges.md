# **V1T CTF**

# Web Exploitation Writeup

## Challenge 1: Login Panel (100 pts)

**Description:**
> login - [challenge link](https://tommytheduck.github.io/login)

### Approach
1. Inspected the page source.
2. Found a comment mentioning `sha-256`.
3. Username and password values were visible in the script:
      ```
      const ajnsdjkamsf = 'ba773c013e5c07e8831bdb2f1cee06f349ea1da550ef4766f5e7f7ec842d836e'; // replace
      const lanfffiewnu = '48d2a5bbcf422ccd1b69e2a82fb90bafb52384953e77e304bef856084be052b6'; // replace
      ```

4. username = v1t, password = p4ssw0rd
5.  Used these credentials to log in.

![img](v1t{burg3rk1ng}/writeup/images/loginpanel.png)

**Flag:** `v1t{p4ssw0rd}`


---

## Challenge 2: Stylish Flag (100 pts)
 
**Description:**
> Are you a front end dev ? [challenge link](https://tommytheduck.github.io/stylish_flag/)

### Approach
1. Inspected the `csss.css` file.
2. Found a class named `.flag` containing hidden text.
```
 .flag {
        width: 8px;
        height: 8px;
        background: #0f0;
        transform: rotate(180deg);
        opacity: 0.05;
        box-shadow:
            264px 0px #0f0,
            1200px 0px #0f0,
            .
            .
            .
            1192px 64px #0f0,
            1200px 64px #0f0;
    }
```
4. Used the CSS code to create a small HTML file to visualize it — the flag appeared after applying transformations (rotation and zoom). [Check out the code](v1t{burg3rk1ng}/writeup/additional/stylishflag.html)

![img](v1t{burg3rk1ng}/writeup/images/stylishflag.png)

**Flag:** `v1t{h1d30ut_CSS}`


---

## Challenge 3: Tiny Flag (100 pts)

**Description:**
> Do you see the tiny flag :> [challenge link](https://tommytheduck.github.io/tiny_flag)

### Approach
1. Looked at the header icon, and it looked different compared to the other challenge sites. 
2. Inspected the page header section.
3. Found the flag embedded in the favicon [check this out](https://tommytheduck.github.io/tiny_flag/favicon.ico)
   
![img](v1t{burg3rk1ng}/writeup/images/tinyflag.png)

**Flag:** `V1T{T1NY_ICO}`


---

## Challenge 4: Mark the Lyrics (100 pts)

**Description:**
> Challenge hinted at “marking” something in the HTML.

### Approach
1. Inspected the source code.
2. Found multiple `<mark>` tags — each containing characters of the flag.

![img](v1t{burg3rk1ng}/writeup/images/markthelyrics.png)

**Flag:** `V1T{MCK-pap-cool-ooh-yeah}`

---

## Challenge 5: 5571 (100 pts)

**Description:**
> My friend got highest mark with this challenge, can you beat it :> [challenge link](http://chall.v1t.site:30300/)

### Approach
1. Tried SSTI (server side template injection, $7*7), SQLI (injection), XSS (cross side scripting)
2. Trying...

**Flag:** `--`




# Reverse Engineering Writeup

## Challenge 2: Snail Delivery (100 pts)

**Description:**
> Enter your flag and the snail will deliver it to headquarters for verification. But be careful - it moves slowly!

### Approach
1. Used Ghidra to view 


---

## Challenge 2: Snail Delivery (100 pts)

**Description:**

### Approach

---

## Challenge 3: Duck RPG (100 pts)

**Description:**

### Approach

---

## Challenge 5: Bad Reverser (100 pts)

**Description:**

### Approach

---

# Cryptography

## Challenge 4: Misconfigured RSA (100 pts)

**Description:**

### Approach
1. Used the standard n, e, c values.
2. n is the product of two large, distinct prime numbers, e is the public exponent (key), and c is the ciphertext.
```
n = 148900953097814724338206947679223698832179691968218755697733749707084556942286184505525791780949441847197006147827388400754499224336852575956050210608024912280019773833889546324355353746095214275985515374968532505153145975517881297436944244066461866248895871696012367810254055557824874852294865749524482337551
e = 65537
c = 107217087223013352864419426588613439434708031699522027786711684217439431898186052583896596846379575153070982123347045493427454234913154021933229641985591412104222934496019950746514726800406326146713516918611779367873873294259462206805554572977819244626333164240237423211396727885901436510649294574529712562954
```
3. Substituting the values in [dcode](https://www.dcode.fr/rsa-cipher), the flag was obtained

**Flag:** `v1t{f3rm4t_l1ttl3_duck}`

---

# Osint Writeup

## Challenge 1: Among USniversity (100 pts)

**Description:** 
> Bro, I found "Among Us" at this school!
> Can you spot the hidden acronym?
> Wrap it in v1t{...} to submit your answer.

### Approach
1. Performed reverse-image searches (Google).
2. Matched image to a university page/profile which contained a short identifier matching the challenge hint.
3. Used the acronym UIT
   
**Flag:** `v1t{UIT}`


---

## Challenge 2: Dusk Till Duck (100 pts)

**Description:**
> As the sun sets over a calm lake, a lone duck drifts across the fading light. The scene looks peaceful, but the park hides more than it seems. Can you figure out where this photo was taken before the night falls?

### Approach
1. Performed reverse-image searches (Google).
2. Found [shutterstock](https://www.shutterstock.com/id/image-photo/stunning-evening-view-swimming-ducks-thames-1781586122).
3. The author of that has a canadian flag on his instagram account.
4. Checked out "Parks on Thames River, Canada"
5. Found Ivey Park and other parks.
6. Tried them one by one.

**Flag:** `{Ivey_Park}`


---


## Challenge 3: Forgotten Inventory (100 pts)

**Description:**
> In the summer of 2007, a massive archive quietly surfaced — a meticulous ledger of items that once rolled across desert sands under foreign command. The file was structured, line after line, page after page, each entry tied to a unit whose banners flew far from home.
> Someone wasn’t happy about its release. A message was sent, demanding its silence — a digital plea from a uniformed gatekeeper. The request was denied.
> Your task is to uncover the sender of that plea.
> Clues hide in old public archives — look for a tabular trail documenting what was once called Operation Freedom, catalogued in a comma-separated vault of** 1,996 pages** worth of equipment.
> Some say the sands between two nations hold the real context — where east met west, and war turned into a spreadsheet.
> Find the **email address** of the official who tried to bury the list.

### Approach
1. Keywords: 2007, archive, east met west.
2. Found [wikileaks](https://wikileaks.org/wiki/Iraq_OIF_Property_List.csv) while searching

![img](v1t{burg3rk1ng}/writeup/images/forgotteninv.png)

**Flag:** `v1t{david.j.hoskins@us.army.mil}`

---

## Challenge 4: Duck Company (100 pts)

**Description:**
> I found this company selling this cute wooden duck for the halloween but i forgot where link web store :< can you help me find it

### Approach
1. Ran reverse-image search.
2. Identified a company landing page and domain referenced in the matching results.
3. Confirmed domain name.

**Flag:** `v1t{dcuk.com}`


---

## Challenge 5: 16th Duck (100 pts)

**Description:**
> Caught someone playing music at this place and here are their belonging, can you find the place? Flag format: v1t{latitude, longitude}

### Approach
1. Reverse searched the image.
2. Found a match showing:
> "OSINT & Phaleristics: Unveiling FSB 16th Center SIGINT Capabilities".
[img]()
3. Extracted coordinates from the matched page.



**Flag:** `v1t{55.592169,37.689097}`

---


# Misc Writeup

## Challenge 4: Blank (100 pts)

**Description:** 
> This image is blank is it?

### Approach
1. Used [Principal Component Analysis](https://29a.ch/photo-forensics/#pca) on the image

![img](v1t{burg3rk1ng}/writeup/images/blank.png)

**Flag:** `v1t{wh1t3_3y3s}`

---

## Challenge 4: Polyglot (100 pts)

**Description:** 
> Look, read, and most importantly, WATCH the duck!
> File can only open in Windows

### Approach
1. Checked for strings and found:
```
There no flag here brother<!--
%PDF-1.7
<</Length 2224897>>
stream
isomiso2avc1mp41
 ftypisom
isomiso2avc1mp41
.
.
.
Create videos with https://clipchamp.com/en/video-editor - free online video editor, video compressor, video converter.
tskip--><style>body{font-size:0}</style><div style=font-size:initial><!DOCTYPE html>
<html lang="en">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>V1t CTF 2025</title>
    <p>Bro you need to be more patient just WATCH the whole thing</p>
</div>
.
.
.
```
2. Changed file name from `polyglot.png` to `polyglot.pdf`, `polyglot.html` and `polyglot.mp4`
3. Found details in all of them, pdf and html were useless. mp4 had a password `HideTheDuck123@`
4. binwalk the png file and extracted `angri.jpg`
5. Used steghide on `angri.jpg` with pass: HideTheDuck123@
```
steghide extract -sf angri.jpg -p HideTheDuck123@
```
6. Got flag.txt
```
cat flag.txt
v1t{duck_l0v3_w4tch1ng_p2r3}
```

**Flag:** `v1t{duck_l0v3_w4tch1ng_p2r3}`
