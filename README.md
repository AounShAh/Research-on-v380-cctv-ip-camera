# Research on V380 CCTV IP Camera

## 🔒 Summary of Vulnerability

A commercial IP camera exposes a **Telnet service (port 23)** by default. This service is **undocumented** and accessible using **hard-coded credentials**, which grant root shell access.

This access poses serious security risks, as:
- Users are unaware of the Telnet interface.
- There is no prompt to change these credentials.
- Telnet cannot be disabled through the mobile app.

---

## 🖥️ Firmware & Software Info

- **App Version**: `AppFHE1_V1.0.6.020230803`
- **Kernel Version**: `KerFHE1_PTZ_WIFI_V3.1.1`
- **Hardware Version**: `HwFHE1_WF6_PTZ_WIFI_20201218`
- **MAC OUI**: `1C:A0:EF` (Shenzhen Liandian Communication Technology LTD)

---

## 🔎 Nmap Output

Scan showing the Telnet service (port 23) is open:

![Nmap Scan Result](nmap_scan.png)

---

## 📸 Telnet Session

Screenshot showing a successful Telnet login as **root** using default/undocumented credentials:

![Telnet Access](screenshot_telnet_login.png)

---

## 📝 Notes

- Vendor does not provide a way to disable Telnet.
- No vendor contact or security advisory page found.
- Root shell access allows complete control over the device, including filesystem, networking, and camera feeds.

---

## ⚠️ Security Impact

- **Privilege Escalation**: Immediate root access
- **Remote Code Execution**: Commands can be executed on the system
- **Backdoor Risk**: Service is undocumented, invisible to the user
- **No Fix Available**: No firmware updates or mitigations provided by vendor

---

## 🧑‍💻 Discoverer

Discovered by: **Aoun Shah**  

---

## 🔗 References
- Firmware versions obtained from camera app and Telnet login
- CVE Request Pending

---

> This report is part of responsible disclosure efforts. This information is provided for educational and defensive security purposes only.
