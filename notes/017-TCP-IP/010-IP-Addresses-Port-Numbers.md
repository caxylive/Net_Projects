<a name="top"></a>
[Back to Main](https://github.com/caxylive/Net_Projects/tree/main/notes)

---

# Cybersecurity: IP Addresses and Port Numbers

## IP Addresses: Attack Vectors

---

* **IP Spoofing:**
    * Attackers forge source IP addresses to:
        * **Masquerade:** Evade detection, appear as trusted sources.
        * **DDoS Amplification:** Overwhelm targets with spoofed traffic.
        * **Mitigation:** Implement ingress/egress filtering, use strong authentication.
* **Reconnaissance:**
    * Attackers use IP ranges to scan for potential targets.
    * **Mitigation:** Limit public exposure, use intrusion detection systems (IDS).

[Back to Top](#top)

---

## Port Numbers: Attack Vectors

* **Port Scanning:**
    * Attackers identify open ports to discover running services and vulnerabilities.
    * **Mitigation:** Close unnecessary ports, use firewalls, implement port knocking.
* **Exploiting Well-Known Ports (0-1023):**
    * **HTTP/HTTPS (80/443):**
        * SQL injection, XSS, directory traversal, web server exploits.
        * **Mitigation:** Web application firewalls (WAFs), input validation, regular patching.
    * **SSH (22):**
        * Brute-force attacks, exploiting SSH vulnerabilities.
        * **Mitigation:** Strong passwords, key-based authentication, limit SSH access.
    * **RDP (3389):**
        * Brute-force attacks, RDP vulnerabilities.
        * **Mitigation:** Network Level Authentication (NLA), limit RDP exposure, use VPNs.
    * **DNS (53):**
        * DNS amplification attacks, DNS cache poisoning.
        * **Mitigation:** Rate limiting, DNSSEC.
    * **FTP (20/21):**
        * anonymous access, bounce attacks.
        * **Mitigation:** Disable anonymous access, use SFTP or FTPS.
* **Exploiting Ephemeral Ports (Dynamic/Private):**
    * **Malware C2 Communication:**
        * Malware uses ephemeral ports to establish covert communication channels.
        * **Mitigation:** Network monitoring, endpoint detection and response (EDR).
* **Man-in-the-Middle Attacks:**
    * Intercepting traffic to steal or modify data.
    * **Mitigation:** Use HTTPS, VPNs, strong encryption.

[Back to Top](#top)

---

## Key Cybersecurity Considerations

* **Firewall Configuration:**
    * Strictly control inbound and outbound traffic based on port numbers and IP addresses.
* **Intrusion Detection/Prevention Systems (IDS/IPS):**
    * Monitor network traffic for suspicious activity, including port scanning and exploit attempts.
* **Vulnerability Management:**
    * Regularly scan for and patch vulnerabilities in operating systems and applications.
* **Network Segmentation:**
    * Isolate critical systems and services to limit the impact of a breach.
* **Least Privilege:**
    * Grant only necessary permissions to users and applications.
* **Regular Security Audits:**
    * Proactively find and fix vulnerabilities.
* **Honeypots/Honeynets:**
    * Lure attackers to a controlled enviroment to study their techniques.
* **Zero Trust Architecture:**
    * Never trust and always verify.
* **Endpoint security:**
    * Antivirus, antimalware, and host based firewalls are all important.

[Back to Top](#top)

---

## IANA and Security

* Understanding IANA port assignments is crucial for identifying legitimate traffic versus malicious activity.
* Regularly check for updates to IANA port assignments and be aware of new or emerging threats.

[Back to Top](#top)

---

## Ephemeral Ports and Security

* Be aware of the ephemeral port ranges used by different operating systems.
* Monitor ephemeral port traffic for suspicious activity, especially communication with unknown or malicious IP addresses.
* Implement application whitelisting to control which applications can use ephemeral ports.
