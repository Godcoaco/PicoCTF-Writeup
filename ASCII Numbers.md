# 🔐 picoCTF WriteUp – ASCII Numbers

<!-- Same as 13 and rotation if you know how hex look like it very easy >;3-->

![Category](https://img.shields.io/badge/category-general-lightgrey)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
They give us the bunch of hex number

### *Short Hex explain
Hex is a base-16 number system that uses digits 0–9 and letters A–F to represent values. It’s commonly used in computing to show binary data in a shorter, more readable form.

---

## 🛠️ Steps to Solve
1. they give us many lines of hex
   <br>
   ```
   0x70 0x69 0x63 0x6f 0x43 0x54 0x46 0x7b 0x34 0x35 0x63
   0x31 0x31 0x5f 0x6e 0x30 0x5f 0x71 0x75 0x33 0x35 0x37
   0x31 0x30 0x6e 0x35 0x5f 0x31 0x6c 0x6c 0x5f 0x74 0x33
   0x31 0x31 0x5f 0x79 0x33 0x5f 0x6e 0x30 0x5f 0x6c 0x31
   0x33 0x35 0x5f 0x34 0x34 0x35 0x64 0x34 0x31 0x38 0x30 0x7d
   ```
   so CyberChef will take care it once again <br>
2. open Cyberchef then drag *from hex* recipe in
3. the flag come out

---
    
### Here your flag : ```picoCTF{r0tat1on_d3crypt3d_7d140864}```

---

### 💻 Tool Used
#### Cyberchef
CyberChef is an online toolkit that lets you transform data easily. You can encode, decode, convert, search, and analyze information by stacking operations in a clear, visual way. It’s widely used for cybersecurity work and CTF challenges because it makes complex data tasks simple and fast.
