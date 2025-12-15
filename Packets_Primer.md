# 🔐 picoCTF WriteUp – Packets Primer

<!-- silly comment as the easter eggs >;3-->
![Category](https://img.shields.io/badge/category-forensics-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
they give us pcap file so we find the flag in it

### *Short Pcap explain
A PCAP file stores captured network packets from a network interface.
It’s used with tools like Wireshark to analyze network traffic, inspect protocols, detect attacks, or solve forensics challenges in CTFs.

---

## 🛠️ Steps to Solve
1. the first thing you can try to deal with pcap file is strings grep because sometime we dont even have to open wireshark
2. let try strings it
   <br>
   ```
    strings network-dump.flag.pcap 
   ```
   <br>
3. oh...
   <br>
   ```
    p i c o C T F { p 4 c k 3 7 _ 5 h 4 r k _ b 9 d 5 3 7 6 5 }
   ```
   <br>
4. when you find some flag like this you can also do this to make it look normal
   <br>
   ```
   echo 'p i c o C T F { p 4 c k 3 7 _ 5 h 4 r k _ b 9 d 5 3 7 6 5 }' | tr -d ' '
   ```
   <br>
---
    
### Here your flag : ```picoCTF{p4ck37_5h4rk_b9d53765}```

---

### 💻 Tool/Command Used
#### tr 
tr is a Unix command used to translate, replace, or delete characters from input text. It’s commonly used to change case, remove characters, or substitute one character set for another in a text stream.
