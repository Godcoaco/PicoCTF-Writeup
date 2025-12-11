# 🔐 picoCTF WriteUp – St3g0

<!-- Let say I know the tool for this one hehe >;3-->
![Category](https://img.shields.io/badge/category-forensics-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
They give us the suspicious png file that have something in it

### *Short Steganography explain
Steganography is the technique of hiding secret data inside normal files—like images, audio, or text—so the hidden message is not noticeable.

---

## 🛠️ Steps to Solve
1. There are many tools that we can use to find the flag when it come to steganography but this time I gonna use my all in one tools called 'Aperi'Solve'
2. Just drag the image in then It will check the picture with couple tools for us and this time we can spot the flag in *Zsteg*
   

---
    
### Here your flag : ```picoCTF{7h3r3_15_n0_5p00n_a1062667}```

---

### 💻 Tool Used
#### Aperi'Solve
Aperi'Solve is an online tool that automatically analyzes images for steganography by running many decoding techniques to reveal any hidden data.
#### Zsteg
zsteg is a command-line tool used to detect hidden data in PNG and BMP images by checking LSB, color channels, and other stego techniques.
