# mobile-ssl-pinning-bypass

> ⚠️ **Legal & Ethical Notice**  
> This repository contains a Frida-based security testing script intended **ONLY** for authorized mobile application VAPT assessments and controlled lab environments.  
> Do **NOT** use this script on applications or devices without explicit written permission.

---

## 📌 Overview

`mobile-ssl-pinning-bypass` is a Frida-powered toolkit used during authorized Android mobile application penetration testing (VAPT).  
It helps security testers analyze and bypass SSL/TLS certificate pinning to evaluate how applications validate certificates during secure communication.

The purpose of this project is strictly:
- For security testers  
- For authorized VAPT engagements  
- For controlled lab use  
- For research and learning  

---

## 📁 Repository Structure

```
/ (repo root)
├── scripts/
│   └── frida_multiple_unpinning.js
├── README.md
├── USAGE.md
├── SECURITY.md
├── CONTRIBUTING.md
├── LICENSE
└── .gitignore
```

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

### Start Frida with the SSL pinning bypass script: (Download [sslpin.js](https://your-url-here.com)
 script)
```
frida -U -f <APP_ID> -l sslpin.js
```

---

## 🧵 Beginner Notes

- Ensure `frida` and `frida-server` versions **match**  
- If the app crashes on spawn, try attaching instead  
- Use a dedicated test device or emulator  
- Ensure proxy/CA certificate is correctly installed if intercepting traffic  

---

## 🛠 Troubleshooting Guide

| Problem | Explanation | Solution |
|--------|-------------|----------|
| `Failed to spawn app` | App blocks injection | Use `-n <PROCESS_NAME>` attach mode |
| `Unexpected EOF` | Wrong frida-server version | Download correct architecture |
| No script logs | Script not loaded | Check file path and extension |
| Device not detected | ADB not connected | Run `adb devices` and reconnect |

---

## 📝 Security Policy

This project is for **authorized** security testing only.  
Read `SECURITY.md` for disclosure guidelines.

---

## 🔧 Contributions

See `CONTRIBUTING.md` to follow contribution guidelines and ethical rules.

---

## 📜 License

Licensed under the **MIT License**.  
See the `LICENSE` file for details.

---

## 🙏 Credits

Original SSL bypass script authored by **Maurizio Siddu**.  
Documentation and structuring adapted for VAPT workflows.

---

# ✔️ End of README.md
