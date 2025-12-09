# 🔐 picoCTF WriteUp – Bitlocker-1 

<!-- Thsi one is a bit tricky So i end up try to understand it with chatgpt >;3-->
![Category](https://img.shields.io/badge/category-forensics-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
They give us the disk that have Bitlocker so we cant just mount it like normally

### *Short bitlocker explain
BitLocker is a Windows feature that encrypts your entire drive so nobody can read the data without the correct password or recovery key. Even if someone removes the drive and plugs it into another computer, everything stays unreadable until it’s unlocked.

---

## 🛠️ Steps to Solve
1. they give us the disk file so I just mount like normally
   <br>
   ```
   mkdir mounted
   ```
   * mkdir : Make the path(folder) that we gonna mount the drive in <br>
   ```
   sudo mount -o loop bitlocker-1.dd mounted
   ```
   * mount -o loop : -o loop make the computer think the file is in computer so we can mount(something like that) and mount is like extract file<br>
   * mounted is the path I make earlier <br>
3. But then it show why we cant do that right away
   <br>
   ```
   mount: /home/kali/Downloads/test: unknown filesystem type 'BitLocker'.
   ```
   <br>
4. Bitlocker can be solve using the key, and we can get that by use the hash inside it
9. we will extract the hash with bitlocker2john right away
   <br>
   ```
   bitlocker2john -i bitlocker-1.dd
   ```
   * bitlocker2john -i : This will show path of encrypth memory unit and also incluse hash. we looking for the one that is normal password and it should start with '$bitlocker$0$'
10. after we get the hash we can use hashcat to get the password of this bitlocker. the number for bitlocker hash is 22100
   <br>
   ```
   hashcat -m 22100 '$bitlocker$0$16$cb4809fe9628471a411f8380e0f668db$1048576$12$d04d9c58eed6da010a000000$60$68156e51e53f0a01c076a32ba2b2999afffce8530fbe5d84b4c19ac71f6c79375b87d40c2d871ed2b7b5559d71ba31b6779c6f41412fd6869442d66d' /usr/share/wordlists/rockyou.txt
   ```
   * hashcat -m 22100 : tell them the type if file is bitlocker(22100) <br>
   * /usr/share/wordlists/rockyou.tx : path to the rockyou.txt (so they can compare it with our hash) <br>
11. you will get the password as *jacqueline*
12. Now that we have password we can use it with dislocker
   <br>
   ```
   mkdir dislocker
   ```
   * mkdir : Make the path(folder) that we gonna unlock the drive in <br>
   ```
   dislocker -u bitlocker-1.dd dislocker 
   ```
   * dislocker -ujacqueline : -u[password] is to unlock the file <br>
13. inside dislocker path you will left with *dislocker-file* and you can mount it again
   <br>
   ```
   sudo mount -o loop dislocker/dislocker-file mounted
   ```
   <br>
14. finally inside the /mount you will find the flag.txt

---
    
### Here your flag : ```picoCTF{us3_b3tt3r_p4ssw0rd5_pl5!_3242adb1}```

---

### 💻 Tool Used
#### bitlocker2john
bitlocker2john is a tool that extracts the BitLocker encryption data from a drive and converts it into a hash format that cracking tools like Hashcat or John the Ripper can use to try to recover the password.
### dislocker
Dislocker is a tool that lets Linux read BitLocker-encrypted drives by unlocking them and creating a decrypted file you can mount to access the data.
