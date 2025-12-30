This is an overview of the Yealink T19P-E2 phone and its "hackability".

There is no "ready to install" 3rd party firmware for the Yealink T19P-E2 phone, because it has 

The Yealink T19P-E2 is a legacy device and "end-of-life" since 2021 - 
but since the firmware security is less robust than newer models, it is the perfect target for hobbyist research.

The Yealink T19P-E2 is a widely used, entry-level IP phone that has been the subject of significant security research. Because it is a budget device running a Linux-based firmware with a relatively wide attack surface, it is considered highly "hackable" for educational and research purposes.

The T19P-E2 is known to have several vulnerability classes

* Command Injection (Root Access): The device has history with authenticated Remote Code Execution (RCE). Specifically, CVE-2023-43959 allows an attacker with credentials (even low-level user ones) to execute arbitrary commands as root via the "Ping" diagnostic tool.
* Weak Encryption/Hardcoded Keys: Security researchers have found hardcoded AES keys in Yealink firmware used to encrypt configuration files. If you can obtain a config file (.cfg) from a network, you can often decrypt it to find cleartext passwords (SIP credentials, admin passwords)
* Supply Chain / Provisioning Attacks: The Yealink RPS (Redirection and Provisioning Service) has been scrutinized. If a phone is reset, it queries Yealink's central server to find its configuration. Researchers have demonstrated that if you can guess the MAC address (which is predictable for specific batches), you can potentially hijack the provisioning flow.

Good links to read
* https://www.synacktiv.com/publications/no-grave-but-the-sip-reversing-a-voip-phone-firmware
* https://www.cvedetails.com/cve/CVE-2023-43959/#:~:text=References%20for%20CVE%2D2023%2D43959,(Authenticated)%20%2D%20Hardware%20webapps%20Exploit
* https://github.com/traviscross/yealink-confenc
