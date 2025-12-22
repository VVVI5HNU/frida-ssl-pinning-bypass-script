# mobile-ssl-pinning-bypass

> ⚠️ **Legal & Ethical Notice**  
> This repository contains a Frida-based security testing script intended **ONLY** for authorized mobile application VAPT assessments and controlled lab environments.  
> Do **NOT** use this script on applications or devices without explicit written permission.

---

## 📌 Overview

`mobile-ssl-pinning-bypass` is a Frida-powered toolkit used during authorized Android mobile application penetration testing (VAPT).  
It helps security testers analyze and bypass SSL/TLS certificate pinning to evaluate how applications validate certificates during secure communication.

---

## ⚙️ Prerequisites

### **Host Machine (Kali/Linux/macOS):**
- `adb` installed  
- `frida-tools` installed (`pip install frida-tools`)  
- Matching `frida-server` binary for your Android device architecture  

### **Android Device:**
- Developer Options enabled  
- USB Debugging enabled  
- Wireless Debugging enabled (optional but recommended)  
- Root access preferred (or use emulator / Frida Gadget)

---

## 📱 Step 1 — Enable Wireless Debugging on Android

On your Android device:

1. Go to **Settings → About phone**  
2. Tap **Build number** 7 times  
3. Go to **Settings → Developer Options**  
4. Enable:  
   - **USB Debugging**  
   - **Wireless Debugging**
5. In Kali install adb (sudo apt install adb)

---

## 💻 Step 2 — Connect Device from Kali/Linux

### Pair the device:
```
adb pair <DEVICE_IP>:<PAIRING_PORT>
```

Enter the pairing code displayed on the device.

### Connect to the device:
```
adb connect <DEVICE_IP>:<ADB_PORT>
```

### Open an ADB shell:
```
adb shell
```

### Gain root access (if available):
```
su
```

### Start Frida server:
```
/data/local/tmp/frida-server
```

---

## 🧪 Step 3 — Run Frida Commands (from another terminal)

### List all running apps:
```
frida-ps -aU
```
Copy the app identifier (package name).

### Start Frida with the SSL pinning bypass script: (Download [sslpin.js](https://github.com/VVVI5HNU/frida-ssl-pinning-bypass-script/blob/main/sslpin.js) script)
```
frida -U -f <APP_ID> -l sslpin.js
```

---

## 🛠 Troubleshooting Guide

### 📌 sometimes it shows “Connected to Wi-Fi but No Internet”
This issue occurs when traffic redirection rules are active on the device.

Use the following commands:

```
iptables -t nat -A OUTPUT -p tcp --dport 80 -j DNAT --to-destination <IP>:<port>
iptables -t nat -A OUTPUT -p tcp --dport 443 -j DNAT --to-destination <IP>:<port>
```

Or reset the rules from ADB shell:

```
adb shell
su
iptables -t nat -L OUTPUT -n --line-numbers
iptables -t nat -F
```

