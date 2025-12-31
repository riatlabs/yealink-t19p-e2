# Device Overview: Yealink T19P-E2

The Yealink T19P-E2 is a budget, entry-level IP phone. It reached End-of-Life (EOL) in 2021, meaning it no longer receives security patches. While there is no "ready-to-install" open-source firmware (like OpenWrt) due to proprietary hardware drivers, its Linux-based system makes it a popular target for security research.

Size: 185mm x 188mm x 143mm.

The T19P-E2 is known to have several vulnerability classes

* Command Injection (Root Access): The device has history with authenticated Remote Code Execution (RCE). Specifically, CVE-2023-43959 allows an attacker with credentials (even low-level user ones) to execute arbitrary commands as root via the "Ping" diagnostic tool.
* Weak Encryption/Hardcoded Keys: Security researchers have found hardcoded AES keys in Yealink firmware used to encrypt configuration files. If you can obtain a config file (.cfg) from a network, you can often decrypt it to find cleartext passwords (SIP credentials, admin passwords)
* Supply Chain / Provisioning Attacks: The Yealink RPS (Redirection and Provisioning Service) has been scrutinized. If a phone is reset, it queries Yealink's central server to find its configuration. Researchers have demonstrated that if you can guess the MAC address (which is predictable for specific batches), you can potentially hijack the provisioning flow.


# Research Tools

Since these phones run on Linux, most research tools are open-source and CLI-based, making them perfect for macOS and Linux users.

Firmware Analysis: Use binwalk (available via brew on macOS or nix-shell -p binwalk on NixOS) to extract the filesystem.

Decryption: You can run yealink-confenc via Python.


Good links to read
* https://www.synacktiv.com/publications/no-grave-but-the-sip-reversing-a-voip-phone-firmware
* https://www.cvedetails.com/cve/CVE-2023-43959/#:~:text=References%20for%20CVE%2D2023%2D43959,(Authenticated)%20%2D%20Hardware%20webapps%20Exploit
* https://github.com/traviscross/yealink-confenc
