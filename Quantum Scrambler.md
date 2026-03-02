# 🔐 picoCTF WriteUp – Quantum Scrambler

<!-- This might be the last one for my first day after come back. Reverse engineer is surprisingly fun! It remind me of Toi a bit and that a good sign for my learning pace wahaha >;3 -->

<!-- CATEGORY -->
![Category](https://img.shields.io/badge/category-reverse_engineering-blue)

<!-- DIFFICULTY -->
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)

![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary

After we launch instance they will give us `nc verbal-sleep.picoctf.net xxxxx` to run on terminal that will give you alot of encoded hex thingy and also a source code of how they encoded it

### Short List(python) Explanation
we will use list alot in this. we can imagin list as the box that have thing in there if it empty box it will look like this [] there can be box inside box [[]] or manything in one box [a, b]

---

## 🛠️ Steps to Solve

1. First let look up the source code they give us (first thing to do in reverse engineer ctf)
   ```python
   import sys

   def exit():
     sys.exit(0) 

   def scramble(L):
     A = L #link A and L if anything happen to A; L also change
     i = 2
     while (i < len(A)):
       A[i-2] += A.pop(i-1) #pop mean join A[i-1] with A[i-2] like  [0x01] += [0x02] -> [0x01, 0x02]
       A[i-1].append(A[:i-2]) #[:i-2] mean from the A[start] to A[i-2]
       i += 1
    

   def get_flag():
     flag = open('flag.txt', 'r').read()
     flag = flag.strip()
     hex_flag = []
     for c in flag:
       hex_flag.append([str(hex(ord(c)))])

     return hex_flag

   def main():
     flag = get_flag()
     cypher = scramble(flag)
     print(cypher)

   if __name__ == '__main__':
     main()
   ```

    - `scramble()` — This is the most important and the one drive me crazy the most now let me explain this
    <br>- start by we will make example list as A = `[[0x01], [0x02], [0x03], [0x04], [0x05], [0x06], ...]`
    <br>- `A[i-2] += A.pop(i-1)` list will become `[[0x01, 0x02], [0x03], [0x04], [0x05], [0x06], ...]`
    <br>- `A[i-1].append(A[:i-2])` list will become `[[0x01, 0x02], [0x03, [0x01, 0x02]], [0x04], [0x05], [0x06], ...]`
    <br>- then `i=3`
    <br>- `A[i-2] += A.pop(i-1)` list will become `[[0x01, 0x02], [0x03, [0x01, 0x02], 0x04], [0x05], [0x06], ...]`
    <br>- `A[i-1].append(A[:i-2])` list will become `[[0x01, 0x02], [0x03, [0x01, 0x02], 0x04], [0x05, [0x01, 0x02], [0x03, [0x01, 0x02], 0x04]], [0x06], ...]`
    <br>- now we can see that the first and the last box of each box are in order. that how we know how to reverse code

3. make the script to decode the hex and run it in terminal
   ```python
   code = [put the hex list they give here]
   for i in range(len(code)) :
        print(code[i][0], code[i][-1], end=" ")
   ```
4. in the front you will get thing as the clear hex line (no one get the same)
5. use from hex in cyberchef ; mine is
   ```
   hex: 0x70 0x69 0x63 0x6f 0x43 0x54 0x46 0x7b 0x70 0x79 0x74 0x68 0x6f 0x6e 0x5f 0x69 0x73 0x5f 0x77 0x65 0x69 0x72 0x64 0x62 0x30 0x63 0x62 0x36 0x62 0x65 0x31
   to: picoCTF{python_is_weirdb0cb6be1
   ```
   <br> then we just have to add `}` after the flag
### 🚩 Flag
*not the same to anyone
```
picoCTF{python_is_weirdb0cb6be1}
```

---

## 💻 Tools / Commands Used

### Cyberchef
CyberChef is a free, browser-based tool made by GCHQ that lets you encode, decode, encrypt, decrypt, and transform data using a simple drag-and-drop "recipe" system — no coding needed. It supports 300+ operations like Base64, AES, hashing, and hex conversion, making it a go-to tool for security analysts, CTF players, and developers. Everything runs locally in your browser, so your data stays private.
