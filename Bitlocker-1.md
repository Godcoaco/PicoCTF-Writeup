# 🔐 picoCTF WriteUp – Bitlocker-1

![Category](https://img.shields.io/badge/category-forensics-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary

They give us a disk that has BitLocker on it, so we can't just mount it normally.

### Short BitLocker Explanation

BitLocker is a Windows feature that encrypts your entire drive so nobody can read the data without the correct password or recovery key. Even if someone removes the drive and plugs it into another computer, everything stays unreadable until it's unlocked.

---

## 🛠️ Steps to Solve

1. They give us the disk file, so I try to mount it normally:

   ```bash
   mkdir mounted
   ```

   - `mkdir` — creates the folder we'll mount the drive into

   ```bash
   sudo mount -o loop bitlocker-1.dd mounted
   ```

   - `-o loop` — makes the computer treat the file as a block device so we can mount it
   - `mounted` — the folder we created earlier

2. But it throws an error showing why we can't do it directly:

   ```
   mount: /home/kali/Downloads/test: unknown filesystem type 'BitLocker'.
   ```

3. BitLocker can be cracked using a hash extracted from the disk. We extract it with `bitlocker2john`:

   ```bash
   bitlocker2john -i bitlocker-1.dd
   ```

   - `-i` — specifies the input disk image
   - We're looking for the hash that starts with `$bitlocker$0$` — that's the normal user password hash

4. Now we use `hashcat` to crack the password. The hash mode for BitLocker is `22100`:

   ```bash
   hashcat -m 22100 '$bitlocker$0$16$cb4809fe9628471a411f8380e0f668db$1048576$12$d04d9c58eed6da010a000000$60$68156e51e53f0a01c076a32ba2b2999afffce8530fbe5d84b4c19ac71f6c79375b87d40c2d871ed2b7b5559d71ba31b6779c6f41412fd6869442d66d' /usr/share/wordlists/rockyou.txt
   ```

   - `-m 22100` — tells hashcat the hash type is BitLocker
   - `/usr/share/wordlists/rockyou.txt` — the wordlist to compare against our hash

5. Hashcat cracks it and gives us the password: **jacqueline**

6. Now that we have the password, we use `dislocker` to decrypt the drive:

   ```bash
   mkdir dislocker
   ```

   ```bash
   dislocker -ujacqueline bitlocker-1.dd -- dislocker
   ```

   - `-u[password]` — unlocks the BitLocker drive with the given password

7. Inside the `dislocker` folder you'll find a file called `dislocker-file`. Mount it:

   ```bash
   sudo mount -o loop dislocker/dislocker-file mounted
   ```

8. Finally, inside `/mounted` you'll find `flag.txt` with the flag!

---

### 🚩 Flag

```
picoCTF{us3_b3tt3r_p4ssw0rd5_pl5!_3242adb1}
```

---

## 💻 Tools Used

### bitlocker2john
Extracts BitLocker encryption data from a drive and converts it into a hash format that cracking tools like Hashcat or John the Ripper can use to recover the password.

### hashcat
A fast password recovery tool that uses wordlists or brute-force to crack password hashes.

### dislocker
Lets Linux read BitLocker-encrypted drives by unlocking them and creating a decrypted virtual file that you can mount to access the data.
