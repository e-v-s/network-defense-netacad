network-defense-netacad<br>
things to note/study/memorize

- [System \& Network Defense](#system--network-defense)
  - [Application Security](#application-security)
  - [Network Hardening: Services and Protocols](#network-hardening-services-and-protocols)
    - [Network and Routing Services: use a port scanner to detect open ports](#network-and-routing-services-use-a-port-scanner-to-detect-open-ports)
    - [Telnet, SSH \& SCP](#telnet-ssh--scp)
    - [Secure Protocols](#secure-protocols)
  - [Network Hardening: Segmentation](#network-hardening-segmentation)
    - [VLANs](#vlans)
    - [DMZ](#dmz)
  - [Hardening Wifi \& Mobile Devices](#hardening-wifi--mobile-devices)
    - [Wifi Security](#wifi-security)
    - [Packet Tracer: Hardening](#packet-tracer-hardening)
    - [Authentication](#authentication)
      - [Types:](#types)
      - [Protocols:](#protocols)
      - [Mutual Authentication](#mutual-authentication)
      - [Communication Methods](#communication-methods)
  - [Cybersec Resilience](#cybersec-resilience)
    - [High Availability](#high-availability)
    - [The Five 9s](#the-five-9s)
    - [Single Points of Failures](#single-points-of-failures)
    - [N+1 Redundancy](#n1-redundancy)
    - [RAID](#raid)
    - [Spanning Tree](#spanning-tree)
    - [Router Redundancy](#router-redundancy)
    - [Location Redundancy](#location-redundancy)
    - [Resilient Design](#resilient-design)
    - [System and Data Backups](#system-and-data-backups)
    - [Designing High Availability Systems](#designing-high-availability-systems)
    - [Power](#power)
    - [HAVAC](#havac)
    - [Threat Manager](#threat-manager)
  - [Embedded and Specialized Systems](#embedded-and-specialized-systems)
    - [Threats to Key Industry Sectors](#threats-to-key-industry-sectors)
    - [Embedded Systems](#embedded-systems)
    - [IoT](#iot)
    - [VoIP Equipment](#voip-equipment)


# System & Network Defense

## Application Security

- Application Development

  Develop & Test --> QA

  Staging & Prod --> Test the app on a staged environment similar to prod

  Provisioning & Deprovisioning --> Automate both

- Security Coding Techniques
  1. Normalization --> Converts an `input str` into `binary`. It allows malware input to be identified --> **Integrity**
  2. Stored procedute --> Use precompiled SQL statements to work on user inputs, it reduces network traffic --> faster results
  3. Obfuscation and camouflage --> Both are used to prevent softwares being reverse engineered. How? **Obfuscation** hides data with random stuff, **camouflage** replaces sensitive data with realistic fictional data
  4. Code reuse --> Pay attention to code reuse, as it can reintroduce vulnerabilities to new code
  5. SDKs --> libs. Pay attention to vulnerabilities in them.
  6. Code signing --> authenticity of a software
  7. Secure cookies --> data stored for future requests, use it with HTTPS

- Input Validation

  Avoids insertion of data --> **Integrity**
  
  Use **validation rules** to every data entry so it matches the parameters defined by the DB designer --> `size`, `format`, `consistency`, `range` and `check digit for error detection`.

- Integrity Checks

  Measures consistencies, verifies integrity against a snapshot. It uses **hash functions** --> `checksum`.
  a. checksum
  b. hash functions --> MD5, SHA-1, SHA-256 and SHA-512
  c. versioning
  d. backup integrity
  e. authorization --> confidentiality

- Countermeasures
  1. Unauthorarized access to physical stuff: `policies/stds/procedures`
  2. Servers and system downtime: `business continuity plan` and `DR plan`
  3. Network OS vulnerability: `policies for patching` and the `patching` itself
  4. Unauthorized access to systems: `MFA` and `monitoring`
  5. Data loss: backup procedures and data classification stds
  6. Software development vulnerabilities: test it


## Network Hardening: Services and Protocols

### Network and Routing Services: use a port scanner to detect open ports

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


### Telnet, SSH & SCP

- Telnet -TCP 23: old protocol, **no encryption*, uses plaintext when authenticating a device and transmitting data;
- SSH -TCP 22: **encrypted** authentication and communication for **remote connection to a device**;
- SCP: **secure file transfer** between devices. It **uses ssh**.

### Secure Protocols

- SNMPv3: collects statistics from TCP/IP devices to monitor network and devices. Prevents **eavesdropping** and **tampering** on data transiting (confidentiality and integrity);
- HTTP 80: use **SSL/TLS** --> HTTPS --> encryption of the communication between client and server;
- FTP: transfers files between client-server, it's **plantext** --> **FTPS** uses SSL/TLS
- POP 110 | IMAP 143 | MIME: the first 2 are insecure, you have to use SSL/TLS. MIME is secure and provides integrity, authentication and nonrepudiation via digital signatures and message encryption.

## Network Hardening: Segmentation

### VLANs

- Group devices (logically) into small sections of your LAN
- Individual ports on a switch is assigned to a specific VLAN
- Another port can interconnect switches to provide communication between VLANs --> **trunk ports**
- Independent network even tho they're sharing an infra with other VLANs
- **Limits broadcast traffic in a switched network**
- It must be secured by:

  a. monitoring its performance
  b. patching
  c. advanced configurations

### DMZ
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


## Hardening Wifi & Mobile Devices

### Wifi Security

- Evolution of WPA
  1. WPA is the evolution of WEP

    - It provides **message integrity checks** (MIC) --> can detect if the data is altered.
    - It uses **temporary key integrity protocol** (TKIP) --> key management and encryption protection

  2. WPA2

    - Mandatory use of AES and replaced TKIP with CCMP


  3. WPA3
     
  4. WPS: do NOT use this

### Packet Tracer: Hardening


- **Part 1:** Configure Basic Security Settings for a Wireless Router

  - Change router's default admin password
  - Disable remote management

- **Part 2:** Configure Wireless Router Network Security

  - Enable SSID broadcast
  - Change the SSID name
  - Security mode: WPA2 Personal
  - Encryption: AES
  - Enable guest profile, do the same: WPA2 Personal and AES

- **Part 3:** Configure Wireless Clients Network Security

  - Connect to the wifi on the clients
  - DHCP
  - configure the IoT devices

- **Part 4:** Verify Connectivity and Security Settings

  - Test internet connectivity on the browser
  - Secure interconnectivity between default & guest by disabling (on router level) the access between them


### Authentication

#### Types:

- Open system authentication (less secure)
- Shared key authentication (more secure)


#### Protocols:

- Extensible Authentication Protocol (EAP)

|                    | EAP-TLS | PEAP   | EAP-TTLS | EAP-FAST |
| ------------------ | ------- | ------ | -------- | -------- |
| Client Cert?       | yes     | no     | no       | no       |
| Server Cert?       | yes     | yes    | yes      | no       |
| Easy do implement? | hard    | medium | medium   | easy     |
| Security           | high    | medium | medium   | medium   |


#### Mutual Authentication


- Prevent rogue access points with **mutual authentication**


#### Communication Methods


- Wifi & bluetooth
- NFC
- IR
- USB


## Cybersec Resilience

### High Availability

- Eliminate **single points of failure**
- Redundant stuff --> reliable crossover
- Active device and system monitoring

### The Five 9s

We have to achieve 99,999% of availability.

- Std systems
  We have to use standards for our systems so it's easier to maintain.
- Clustering
  Multiple devices serving a service, and for the users it looks like a unity: if one service fails, it's still running.
- Shared components systems
  The systems are built so that if a complete system fails there's another one to take its place.

### Single Points of Failures

Weak links along the service chain that fails to deliver high availability. It can be:

- Hardware
- Process
- Data
- Utility
- Anything

### N+1 Redundancy

A componenet **N** has to hova at least **+1** componenet so it can be redundant.

### RAID

It spreads data across several drives *except for RAID 0*.


RAID can be software-based or hardware-based. Terms:


- Mirrorring: it mirrors the drive to another drive;
- Striping: writes data across multiple drives, consecutive segments are stored in different drives;
- Striping with parity: after striping, checksums are generated to check if there are errors. These checksums are stored on a different drive.


| RAID<br>Level | # of<br>drives | Description                                     | PROS                               | CONS                                                    |
| ---------- | ----------- | ----------------------------------------------------- | ---------------------------------- | ------------------------------------------------------- |
| 0          | 2           | No redundancy                                         | Highest<br>performance             | No data<br>protection                                   |
| 1          | 2           | Disk mirrorring                                       | Data is<br>duplicated              | High cost                                               |
| 2          | 2           | Error-correcting<br>coding                            | NOT USED<br>ANYMORE                | Same performance<br>can be achieved<br>using RAID 3     |
| 3          | 3           | Byte-level<br>data striping<br>with dedicated parity  | Large sequencial<br> data requests | NO simultaneous<br>read+write<br>requests               |
| 4          | 3           | Block-level<br>data striping<br>with dedicated parity | Multiple read<br>requests          | Dedicated parity<br>drive bottlenecks<br>write requests |
| 5          | 3           | Striping + parity                                     | Simultaneous reads<br>and writes   | Performance<br>slower than<br>RAID 0 and 1              |



### Spanning Tree

When applying redundancy on a network infrastructure, **loops** and **duplicated frames** can occur on a switched network. **STP** addresses these issues. This protocol *prevents loops* on a network by blocking paths that could cause it, as when *switches interconnect* via multiple paths. If a switch of a cable fails, STP recalculates the paths and unblock the necessary ports.


### Router Redundancy

Standby router installation to prevent single point of failure of a default gateway.


**Example**


A **redundancy protocol** determines which router should take the active role in fwding traffic:

- fwding router
- standby router

Each router has its IP, but they share the virtual router which its IP addr is used by the endpoints. These endpoints will use the same default gateway even tho the redundancy protocol changes its default router.


Standby and fwding routers communicates with each other to make sure both are available. If the standby router fails, the fwding router will take the default role by itself and forward the traffic from the ISP to the virtual router and then to the endpoins --> **this is FIRST-HOP REDUNDANCY**


### Location Redundancy

- Sync replication
- Async replication
- Point-in-time replication


### Resilient Design

```
Network tolerant of failure
```

- Redundant switch links + STP
- Routing protocols with fine-tuning
- Application resilience:
  - Fault tolerant hardware
  - Cluster architecture
  - Backup and restore
- **Interwork Operating System** IOS resilience:
  - Resilient configuration feature
  - Maintains a secure working copy of the router IOS image file and a copy of the running config file

    ```
    R1# conf t
    R1(config)# secure boot-image
    R1(config)# secure boot-config
    ```

### System and Data Backups

### Designing High Availability Systems

- Elimination or Reduction of **Sinle Points of Failure**
  - Clusters
- Fault Tolerance
  - Data mirrorring
- System Resiliency


### Power

- Data centers: =/= power supply than the rest of the building;
- Redundant power sources;
- Power conditioning
- Backup power systems
- UPS available


### HAVAC

### Threat Manager

- Unauthorized access to facilities
  - Implement badge encryption for entry access
- Power interruptions
  - develop a DRP
- Social engineering
  - training and awareness
- Theft
  - asset tagging system



## Embedded and Specialized Systems

### Threats to Key Industry Sectors

SCADA --> Stuxnet


### Embedded Systems

These systems capture, store and process data.


- Why are they vulnerable?
  Because they are susceptible to timing attacks --> side-channel attack:

  ```
  side-channel attack is based on info gained from the implementation of a system, not the weaknesses in the software. Timing information, power consumption, electromagnetic leaks or even sound can be the source of information.
  ```

- How to protect them?
  Use **System on Chip (SoC) technology**, which is a *Small Form Factor SFF* hardware module, like raspberry pi or arduino. These devices are single-board computers and can be implemented using an integrated circuit that can me programmed or modified in the field called *field-programmable gate array FGPA*. That means that **it can be changed AFTER deploying the device**.

  ```
  many of the SoC devices have poor authentication and cannot be upgraded or patched --> implied trust --> because no formal program can verify security controls
  ```


### IoT

These devices expand the cyber attack surface.

1. Evaluation of the devices to ensure its ability to have its firmware updated with security patches;
2. Default credentials must be changed.


They are used to:

- track inventory, vehicles and personnel because they contain geospatial sensors;
- they use a **Real-Time OS**, RTOS, which means it allows rapid switching of tasks considering time, not throughput;
- can capture and transmit sensitive infos;
- Vulnerabilites of RTOS:
  - code injection
  - DoS attacks
  - Priority inversion
- they communicate using short, medium and long-range methods like 4G, 5G and zigbee.
- to secure IoT devices you should:
  - secure wifi;
  - know the devices connected to your network;
  - know what each of these devices do;
  - install security software on devices if possible;
  - secure mobile apps and smartphones used to communicate with IoT devices.


### VoIP Equipment



