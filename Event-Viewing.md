# 🔐 picoCTF WriteUp – Event-Viewing

<!-- If anyone have trick to find the right event-id please contact me I will be very greatful >;3-->
![Category](https://img.shields.io/badge/category-forensics-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
they give us the window log file and tell us the flag part is in these event
1. install the software installer
2. after they run the installer nothing happen
3. the computer keep shutting down everytime they boot up

### *Short Window log file explain
A Windows log file is a record of system, security, and application events that Windows stores for troubleshooting and monitoring.

---

## 🛠️ Steps to Solve
1. Base on the file that already told us it the window log file so im doing this in window
2. after open it in window we will open it in the app call event viewer
3. here you can filter the log with specific id for each event to find the flag (this was the hardest part for me so i just asking llm for possible id)
4. at the right side you will see the filter mode and there you can include the event id for each event then you will find part of the flag
   <br>
   ```
   Installation : 1033
   Registry Change : 4657
   Shutdown : 1074
   ```
   * Registry change mean the program is install something to computer and because casue problem happen after we run so we can try this one
   <br>
5. after you find each part it gonna give you 3 flags part
   <br>
   ```
   cGljb0NURntFdjNudF92aTN3djNyXw==
   MXNfYV9wcjN0dHlfdXMzZnVsXw==
   dDAwbF84MWJhM2ZlOX0=
   ```
   <br>
6. Then we can drop those in cyberchef then the flag gonna come out
### Extra
you can also do this in linux by convert the file into .json and open it in vscode then search for the event. or just = and ==

---
    
### Here your flag : ```picoCTF{Ev3nt_vi3wv3r_1s_a_pr3tty_us3ful_t00l_81ba3fe9}```

---

### 💻 Tool Used
#### CyberChef
CyberChef is a web tool that lets you easily encode, decode, convert, and analyze data using drag-and-drop operations.
#### Event-Viewer
Event Viewer is a Windows tool that shows system, application, and security logs so you can check errors, warnings, and other events.
