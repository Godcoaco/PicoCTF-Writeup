# 🔐 picoCTF WriteUp – MacroHard WeakEdge

<!-- this one is really test your detective skills... maybe i will try grep hidden as another keyword next times >;3-->
![Category](https://img.shields.io/badge/category-forensics-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
they give us the powerpoint file! this one is rare and unique one

### *Short .ppt explain
.ppt is a Microsoft PowerPoint presentation file format. It stores slides with text, images, and media, and in forensics or CTFs it may hide metadata or embedded files And it also actually similar to zip file!

---

## 🛠️ Steps to Solve
1. Because the powerpoint is actually similar to the zip file we can see what inside first with the binwalk
   <br>
   ```
   binwalk -e 'Forensics is fun.pptm'
   ```
   <br>
2. just then my eyes catch the lastest path they show in binwalk that look very suspicious
   <br>
   ```
   88548         0x159E4         Zip archive data, at least v2.0 to extract, compressed size: 81, uncompressed size: 99, name: ppt/slideMasters/hidden
   ```
   <br>
   hidden? I mean what kind of file name "hidden" bro
3. after we see what shout we go and check let extract it out with 7z
   <br>
   ```
   7z e 'Forensics is fun.pptm' 
   ```
   <br>
4. After that I go straight to the hidden file (we already know the path where it is from binwalk 'ppt/slideMasters/hidden')
5. after that you got the base 64 ```Z m x h Z z o g c G l j b 0 N U R n t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q```
6. so for easiler I just copy it and get the ' ' out
   <br>
   ```
   echo 'Z m x h Z z o g c G l j b 0 N U R n t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q' | tr -d ' '
   ->ZmxhZzogcGljb0NURntEMWRfdV9rbjB3X3BwdHNfcl96MXA1fQ
   ```
   <br>
   
7. Throw it in CyberChef
---
    
### Here your flag : ```picoCTF{D1d_u_kn0w_ppts_r_z1p5}```

---

### 💻 Tool/Command Used
#### CyberChef
CyberChef is a web-based tool for analyzing and transforming data. It’s commonly used in CTFs to decode, decrypt, convert formats, and quickly test different data operations without writing code.
#### 7z
7z is a compressed archive file format used by 7-Zip. It offers high compression ratios and is commonly seen in CTFs to bundle files or hide data inside archives.
#### binwalk
Binwalk is a firmware and file analysis tool used to detect and extract embedded files from binaries. In CTFs, it’s commonly used to find hidden files, compressed data, or file signatures inside images, firmware, or unknown binaries.
