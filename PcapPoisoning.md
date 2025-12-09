# 🔐 picoCTF WriteUp – MSB

<!-- This one we got lucky so we dont have to use wireshark but I recommand you to learn how to use it for next one anyway >;3-->
![Category](https://img.shields.io/badge/category-crypto-blue)
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)
![Category](https://img.shields.io/badge/category-forensics-blue)

---

## 📄 Summary
They give us .pcap file and we have to find the flag from it

### *Short pcap explain
.pcap file is a packet capture file that stores raw network traffic recorded from a network interface. Tools like Wireshark or tcpdump use it to save every packet—source, destination, protocol, timestamps—so you can analyze what happened on the network later, find flags, inspect attacks, or debug connections.

---

## 🛠️ Steps to Solve
1. they give us .pcap file so normally we will have to open it with wireshark to find the flag
2. But .pcap file can also read with string command so we can try basic grep first
   <br>
   ```
   strings trace.pcap | grep -i pico
   ```
   * string : read the file <br>
   * grep -i : only output something you mention -i make it ignore the case different <br>
4. this one is easy so the flag come off right away (maybe we just lucky but it work so....)

---
    
### Here your flag : ```picoCTF{P64P_4N4L7S1S_SU55355FUL_4624a8b6}```

---
