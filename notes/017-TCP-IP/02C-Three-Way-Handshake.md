# TCP Connection Establishment and Data Transfer: Cybersecurity Implications

## Connection Establishment (Three-Way Handshake) - Vulnerability and Defense

* **Connection-Oriented:** TCP's connection-oriented nature, while ensuring reliability, can be exploited.
* **Three-Way Handshake and SYN Flood Attacks:**
    * **Attack:** A malicious actor (attacker) sends a flood of SYN packets to a target server (host B).
    * **Exploitation:** The server allocates resources for each SYN-ACK it sends, waiting for the final ACK. If the ACKs never come (because the attacker is spoofing IP addresses or simply not sending them), the server's resources are exhausted, leading to a denial-of-service (DoS).
    * **Defense:**
        * **SYN Cookies:** The server doesn't immediately allocate full resources. Instead, it encodes SYN-ACK information into a cookie and sends it back. If the final ACK is valid, the server allocates resources.
        * **Firewall Rate Limiting:** Limiting the number of SYN packets a server can receive within a specific timeframe.
        * **Intrusion Prevention Systems (IPS):** Detecting and blocking SYN flood patterns.

## Sequence Numbers and Acknowledgements - Spoofing and Hijacking

* **Sequence Number Prediction:**
    * **Attack:** Older TCP implementations had predictable sequence number generation. An attacker could predict the next sequence number, allowing them to inject malicious packets or hijack an existing connection.
    * **Exploitation:** By injecting packets with the correct sequence number, an attacker can insert malicious data into the communication stream, or take over the session.
    * **Defense:**
        * **Randomized Sequence Numbers:** Modern TCP stacks use highly randomized sequence number generation to prevent prediction.
        * **IPsec:** Encrypting and authenticating TCP traffic, making it much harder for attackers to inject or modify packets.

* **TCP Hijacking:**
    * **Attack:** An attacker intercepts a TCP connection and takes over the session.
    * **Exploitation:** If an attacker can determine the current sequence and acknowledgement numbers, they can inject packets that appear to be from the legitimate client.
    * **Defense:**
        * **Strong Authentication:** Using strong authentication methods (e.g., TLS/SSL) to verify the identity of communicating parties.
        * **Session Monitoring:** Implementing intrusion detection systems (IDS) to monitor for suspicious changes in sequence numbers or other session characteristics.

## Flow Control - DoS and Resource Exhaustion

* **Window Size Manipulation:**
    * **Attack:** Malicious actors could send crafted packets that manipulate the window size, potentially causing DoS conditions.
    * **Exploitation:** By sending packets that trick a host into setting its window size to 0, an attacker could effectively block the flow of legitimate traffic. Or by flooding a server with requests, and forcing the server to have a window size of 0, they can make the server appear to be down.
    * **Defense:**
        * **Firewall Inspection:** Firewalls can inspect TCP headers and filter out packets with suspicious window size values.
        * **Rate Limiting:** Limiting the rate of incoming connections and data to prevent resource exhaustion.
* **Resource Exhaustion:**
    * **Attack:** Attackers can flood a server with requests, forcing it to allocate resources and fill its buffers, leading to a DoS.
    * **Defense:**
        * **Load Balancing:** Distributing traffic across multiple servers to prevent any single server from being overwhelmed.
        * **Intrusion Detection/Prevention Systems (IDS/IPS):** Detecting and blocking malicious traffic patterns.
        * **Properly configured firewalls.**
