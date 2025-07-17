# Research on V380 CCTV IP Camera

## CVE-2025-7503

 ### 🔒 Summary of Vulnerability

A commercial IP camera exposes a **Telnet service (port 23)** by default. This service is **undocumented** and accessible using **hard-coded credentials**, which grant root shell access.

This access poses serious security risks, as:
- Users are unaware of the Telnet interface.
- There is no prompt to change these credentials.
- Telnet cannot be disabled through the mobile app.

---

### 🖥️ Firmware & Software Info

- **App Version**: `AppFHE1_V1.0.6.020230803`
- **Kernel Version**: `KerFHE1_PTZ_WIFI_V3.1.1`
- **Hardware Version**: `HwFHE1_WF6_PTZ_WIFI_20201218`
- **MAC OUI**: `1C:A0:EF` (Shenzhen Liandian Communication Technology LTD)

---

### 🔎 Nmap Output

Scan showing the Telnet service (port 23) is open:

![Nmap Scan Result](nmap_scan.png)

---

### 📸 Telnet Session

Screenshot showing a successful Telnet login as **root** using default/undocumented credentials:

![Telnet Access](screenshot_telnet_login.png)

---

### 📝 Notes

- Vendor does not provide a way to disable Telnet.
- No vendor contact or security advisory page found.
- Root shell access allows complete control over the device, including filesystem, networking, and camera feeds.

---

### ⚠️ Security Impact

- **Privilege Escalation**: Immediate root access
- **Remote Code Execution**: Commands can be executed on the system
- **Backdoor Risk**: Service is undocumented, invisible to the user
- **No Fix Available**: No firmware updates or mitigations provided by vendor

---

###  Discoverer

Discovered by: **Aoun Shah**  

---

### 🔗 References
- [CVE-2025-7503](https://www.cve.org/cverecord?id=CVE-2025-7503)

---

## Plaintext wifi credentials in the filesystem

### 🔒 Summary of Vulnerability
Shenzhen Liandian Communication Technology LTD OEM IP camera (hardware id: HwFHE1_WF6_PTZ_WIFI_20201218) with firmware AppFHE1_V1.0.6.0 was discovered to store plaintext Wi-Fi credentials in the filesystem. This vulnerability allows attackers with root shell access to retrieve Wi-Fi SSIDs and passwords directly from the device’s storage.

### Details
Wi-Fi credentials are stored in `/tmp/wificonf/wpa_supplicant.conf` file on the filesystem.The contents of this file can be accessed throught linux commands in the root shell of the device.

Here is the screenshot of the file

[screenshot]


### Proof of Concept:
  Gain root shell access (e.g. through [CVE-2025-7503](https://www.cve.org/cverecord?id=CVE-2025-7503))
  Run `cat /tmp/wificonf/wpa_supplicant.conf` command
  Verify credentials being displayed

### Impact:
An attacker with root shell access can gain access to plaintext credentials. This allows the attacker to gain access to the Wi-Fi network.

---
> This report is part of responsible disclosure efforts. This information is provided for educational and defensive security purposes only.
