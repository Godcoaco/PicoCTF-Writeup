# 🔐 picoCTF WriteUp – plumbing

<!-- ez peasy after learn basic linux >;3-->
![Category](https://img.shields.io/badge/category-general_skills-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
they give us netcat that when we run will result with long text

### *Short netcat explain
Netcat (nc) is a simple networking tool used to read and write data over TCP or UDP connections. In CTFs, it’s commonly used to connect to remote challenge servers, listen for incoming connections, transfer files, or spawn a shell.

---

## 🛠️ Steps to Solve
1. run the instance
2. they will give you something like fickle-tempest.picoctf.net xxxxx you can run it by put ```nc``` in the front
3. when you run it in terminal they will give us alot of text so let out it in file.txt
   <br>
   ```
   nc fickle-tempest.picoctf.net xxxxx > file.txt
   ```
   <br>
4. after we get the text file we can try grep from it
   <br>
   ```
   grep file-txt -i pico
   ```
   <br>
5. The flag reveal!

---
    
### Here your flag : ```picoCTF{digital_plumb3r_1eBfC512}```

---
