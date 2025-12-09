# 🔐 picoCTF WriteUp – rotation
<!-- Same as 13 if you know how rot look like it very easy >;3-->
![Category](https://img.shields.io/badge/category-crypto-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
They give us the text file that have weird line inside that look like rot

### *Short Rot explain
ROT is a simple letter-shifting cipher where each letter is moved forward or backward by a set number of positions in the alphabet, like ROT13 which shifts letters by 13.

---

## 🛠️ Steps to Solve
1. they give us the text file that contain ```xqkwKBN{z0bib1wv_l3kzgxb3l_7l140864}``` and it look like rot so CyberChef will talk care of it
2. open Cyberchef then drag rot13 recipe in
4. then we relize that this is not rot13 but it still look like rot so we can increase the rot amount
5. at the rot *18* the flag will reveal

---
    
### Here your flag : ```picoCTF{r0tat1on_d3crypt3d_7d140864}```

---

### 💻 Tool Used
#### Cyberchef
CyberChef is an online tool for encoding, decoding, converting, and analyzing data using a simple interface. It lets you stack operations to quickly transform information, making it useful for cybersecurity and CTF tasks.
