# 🔐 picoCTF WriteUp – hashcrack

<!-- To anyone who reading this it my first time using github for my own so please aware of bad english and messy format >;3-->
![Category](https://img.shields.io/badge/category-crypto-blue)
![Difficulty](https://img.shields.io/badge/difficulty-easy-green)
![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
They give us hash and request some password so we gonna compare then to rock.txt to get those password out

### *Short Hash explain
hash is basily the fingerprint, the dna of file. Like if you have example.txt the hash of that text might be like 'bf58e3391a9d2592beb865232353d11d5c7508f28136a58af24771b8dc4cc64e' and if you add anything into that file the hash not gonna be the same
and Hash have alot of type like Sha256, Md5, etc... so you might have to tell the command what type of hash when you dealing with them

---

## 🛠️ Steps to Solve
1. Start the Instance then they will give you command to run on terminal
2. After you run the command they will give you the hash "482c811da5d5b4bc6d497ffa98491e38" and request you to input the password
4. We can solve this by using the 'rockyou.txt' that have alot of basic password in it. You can find it direction by search bar on kali - navigate yourself to the file
5. we will compare the password by using hashcat but we still dont know the type of hash so we have to find it first
6. use ```hash-identifier``` to find you hash type and in this case it MD5
7. the hashcat require the specific number for each type of hash so we will look that up in hashcat wiki: *https://hashcat.net/wiki/doku.php?id=example_hashes*
8. after we get that number now we can run the hashcat to compare the password **Make sure you are in the rockyou.txt directory mine is ```/usr/share/wordlists```**
   ```bash
   hashcat -m 0 '482c811da5d5b4bc6d497ffa98491e38' rockyou.txt
   ```
   * -m : tell hashcat the type of hash they are dealing with<br>
   * 0 : the specific number for hash type of MD5<br>
   * '482c811da5d5b4bc6d497ffa98491e38' : hash line that they give us<br>
   * rockyou.txt : file that contain lots of basic password<br>
   * --show : this is optional. It just give you hash and the password that match immediatly<br>
10. after we type in hashcat will give us the password that match it will look something like ```482c811da5d5b4bc6d497ffa98491e38:password123``` only the one after ':' matter
11. after you paste in password it will give you another hash. We just have to do the same like before! <br>find the type of hash <br> find the number of that type <br> use ```hashcat -m [the number of that hash type] '[the hash]' rockyou.txt```
12. here the list of hash and password
    <br>
    ```
    482c811da5d5b4bc6d497ffa98491e38:password123
    b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3:letmein
    916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745:qwerty098
    ```
    <br>

---
    
### Here your flag : ```picoCTF{UseStr0nG_h@shEs_&PaSswDs!_4c95d69f}```

---

### 💻 Commands Used
```bash
hash-identifier : use to find hashtype
hashcat -m : use to compare the password with rockyou.txt
```
