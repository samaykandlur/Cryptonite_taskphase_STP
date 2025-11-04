# **V1T CTF**

# Web Exploitation Writeup — V1T CTF

## Challenge 1: Login Panel (100 pts)

**Description:** Simple login portal, possible client-side hash verification.

### Approach
1. Inspected the page source.
2. Found a comment mentioning `sha-256`.
3. Username and password values were visible in the script:
   username = v1t
   password = p4ssw0rd
   {}

4. Used these credentials to log in.

**Flag:** `v1t{p4ssw0rd}`


---

## Challenge 2: Stylish Flag (100 pts)
 
**Description:** Challenge hinted at something hidden in the page’s style files.

### Approach
1. Inspected the `style.css` file.
2. Found a class named `.flag` containing hidden text.
3. Used the CSS code to create a small HTML file to visualize it — the flag appeared after applying transformations (rotation and zoom).

**Flag:** `v1t{h1d30ut_CSS}`


---

## Challenge 3: Tiny Flag (100 pts)

**Description:** Something hidden in the page header.

### Approach
1. Inspected the page header section.
2. Found the flag embedded in the favicon metadata or a tiny header tag.

**Flag:** `V1T{T1NY_ICO}`


---

## Challenge 4: Mark the Lyrics (100 pts)

**Description:** Challenge hinted at “marking” something in the HTML.

### Approach
1. Inspected the source code.
2. Found multiple `<mark>` tags — each containing characters of the flag.

**Flag:** `V1T{MCK-pap-cool-ooh-yeah}`
