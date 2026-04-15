# Nmap Lab Notes

This document captures basic Nmap usage in a controlled lab environment to identify live hosts, open ports, exposed services, and potential attack surface.

## Objective

Use Nmap to simulate a basic security assessment by:
- discovering reachable hosts
- identifying open ports
- detecting exposed services
- understanding how scan results inform defensive decisions

## Lab Scope

The scans in this document are intended for local, private, or otherwise authorized lab environments only.

## 1. Host Discovery

### Command
```bash
nmap -sn 192.168.1.0/24
```

### Purpose
Identify which hosts in the subnet respond and appear to be online.

### Security Relevance
Host discovery helps define the active attack surface before deeper enumeration begins.

## 2. Basic TCP Port Scan

### Command
```bash
nmap 192.168.1.10
```

### Purpose
Scan the most common TCP ports on a target host.

### Example Findings
- `22/tcp` open — SSH
- `80/tcp` open — HTTP
- `443/tcp` open — HTTPS

### Security Relevance
Open ports reveal exposed services and help determine where further hardening or segmentation may be needed.

## 3. Full TCP Port Scan

### Command
```bash
nmap -p- 192.168.1.10
```

### Purpose
Scan all 65535 TCP ports instead of only the default common set.

### Security Relevance
This can identify non-standard services that may be missed by a default scan.

## 4. Service Version Detection

### Command
```bash
nmap -sV 192.168.1.10
```

### Purpose
Identify the software and version associated with exposed services.

### Security Relevance
Version information helps assess patching status and possible vulnerability exposure.

## 5. Operating System Detection

### Command
```bash
sudo nmap -O 192.168.1.10
```

### Purpose
Attempt to identify the remote operating system.

### Security Relevance
OS detection helps defenders validate asset inventory and helps explain service behavior during analysis.

## 6. Aggressive Scan

### Command
```bash
sudo nmap -A 192.168.1.10
```

### Purpose
Combine OS detection, version detection, script scanning, and traceroute.

### Security Relevance
This gives a broader profile of the target, but is noisier and more detectable.

## 7. UDP Scan

### Command
```bash
sudo nmap -sU 192.168.1.10
```

### Purpose
Check for common UDP services such as DNS, SNMP, or DHCP-related exposure.

### Security Relevance
UDP services are often overlooked and may expose administrative or infrastructure functions.

## 8. Example Security Takeaways

- Unnecessary open ports should be closed or filtered
- Exposed administrative services such as SSH should be restricted by firewall rules or security groups
- Service versions should be reviewed for patching and support status
- Scan results should be compared against expected system purpose to identify drift or misconfiguration

## Notes

Nmap is useful for validating network exposure, confirming service availability, and identifying potential attack paths in controlled environments. It should be used only on systems that you own or are explicitly authorized to assess.
