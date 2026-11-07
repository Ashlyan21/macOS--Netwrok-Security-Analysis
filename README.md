# macOS Network Security Analysis Lab

## Project Overview

This project focuses on analyzing active network connections and listening ports using built-in macOS command-line utilities.

The objective is to develop foundational networking and security analysis skills relevant to IT Help Desk and Security Operations Center (SOC) roles.

## Tools Used

- macOS Terminal
- netstat
- lsof
- GitHub

## Lab 1: Analyzing TCP Connections

**Command:**

`netstat -an -p tcp`

### Findings: TCP Connection Analysis

**Command Executed:** `netstat -an -p tcp`

**Observations:**
- Identified multiple active TCP connections using macOS Terminal.
- Observed both ESTABLISHED and LISTEN connection states.
- Identified network activity using IPv4 (tcp4) and IPv6 (tcp6).
- Observed several remote connections using port 443, commonly associated with HTTPS traffic.
- Identified connections involving the loopback address (127.0.0.1), which is used for local communication between processes.
- Observed multiple listening sockets, indicating services waiting for incoming TCP connections.

**Security Analysis:**

The results demonstrate that multiple applications and services were communicating over the network. Connections using port 443 are consistent with common HTTPS traffic, although the port number alone does not verify that the traffic is secure or legitimate.

Listening ports may represent legitimate system services or applications. Additional investigation is necessary to determine which processes own these ports and whether they are expected.

**Conclusion:**

Successfully analyzed TCP connection states and identified active network activity using the macOS `netstat` utility. No definitive evidence of malicious activity was established from the connection listing alone.

Further investigation using `lsof` is recommended to identify listening processes and assess their purpose.

## Lab 2: Identifying Listening Ports

**Command:**

`lsof -nP -iTCP -sTCP:LISTEN`

### Findings: Listening Port Analysis

**Command Executed:**

`lsof -nP -iTCP -sTCP:LISTEN`

**Objective:**

Identify applications and background processes listening for incoming TCP connections on macOS.

**Observations:**

- Identified multiple processes with active listening TCP sockets.
- Observed the Apple `rapportd` process listening on TCP port 51256.
- Identified a process labeled `ControlCe` listening on TCP ports 5000 and 7000 using IPv4 and IPv6.
- Observed several Adobe-related background processes listening on local TCP ports.
- Identified both wildcard listening addresses (`*`) and loopback addresses (`127.0.0.1`).

**Security Analysis:**

The results show that multiple system services and application processes were listening for TCP connections.

Several Adobe-related processes were bound to the loopback address, indicating that those sockets were configured for local communication.

Other processes were bound to wildcard addresses, which may permit incoming network connections depending on system configuration and firewall rules.

The presence of listening ports does not automatically indicate a security vulnerability or malicious activity.

**Conclusion:**

Successfully used the macOS `lsof` utility to identify listening TCP ports and their associated processes.


Further investigation could include examining process paths, verifying application identities, and reviewing macOS firewall settings.

**Skills Demonstrated:**

- Network connection analysis
- TCP port identification
- Process investigation
- Understanding loopback versus wildcard listening addresses
- Basic security assessment
- Technical documentation

## Lessons Learned

This lab demonstrates how built-in macOS tools can help investigate network activity and identify applications accepting incoming connections.

### Process Investigation: macOS Control Center

**Command Executed:**

`ps -p 687 -o pid,comm,args`

**Objective:**

Investigate the process associated with TCP ports 5000 and 7000 to determine its identity and location.

**Findings:**

- Identified process ID (PID) 687.
- Confirmed the process was associated with macOS Control Center.
- Located the executable within `/System/Library/CoreServices/ControlCenter.app/`.
- The process path was consistent with a standard macOS system application.

**Security Assessment:**

The process appeared consistent with legitimate macOS system activity. No obvious indicators of malicious behavior were identified from the process information examined.

However, additional verification, such as checking the application's code signature, would be required to establish greater confidence in its authenticity.

**Conclusion:**

Successfully investigated a listening network process and identified its associated application and executable path using macOS command-line tools.
