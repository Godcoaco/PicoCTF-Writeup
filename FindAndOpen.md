# 🔐 picoCTF WriteUp – FindAndOpen

<!-- I dont even relize that thing is the key in the first time >;3-->
![Category](https://img.shields.io/badge/category-forensics-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
they give us the flag file that need the password to read and the .pcap file that have the key inside it

### *Short Advice
when it come to password finding like this you can try as many time as you want to make sure yuo dont just miss the password by accident

---

## 🛠️ Steps to Solve
1. Fist we have to find the key otherwise we cant open the flag
2. first I look through the wireshark first. The trick is you can sort it by length to find the odds one too! and this is what I found
   <img width="1590" height="331" alt="wireshark-capture" src="https://github.com/user-attachments/assets/4b542530-3c9b-49f4-bd8e-7a54cd719b6e" />
   <br>
   ```
   VGhpcyBpcyB0aGUgc2VjcmV0OiBwaWNvQ1RGe1IzNERJTkdfTE9LZF8=
   ```
   <br>
   The suspicious base64 isnt it? so I try throw it in cyberchef
3. after decode we got 
   <br>
   ```
   This is the secret: picoCTF{R34DING_LOKd_
   ```
   <br>
   and that the key! picoCTF{R34DING_LOKd_
4. Then we put the key into the flag file then the flag will readable

---
    
### Here your flag : ```picoCTF{R34DING_LOKd_fil56_succ3ss_cbf2ebf6}```

---

### 💻 Tool Used
#### Wireshark
Wireshark is a network protocol analyzer used to capture and inspect network traffic. It lets you view packets in detail to analyze protocols, troubleshoot networks, or solve CTF forensics challenges.
#### CyberChef
CyberChef is a web-based tool for analyzing and transforming data. It’s commonly used in CTFs to decode, decrypt, convert formats, and quickly test different data operations without writing code.
