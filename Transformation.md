# 🔐 picoCTF WriteUp – [Challenge Name]

<!-- I'm back baby. this one I learn with my new teacher claude ai and it nice(?) I guess. also the first reverse engineer ctf I done >;3 -->

<!-- CATEGORY -->
![Category](https://img.shields.io/badge/category-reverse_engineering-blue)

<!-- DIFFICULTY -->
![Difficulty](https://img.shields.io/badge/difficulty-easy-green)

![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary

They give us the text file and how they encode them. We have revease to get the original message of it
>I wonder what this really is... <br> enc ''.join([chr((ord(flag[i]) << 8) + ord(flag[i + 1])) for i in range(0, len(flag), 2)])

### Short Unicode Explanation

In this part we will play with something call unicode. for short it just the bigger table of ascii (ascii = 128 char but unicode = 1.1 million char). That mean each character have it own unicode number/order and it can write in binary.
and in python we can change any char into unicode number by using ord('char') and change it back by using chr('unicodenum')

---

## 🛠️ Steps to Solve

1. first I open the enc file that we can download and see bunch of chinese(?)
  ```
  灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸形㝦㘲捡㕽
  ```
2. So let break what they did to the encoded text by look at this

   ```python
   .join([chr((ord(flag[i]) << 8) + ord(flag[i + 1])) for i in range(0, len(flag), 2)])
   ```

   - `.join([])` — join thing together like -> `join(['a', 'b']) = 'ab'`
   - `for i in range(0, len(flag), 2)` — run from order 0 untill last flag order 2 steps at the time -> `for i in range(0, 4, 2) mean i=0 -> i=2 -> i=4 `
   - `ord(flag[i]) << 8` — the bits of flag[i] got to left side 8 bits -> `if ord(flag[i]) =  00000001 then ord(flag[i]) << 2 = 00000100`
   - `+ ord(flag[i + 1])` — after we shift flag[i] 8 bits to the left we add ord(flag[i+1])
   - that mean we make it half the orginal size cuz we join flag[i] that shift to the left 8 times and flag[i+1] to become new one character
   - `chr()` — change the bits number into unicode char

3. now we just have to reverse what they encode from the first to decode it!

   ```python
   encode = "灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸形㝦㘲捡㕽"

   flag = []

   for i in range(0, len(encode)) :
	   enc = ord(encode[i])
	   number = enc & 0xFF
	   flag.append(chr(enc >> 8))
	   flag.append(chr(number))
	
    print(flag)
   ```

   - `encode = "灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸形㝦㘲捡㕽"` — the encoded text
   - `for i in range(0, len(encode)) :` — repeat the loop from 0(start) to the end of encoded text 
   - `enc = ord(encode[i])` — get the order or first character from the encoded text
   - `number = enc & 0xFF` — the called AND mask it the bit that look like this:`00000000 11111111` so when we use `&` only the last part of the bits are left and in this case the last part of the bits is the `ord(flag[i+1])` part (the part that didn't get shift) and we going to save it in variable `number` to add it later because it in i+1 place
   - `flag.append(chr(enc >> 8))` — shift 8 bits to the right so now the first 8 bit replace the last 8 bits, the last 8 bit going to get writeover but it fine because we already save it in variable `number` and we can add it in answer list because it in the right order already `flag[i]`
   - `flag.append(chr(number))` — now we can add number to the answer last as the original it come after `flag[i]` as `flag[i+1]`
   - `print(flag)` — print what we get from the loop!

4. then we can run python on the terminal

   ```bash                                   
   python text.py
   ```
   you will get

   ```bash
   ['p', 'i', 'c', 'o', 'C', 'T', 'F', '{', '1', '6', '_', 'b', 'i', 't', 's', '_', 'i', 'n', 's', 't', '3', '4', 'd', '_', 'o', 'f', '_', '8', '_', '0', 'd', 'd', 'c', 'd', '9', '7', 'a', '}']
   ```
   

6. *Tip:we can make it easier to copy by cut out the thing between each flag charater using `tr -d "[thing between each letter]"`

   ```bash
   python text.py | tr -d "', '"
   ```

   - `tr -d` — `tr` use to tranlate or delete thing and `-d` is option to delete

---

### 🚩 Flag

```
picoCTF{16_bits_inst34d_of_8_b7f62ca5}
```

---
