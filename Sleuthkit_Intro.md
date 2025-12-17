# 🔐 picoCTF WriteUp – Sleuthkit Intro

<!-- new tool unlock! >;3-->
![Category](https://img.shields.io/badge/category-forensics-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
they give us the netcat and the disk file(in zip)

### *Short Sleuth Kit explain
The Sleuth Kit is a digital forensics toolkit used to analyze disk images and file systems. It helps examine deleted files, timelines, and file metadata, and is widely used in forensic investigations and CTFs.

---

## 🛠️ Steps to Solve
1. first we have to extract teh disk out of it zip
2. after that is pretty basic. when you run netcat they ask us the linux patition size of the disk so let find it by using mmls
   <br>
   ```
   something in command line
   ```
   <br>
3. *https://website/*
   <br>
   ```
   ┌──(kali㉿kali)-[~/Downloads]
    └─$ mmls disk.img              
    DOS Partition Table
    Offset Sector: 0
    Units are in 512-byte sectors

          Slot      Start        End          Length       Description
    000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
    001:  -------   0000000000   0000002047   0000002048   Unallocated
    002:  000:000   0000002048   0000204799   0000202752   Linux (0x83)
   ```
   <br>
   We can see that the length(size) of the linux partition is "202752"
4. after we put that in the nc we get the flag
   <br>
   ```
   nc saturn.picoctf.net 53956
   ->What is the size of the Linux partition in the given disk image?
     Length in sectors: 202752
     202752
     Great work!
     picoCTF{mm15_f7w!}
   ```
   <br>
---
    
### Here your flag : ```picoCTF{mm15_f7w!}```

---

### 💻 Tool/Command Used
#### mmls
mmls is a Sleuth Kit command used to list partition layouts in a disk image. It shows partition offsets and sizes, helping you identify where file systems start before further forensic analysis.
