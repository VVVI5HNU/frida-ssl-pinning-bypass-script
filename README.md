# mobile-ssl-pinning-bypass

> ⚠️ Legal & Ethical Notice  
> This repository contains a Frida-based testing script intended **only** for authorized mobile application security assessments (VAPT) and lab experiments. Do not use these tools on systems or apps without explicit written permission.

## Overview
A Frida-powered SSL/TLS pinning bypass toolkit designed to help security testers analyze and validate SSL certificate pinning implementations in Android applications during authorized VAPT engagements. The script instruments many common pinning implementations to help observe network behavior within a controlled environment.

## Repository layout
/ (repo root)
├── scripts/
│ └── frida_multiple_unpinning.js
├── README.md
├── USAGE.md
├── SECURITY.md
├── CONTRIBUTING.md
├── LICENSE
└── .gitignore


## Quick start (high-level)
1. Prepare device and host (adb, frida).
2. Push and run `frida-server` on device.
3. Run `frida -U -f <APP_ID> -l scripts/frida_multiple_unpinning.js --no-pause`.
4. Observe Frida output for bypass logs.

See `USAGE.md` for a beginner-friendly, step-by-step walkthrough and copy-paste commands.

## Purpose & scope
This tool is for diagnostic and remediation purposes during authorized assessments. It helps testers:
- Bypass common Android SSL pinning implementations using Frida.
- Validate whether network interception (Burp, mitmproxy) is feasible post-bypass.
- Provide remediation guidance for developers.

## Responsible use
- Test in a controlled lab or with a dedicated test device.
- Back up devices and obtain written authorization.
- Follow client's disclosure policy before sharing findings.

## Credits
Original script by Maurizio Siddu. Packaged and documented for authorized VAPT use.

