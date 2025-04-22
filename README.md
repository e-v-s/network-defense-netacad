# network-defense-netacad
things to note/study/memorize

### [System & Network Defense](#system-network-defense)
#### [Application Security](#app-sec)
#### [Network Hardening: Services and Protocols](#net-hardening-services)
#### [Network Hardening: Segmentation](#net-hardening-segmentation)
#### [Hardening Wifi & Mobile Devices: Segmentation](#hardening-wifi)

<h1 id="system-network-defense">System & Network Defense</h1>

<h2 id="app-sec">Application Security</h2>

- Application Development

  Develop & Test --> QA

  Staging & Prod --> Test the app on a staged environment similar to prod

  Provisioning & Deprovisioning --> Automate both

- Security Coding Techniques
  1. Normalization --> Converts an <mark>input str</mark> into <mark>binary</mark>. It allows malware input to be identified --> **Integrity**
  2. Stored procedute --> Use precompiled SQL statements to work on user inputs, it reduces network traffic --> faster results
  3. Obfuscation and camouflage --> Both are used to prevent softwares being reverse engineered. How? **Obfuscation** hides data with random stuff, **camouflage** replaces sensitive data with realistic fictional data
  4. Code reuse --> Pay attention to code reuse, as it can reintroduce vulnerabilities to new code
  5. SDKs --> libs. Pay attention to vulnerabilities in them.
  6. Code signing --> authenticity of a software
  7. Secure cookies --> data stored for future requests, use it with HTTPS

- Input Validation

  Avoids insertion of data --> **Integrity**
  
  Use **validation rules** to every data entry so it matches the parameters defined by the DB designer --> <mark>size</mark>, <mark>format</mark>, <mark>consistency</mark>, <mark>range</mark> and <mark>check digit for error detection</mark>.

- Integrity Checks

  Measures consistencies, verifies integrity against a snapshot. It uses **hash functions** --> <mark>checksum</mark>.
  a. checksum
  b. hash functions --> MD5, SHA-1, SHA-256 and SHA-512
  c. versioning
  d. backup integrity
  e. authorization --> confidentiality

- Countermeasures
  1. Unauthorarized access to physical stuff: <mark>policies/stds/procedures</mark>
  2. Servers and system downtime: <mark>business continuity plan</mark> and <mark>DR plan</mark>
  3. Network OS vulnerability: <mark>policies for patching</mark> and the <mark>patching</mark> itself
  4. Unauthorized access to systems: <mark>MFA</mark> and <mark>monitoring</mark>
  5. Data loss: backup procedures and data classification stds
  6. Software development vulnerabilities: test it


<h2 id="net-hardening-services">Network Hardening: Services and Protocols</h2>

<h3>Network and Routing Services: use a port scanner to detect open ports</h3>

  *only necessary ports must be exposed*

- DHCP **it's a server that assigns IP addresses and other config info to network devices**:

   [ ] Physically secure it
  
   [ ] Patching
  
   [ ] Put it behind a firewall
  
   [ ] Monitor it and review logs
  
   [ ] Antivirus
  
   [ ] Hardening
  
   [ ] Close unused ports

- DNS **translates url into an IP address**:

  [ ] Use DNSSEC

  [ ] Patching

  [ ] Prevent version string

  [ ] Separate internal and external DNS servers

  [ ] Restrict allowed transactions by client IP

  [ ] Disable/restrict zone transfers and dynamic updates as much as possible

  [ ] Monitor it and review logs

  [ ] Sign zones

- ICMP **protocol is used to send error messages, it's used by ping**

  [ ] Network filtering of ICMP requests

- RIP **limits the number of hops from src to destination that are allowed in a network path**, it calculates the best route based on the hop count.

  [ ] Patching

  [ ] Athentication

- NTP **syncs the network computer system clocks**, it is used by hackers to disrupt secure communication thast depends on digital certificates and to hide attack info.

  [ ] Use NTP authentication to verify if the server is trusted


<h3>Telnet, SSH & SCP</h3>

- Telnet -TCP 23: old protocol, **no encryption*, uses plaintext when authenticating a device and transmitting data;
- SSH -TCP 22: **encrypted** authentication and communication for **remote connection to a device**;
- SCP: **secure file transfer** between devices. It **uses ssh**.

<h3>Secure Protocols</h3>

- SNMPv3: collects statistics from TCP/IP devices to monitor network and devices. Prevents **eavesdropping** and **tampering** on data transiting (confidentiality and integrity);
- HTTP 80: use **SSL/TLS** --> HTTPS --> encryption of the communication between client and server;
- FTP: transfers files between client-server, it's **plantext** --> **FTPS** uses SSL/TLS
- POP 110 | IMAP 143 | MIME: the first 2 are insecure, you have to use SSL/TLS. MIME is secure and provides integrity, authentication and nonrepudiation via digital signatures and message encryption.

<h2 id="net-hardening-segmentation">Network Hardening: Segmentation</h2>

<h3>VLANs</h3>

- Group devices (logically) into small sections of your LAN
- Individual ports on a switch is assigned to a specific VLAN
- Another port can interconnect switches to provide communication between VLANs --> **trunk ports**
- Independent network even tho they're sharing an infra with other VLANs
- **Limits broadcast traffic in a switched network**
- It must be secured by:

  a. monitoring its performance
  b. patching
  c. advanced configurations

<h3>DMZ</h3>
Network between trusted and untrusted network.

| INSIDE | 
| ------------- |
| Allows access to an unstrusted network, without compromising the internal network | 
| web servers | 
| mail servers |

| Level of Risk | Zones         |
| ------------- | ------------- |
| low           | LAN zone      |
| medium-low    | extranet zone |
| medium-high   | DMZ           |
| high          | internet      |

- Zero trust model

  Firewalls manage east-west traffic --> between servers inside de DC and north-south traffic --> data in/out the network

  **Monitoring ALL users inside the network regardless of their status/role**

  - Unauthorized access to systems, applications and data --> Define strict access control stuff

  - Unauthorized LAN access --> Securing wiring closets, data centers and computer rooms. deny access to anyone without proper credentials

  - Exploits of data in transit --> encryption
  - Network OS vulnerabilities --> patching
  - Unauthorized access by rogue users --> Require passphrases or authentication for wifi
  - Unauthorized network probing and port scanning --> conduct post-config pentest


<h2 id="hardening-wifi">Hardening Wifi & Mobile Devices</h2>
<h3>Wifi Security</h3>

- Evolution of WPA
  1. WPA is the evolution of WEP. It provides **message integrity checks** (MIC)





  


