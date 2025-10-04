# Ex 10 Using-Wireshark---analyzing-web-browser-artifacts-email-header-analysis
## AIM:
To use Wireshark to analyze web browser activities and inspect email headers from captured network traffic.
## Architecture Diagram:
```mermaid
flowchart TD
    A[User System] --> B[Web Browser]
    A --> C[Email Client]
    B --> D[Network Traffic]
    C --> D
    D --> E[Wireshark Capture Engine]
    E --> F[Protocol Decoders HTTP SMTP IMAP POP]
    F --> G[Browser Artifacts URLs Cookies Auth]
    F --> H[Email Headers Source IP Server Timestamps]
    G --> I[Findings and Reports]
    H --> I
```
## DESIGN STEPS:
### Step 1:
- Install Wireshark and ensure correct network adapter selection.
- Enable packet capturing for your active interface (Wi-Fi/Ethernet).

### Step 2:
**Web Browser Artifact Analysis**
- Open a browser and visit websites with login forms (use dummy credentials).
- In Wireshark, filter traffic with:
    - ```http``` for normal HTTP requests
    - ```http.cookie``` for cookies
    - ```http.authbasic``` for basic authentication
- Identify:
    - URLs visited
    - GET/POST requests
    - Cookies & session IDs
    - Credentials (if plaintext HTTP is used)
### Step 3:
- Capture email traffic by sending/receiving emails (dummy mail server or provided PCAP).
- Use filters:
    - ```smtp``` (Simple Mail Transfer Protocol)
    - ```pop``` / ```imap``` (for received mail)
- Inspect email headers:
    - Source IP
    - Mail server hostname
    - Timestamps
    - Possible forged headers
## PROGRAM:
```mermaid
flowchart TD
    A[Start Wireshark Capture] --> B[Generate Traffic: Web Browsing & Emails]
    B --> C[Apply Protocol Filters: HTTP/SMTP/IMAP/POP]
    C --> D[Extract Browser Artifacts: URLs, Cookies, Credentials]
    C --> E[Analyze Email Headers: Source, Server, Metadata]
    D --> F[Save Findings]
    E --> F[Save Findings]
    F --> G[Generate Digital Forensic Report]
```

## A. Capturing Traffic in Wireshark

1. Open Wireshark and start capturing on the active interface (Wi-
Fi/Ethernet).

<img width="1366" height="768" alt="Screenshot (46)" src="https://github.com/user-attachments/assets/7de784b9-89d5-4268-abd5-c77e1d5c4d35" />

2. Perform activities like opening a website or sending an email through a
client (e.g., Gmail via browser or Thunderbird).

<img width="1366" height="768" alt="Screenshot (45)" src="https://github.com/user-attachments/assets/baef193d-6eb5-4e37-bf17-f1b31bb9be4b" />

3. Stop the capture once done.

## B. Analyzing Web Browser Artifacts
1. Apply filters like: http, tcp.port == 443 (for HTTPS), or dns to isolate
browser traffic.

<img width="1366" height="768" alt="Screenshot (45)" src="https://github.com/user-attachments/assets/f0f4bdfb-4e75-4912-a81f-588a7319b276" />

2. Inspect HTTP GET/POST requests:
o Look for URLs, hostnames, user agents, and cookies in the HTTP
headers.
o Follow TCP Stream to reconstruct page request flow:
▪ Right-click a packet → Follow → TCP Stream.

<img width="1366" height="768" alt="Screenshot (47)" src="https://github.com/user-attachments/assets/4c873708-2e6b-427d-9f58-97508701c642" />

3. Analyze DNS Queries:
o Filter: dns
o Reveal domains the browser tried to resolve.

<img width="1366" height="768" alt="Screenshot (48)" src="https://github.com/user-attachments/assets/dc879029-c000-480c-97f4-72575a6aecf8" />

## C. Email Header Analysis
1. Apply relevant filters:
o For POP3: tcp.port == 110
o For SMTP: tcp.port == 25 or 587
o For IMAP: tcp.port == 143 or 993

<img width="1366" height="768" alt="Screenshot (49)" src="https://github.com/user-attachments/assets/c4dff935-26e5-49ed-a124-0962f13c664a" />

2. Locate email data:
o Look for SMTP packets to see sender/receiver email addresses.
o Use "Follow TCP Stream" to view the full email headers and body if
unencrypted.

<img width="1366" height="768" alt="Screenshot (50)" src="https://github.com/user-attachments/assets/8b1d75d8-57ad-4720-8250-2462c552dd97" />

3. Extract Email Header Fields:
o Analyze From, To, Subject, Date, Message-ID, and relay servers used
in sending the email.

<img width="1366" height="768" alt="Screenshot (51)" src="https://github.com/user-attachments/assets/5eff731e-470e-4dbe-8430-240c0c81ef62" />

## OUTPUT:
Captured Web Activity and Email Header Information

## RESULT:
Web browser artifacts and email headers were successfully analyzed using Wireshark.

