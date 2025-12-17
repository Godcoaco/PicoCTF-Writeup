# 🔐 picoCTF WriteUp – hideme
<!-- Sadly I cant just use this in aperi'solve >;3-->
![Category](https://img.shields.io/badge/category-forensics-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
they give us the png image

### *Short png explain
PNG is a lossless image format that supports transparency. It uses compression without quality loss and is commonly used for graphics, screenshots, and CTF forensics challenges.

---

## 🛠️ Steps to Solve
1. Because It .png file. So i start with using strings, aperi solve, zsteg, binwalk and then I found this in binwalk
   <br>
   ```
   binwalk -e flag.png 

    DECIMAL       HEXADECIMAL     DESCRIPTION
    --------------------------------------------------------------------------------
    41            0x29            Zlib compressed data, compressed
    39739         0x9B3B          Zip archive data, at least v1.0 to extract, name: secret/
    39804         0x9B7C          Zip archive data, at least v2.0 to extract, compressed size: 2869, uncompressed size: 3024, name: secret/flag.png

    WARNING: One or more files failed to extract: either no utility was found or it's unimplemented
   ```
   <br>
2. from binwalk we can see it actuallyzip inside this png file so let extect them out with 7z
   <br>
   ```
   7z e flag.png
   ```
   <br>
   
3. we can see there a flag.png inside the extracted directory
   <br>
   ```
    ┌──(kali㉿kali)-[~/Downloads]
    └─$ cd _flag.png.extracted
                                                                                                                                                                                                                                            
    ┌──(kali㉿kali)-[~/Downloads/_flag.png.extracted]
    └─$ tree
    .
    ├── 29
    ├── 29.zlib
    ├── 9B3B.zip
    └── secret
        └── flag.png

   ```
4. The flag.png inside is the picture of the flag

---
    
### Here your flag : ```picoCTF{Hiddinng_An_imag3_within_@n_ima9e_cda72af0}```

---

### 💻 Tool Used
#### 7z
7z is a compressed archive file format used by 7-Zip. It offers high compression ratios and is commonly seen in CTFs to bundle files or hide data inside archives.
#### binwalk
Binwalk is a firmware and file analysis tool used to detect and extract embedded files from binaries. In CTFs, it’s commonly used to find hidden files, compressed data, or file signatures inside images, firmware, or unknown binaries.
