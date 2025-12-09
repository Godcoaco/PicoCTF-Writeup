# 🔐 picoCTF WriteUp – Dear Diary

<!-- This one is solve by look at other write up cuz there no way i gonna find this by myself so i recommand look it up cause i dont plan to include any picture. Sorry >;3-->
![Category](https://img.shields.io/badge/category-forensics-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
They give us disk file and this time we using autopsy

### *Short disk explain
A disk is a storage device that saves data like files, programs, and the operating system so the computer can read and use them.

---

## 🛠️ Steps to Solve
1. they give us the zip that have disk file inside and after extract it out we will be using autopsy to look into this thing (the description also mention case)
2. in kali we can use this command and go to the local host they give us to access the autopsy
   <br>
   ```
   sudo autopsy
   ```
   <br>
4. after we in autopsy just click new case and give it a name then click on newcase
5. then add host. we can just click addhost stright away dont have to change anything
6. after that we can add imagefile by give them the path of our image like mine is
   <br>
   ```
   /home/kali/Downloads/disk.flag.img
   ```
   <br>
7. after that we can analyze the raw file to find some keyword by using *keyword serch*
8. I try to find the *pico* but it didnt work so I find *.txt* and look at their ASCII one by one
9. then I saw the piece of flag in one of them as *pic* and the one next to it is *oCT* so I place it one by one in the textediter untill it end with } theb try it out
10. And it correct!

---
    
### Here your flag : ```picoCTF{1_533_n4m35_80d24b30}```

---

### 💻 Tool Used
#### Autopsy
Autopsy is a digital forensics tool that lets you analyze disks, files, and system artifacts through a graphical interface to find evidence or recover data.
