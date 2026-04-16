# Nmap EC2 Validation

This document captures an authorized Nmap scan against a self-managed EC2 lab instance used to validate externally exposed services.

## Objective

Verify that the externally visible services on the EC2 instance match the intended configuration after deployment and service setup.

## Environment

- Platform: AWS EC2
- OS: Amazon Linux
- Public IP: `54.152.204.119`
- Intended exposed services:
  - `22/tcp` for SSH administration
  - `80/tcp` for HTTP web service

## Local Service Context

On the instance, Apache was installed and started successfully, and local service checks confirmed that SSH and HTTP were listening.

## External Scan 1: Service Version Detection

### Command
`nmap -Pn -sV 54.152.204.119`

### Output
```text
Starting Nmap 7.99 ( https://nmap.org ) at 2026-04-15 23:21 -0300
Nmap scan report for ec2-54-152-204-119.compute-1.amazonaws.com (54.152.204.119)
Host is up (0.16s latency).
Not shown: 998 filtered tcp ports (no-response)

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.7 (protocol 2.0)
80/tcp open  http    Apache httpd 2.4.66 ((Amazon Linux))

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 21.39 seconds
```

## External Scan 2: Full TCP Scan

### Command
`nmap -Pn -p- 54.152.204.119`

### Output
```text
Starting Nmap 7.99 ( https://nmap.org ) at 2026-04-15 23:24 -0300
Nmap scan report for ec2-54-152-204-119.compute-1.amazonaws.com (54.152.204.119)
Host is up (0.16s latency).
Not shown: 65533 filtered tcp ports (no-response)

PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 228.83 seconds
```

## Interpretation

The external scan confirmed that only the intended services were exposed:

- `22/tcp` was reachable for SSH administration
- `80/tcp` was reachable for the Apache web service
- no additional unexpected TCP services were externally exposed

This result aligned with the expected security group and host service configuration.

## Security Relevance

This validation demonstrates the importance of checking externally visible services instead of assuming that a locally running service is reachable. It also shows how Nmap can be used to confirm whether cloud network controls and host configuration match the intended attack surface.

## Notes

This scan was performed against a self-managed EC2 instance in an authorized personal lab environment.
