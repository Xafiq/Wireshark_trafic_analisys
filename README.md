# Wireshark trafic analisys
<!-- hide -->

> By [@xafiq](https://github.com/xafiq) at [4Geeks Academy](https://4geeksacademy.co/)

[![build by developers](https://img.shields.io/badge/build_by-Developers-blue)](https://4geeks.com)
[![build by developers](https://img.shields.io/twitter/follow/4geeksacademy?style=social&logo=twitter)](https://twitter.com/4geeksacademy)

*These instructions are [available in spanish](https://github.com/breatheco-de/set-up-an-SSL-in-openSSL-with-a-secure-server/blob/main/README.md)*


# 🌱 How to Start This Project?


## Requirements

- Kali Machine (attacker)
- Debian (victim)
- Metasploitable Machine (server)

## Practical Wireshark traffic analysis

# 📝 Instructions

## 1 - Capture and analyze HTTP request

### Step-by-step instructions:

**Step 1: Set up Wireshark**

- Open Wireshark on Kali Linux.
- Click on "Capture" in the top menu bar to start capturing packets.

**Step 2: Apply TCP filter for HTTP traffic**

- In the filter box at the bottom of the Wireshark window, enter `tcp.port == 80` and press Enter. This will capture all HTTP traffic.

**Step 3: Make an HTTP request in the browser**

- Open a web browser on Kali Linux.
- Navigate to the DVWA login page (e.g., http://[IP-OF-KALI]/dvwa/login.php).
- Enter valid credentials and submit the form.

**Step 4: Analyze the captured packets**

- In Wireshark, look for the HTTP request packet that matches your login attempt.
- Pay attention to the TCP negotiation handshake (SYN, SYN/ACK, ACK) in the packet details.

### Explanation of the expected outcome:

- The TCP handshake will be visible in the packet details as three consecutive packets with specific flags and sequence numbers.
- In the HTTP request section, you should see the username used for authentication (e.g., "admin") along with its corresponding password.


## 2 - Capture and analyze XSS attack

### Step-by-step instructions:

**Step 1: Set up Wireshark**

- Open Wireshark on Kali Linux.
- Click on "Capture" in the top menu bar to start capturing packets.

**Step 2: Apply filter for HTTP traffic from Kali Linux**

- In the filter box at the bottom of the Wireshark window, enter `host [IP-OF-KALI] and http` and press Enter. This will capture all HTTP requests from your Kali machine.

**Step 3: Perform an XSS attack in DVWA**

- Open a web browser on Kali Linux.
- Navigate to the DVWA site (e.g., http://[IP-OF-KALI]/dvwa/vulnerabilities/xss_r.php).
- Enter a simple XSS payload, such as `<script>alert('XSS')</script>`, and submit the form.

**Step 4: Analyze the captured packets**

- In Wireshark, look for the HTTP request packet that matches your XSS attack.
- You should see the exact line where the XSS payload was sent.


### Explanation of the expected outcome:

- The HTTP request will contain the XSS payload in its data section. This payload can be used to execute JavaScript code on the target's browser.



## 3 - Capture and analyze Google search certificate validation

### Step-by-step instructions:

**Step 1: Set up Wireshark**

- Open Wireshark on Kali Linux.
- Click on "Capture" in the top menu bar to start capturing packets.

**Step 2: Apply filter for HTTP traffic from Kali Linux**

- In the filter box at the bottom of the Wireshark window, enter `host [IP-OF-KALI] and http` and press Enter. This will capture all HTTP requests from your Kali machine.

**Step 3: Make a request to Google search engine**

- Open a web browser on Kali Linux.
- Navigate to google.com and perform a simple search (e.g., "Wireshark tutorial").

**Step 4: Analyze the captured packets**

- In Wireshark, look for the HTTP request packet that matches your Google search.
- Look for the line where the certificate status is displayed. It should indicate whether the certificate used on google.com is valid or not.


### Explanation of the expected outcome:

- The certificate validation result will be displayed in the SSL/TLS handshake section. If it's a valid certificate, you'll see "OK" at the bottom.



## 4 - Capture and analyze Cocacola website request

### Step-by-step instructions:

**Step 1: Set up Wireshark**

- Open Wireshark on Kali Linux.
- Click on "Capture" in the top menu bar to start capturing packets.

**Step 2: Apply filter for HTTP traffic from Kali Linux**

- In the filter box at the bottom of the Wireshark window, enter `host [IP-OF-KALI] and http` and press Enter. This will capture all HTTP requests from your Kali machine.

**Step 3: Make a request to Cocacola website**

- Open a web browser on Kali Linux.
- Navigate to cocacola.com (or any other website of choice).

**Step 4: Analyze the captured packets**

- In Wireshark, look for the HTTP request packet that matches your Cocacola site request.
- You should see the exact line where the requested URL is displayed.


### Explanation of the expected outcome:

- The HTTP request will contain the full URL of the website you accessed (e.g., "GET / HTTP/1.1").


5º- Connect via FTP to the metasploitable server from the Kali Linux machine and acquire the my.cnf file. Record the entire process with Wireshark and filter all the steps carried out by said protocol. Pay special attention to the data displayed by ftp (ftp server version, user used, etc.).
