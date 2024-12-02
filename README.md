# Wireshark trafic analisys

Practical Wireshark traffic analysis

1 – Make an http request to the DVWA (Damn Vulnerable Web App) login site using valid credentials. Capture this request with Wireshark using the TCP filter on port 80 and identify the TCP negotiation handshake. Identifies the username used and its password.



2º- Enter an XSS reflected in the DVWA site and capture it with Wireshark. Next, apply a filter showing all requests made via http and where the source IP address is Kali Linux. View the http request where the XSS is executed.



3º- Make a request to the Google search engine and capture said request with Wireshark. Identifies the query performed to find out if the certificate used on the website is valid. Shows the exact line where the certificate status is returned. 



4º- Capture a request with Wireshark to the Cocacola website. Identifies the request using the requested url in the browser.



5º- Connect via FTP to the metasploitable server from the Kali Linux machine and acquire the my.cnf file. Record the entire process with Wireshark and filter all the steps carried out by said protocol. Pay special attention to the data displayed by ftp (ftp server version, user used, etc.).
