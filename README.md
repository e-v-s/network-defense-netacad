# network-defense-netacad
things to note/study/memorize

### [System & Network Defense](#system-network-defense)
#### [Application Security](#app-sec)
#### [Network Security](#net-sec)

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


<h2 id="net-sec">Network Security</h2>

- Network and Routing Services: use a port scanner to detect open ports
  


