# Task 1: Local Network Port Scanning using Nmap

## Objective
The objective of this task was to conduct a basic reconnaissance of the local network in order to identify active hosts and detect any open TCP ports on those devices. This exercise is essential in understanding how network services can be exposed and potentially exploited if not properly secured. The task also aims to build hands-on familiarity with one of the most widely used network scanning tools, Nmap.

## Environment
- **Operating System**: Kali Linux (Virtual Machine)
- **Network Interface**: eth0
- **Local IP Address**: 192.168.12.128
- **Network Range Scanned**: 192.168.12.0/24

## Tools Used
- **Nmap**: Used for performing a TCP SYN scan to discover live hosts and open ports.
- *(Optional)* **Wireshark**: Not used in this task but can be leveraged to monitor traffic during scans.

## Methodology

### Step 1: Identify Local IP and Network Range
The following command was used to find the local IP and subnet range:
```bash
ip a
The result indicated that the local IP address was 192.168.12.128, and the subnet was /24, leading to a network scan range of 192.168.12.0/24.

Step 2: Run a TCP SYN Scan
A TCP SYN scan was performed on the full subnet using Nmap:

bash
Copy code
nmap -sS 192.168.12.0/24
This type of scan sends SYN packets to initiate a connection and identifies open ports based on responses received.


Step 3: Save the Output
To retain a copy of the scan results, the output was redirected to a text file using:

bash
Copy code
nmap -sS 192.168.12.0/24 -oN scan-results.txt

Scan Results

| IP Address     | Open Ports        | Service | Notes                                               |
| -------------- | ----------------- | ------- | --------------------------------------------------- |
| 192.168.12.1   | 80/tcp            | HTTP    | Indicates a web interface, likely for router/device |
| 192.168.12.2   | 53/tcp (filtered) | DNS     | Port is filtered; may be DNS with firewall enabled  |
| 192.168.12.254 | None              | -       | All ports are filtered; no services identified      |
| 192.168.12.128 | None              | -       | Local machine; all scanned ports are closed         |

Analysis
192.168.12.1 is hosting a web service on port 80, potentially a management interface which could be a target if not secured.

192.168.12.2 shows a filtered DNS port, suggesting either firewall protection or traffic control mechanisms in place.

The scan also confirms that the local system is not exposing any TCP services, which is a good baseline from a security standpoint.

Conclusion
This task successfully demonstrated how to perform a TCP SYN scan on a local network using Nmap. The scan provided visibility into active systems and the services they are exposing. From a security perspective, identifying such services is a critical first step in risk assessment and vulnerability management. Ensuring that only necessary services are running, and that firewall rules are properly configured, is essential in protecting any networked environment from external and internal threats.

Recommendations
Disable or secure unnecessary services discovered during port scans.

Implement firewall rules to filter or block unused ports.

Regularly audit and monitor network activity using tools like Nmap and Wireshark.
