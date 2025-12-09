# 🔐 picoCTF WriteUp – Mob psycho

<!-- For this one the first hint give it away 'Did you know you can unzip APK files?' >;3 -->
![Category](https://img.shields.io/badge/category-forensics-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
They give us .apk file ; That the android file you know?

### *Short .apk explain
An APK is the package file used to install apps on Android. It contains all the code, resources, and files an app needs to run, similar to an installer for Android devices.

---

## 🛠️ Steps to Solve
1. they give us the apk file so it actually really easy cause android apk is similar to zip
2. extract the file
4. you can look through the file for flag so i use the search bar and type in 'flag' and the *flag.txt* appear (you can do this one easily on window)
5. But in there it was hex '7069636f4354467b6178386d433052553676655f4e5838356c346178386d436c5f37303364643965667d' so we can just use cyberchef to deal with it
6. we drag the *from hex* recipe and the flag come out

---
    
### Here your flag : ```picoCTF{ax8mC0RU6ve_NX85l4ax8mCl_703dd9ef}```

---

### 💻 Tool Used
#### CyberChef
CyberChef is an online tool that lets you quickly encode, decode, convert, and analyze data using simple drag-and-drop operations.
