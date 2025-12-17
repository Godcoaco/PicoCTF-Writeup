# 🔐 picoCTF WriteUp – Lookey here

<!-- aight bro how th is this medium >;3-->
![Category](https://img.shields.io/badge/category-forensics-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
They give us the text file... a really long one

---

## 🛠️ Steps to Solve
1. just grep it man 😔🤘
   <br>
   ```
   strings anthem.flag.txt| grep -i pico
   -> we think that the men of picoCTF{gr3p_15_@w3s0m3_4c479940}
   ```
   <br>

---
    
### Here your flag : ```picoCTF{gr3p_15_@w3s0m3_4c479940}```

---

### 💻 Command Used
#### grep
grep is a command-line tool used to search for text patterns in files or input. It’s commonly used to quickly find keywords, flags, or specific strings using plain text or regular expressions.
