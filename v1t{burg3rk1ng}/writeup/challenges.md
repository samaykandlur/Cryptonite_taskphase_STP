# **V1T CTF**

# Web Exploitation Writeup — V1T CTF

## Challenge 1: Login Panel (100 pts)

**Category:** Web  
**Description:** Simple login portal, possible client-side hash verification.

### Approach
1. Inspected the page source.
2. Found a comment mentioning `sha-256`.
3. Username and password values were visible in the script:
   username = v1t
   password = p4ssw0rd
   {}

