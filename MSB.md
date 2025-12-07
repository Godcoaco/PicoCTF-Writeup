# 🔐 picoCTF WriteUp – MSB

<!-- This is not the easy one But once you know the tool it very easy! I did this with Fujatyping and make this writeup right away >;3-->
![Category](https://img.shields.io/badge/category-crypto-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Category](https://img.shields.io/badge/category-forensics-blue)

---

## 📄 Summary
They give us the encoded png file that have something to do with visual artifacts while they talking about LSB in the description

### *Short LSB/MSB explain
A pixel is made of numbers (like R-G-B values). Each number has 8 bits.
LSB (Least Significant Bit) means the tiny bit at the end. changing it barely affects the color, so people hide secret data in LSBs because the image still looks normal.
MSB (Most Significant Bit) means the big, important bit at the front. changing MSBs heavily changes the color, so if someone modifies or removes MSBs, the image becomes bright, noisy, or corrupted-looking.
So:
LSB → good for hiding data (image still looks normal).
MSB → if modified, image becomes crazy colors/glitchy.

---

## 🛠️ Steps to Solve
1. they give us the png picture that look like it broke something like "colored static" and they did mention MSB in the title, LSB in the description
2. Im using StegOnline *https://georgeom.net/StegOnline/upload* To solve this one
3. Upload the picture and click 'extrack file/Data'
4. I check on all three rgb on 7 pixels and ascii look readable so I download it
5. the file will come in .dat so you have to read them with strings on terminal
   <br>
   ```
   strings Ninja-and-Prince-Genji-Ukiyoe-Utagawa-Kunisada.dat
   ```
   * strings : read the file in readable term (if it possible) <br>
6. We can see that there a long paragrap of readable text so I just try grep the flag
   <br>
   ```
   strings Ninja-and-Prince-Genji-Ukiyoe-Utagawa-Kunisada.dat | grep -i pico
   ```
   * grep -i : only output something you mention -i make it ignore the case different <br>
7. And then we got Flag just like that!

---
    
### Here your flag : ```picoCTF{15_y0ur_que57_qu1x071c_0r_h3r01c_ea7deb4c}```

---

### 💻 Tool Used
#### StegOnline
StegOnline is a website that lets you quickly check images for hidden data. You upload a picture, and it shows LSB layers, color channels, and bit-planes so you can see if anything is secretly hidden inside.
