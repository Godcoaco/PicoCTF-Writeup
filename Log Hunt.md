# 🔐 picoCTF WriteUp – Log Hunt

<!-- This is a very easy one too >;3-->
![Category](https://img.shields.io/badge/category-general_skills-blue)
![Difficulty](https://img.shields.io/badge/difficulty-easy-green)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
They give us the log file so we find the flag in it

### *Short log explain
A log is a record of system or application events used to track activity, errors, and changes for troubleshooting or investigation.

---

## 🛠️ Steps to Solve
1. they give us the log file so we can just open it with text editer
2. we can see right away that there are
   <br>
   ```
   [1990-08-09 10:00:10] INFO FLAGPART: picoCTF{us3_
   ```
   on the very first line
   <br>
3. So we can just look through it and collect the part then the flag will come out! I will use grep tho i lazy scrolling
   <br>
   ```
   strings server.log | grep -i Flag
   ```
   * strings : output the file in readable text if possible <br>
   * grep -i : Show only the part that contain Flag -i make them ignore case sensitive
4. assemble the flag!

---
    
### Here your flag : ```picoCTF{us3_y0urlinux_sk1lls_cedfa5fb}```

---
