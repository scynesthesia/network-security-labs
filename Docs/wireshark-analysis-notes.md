# Wireshark Analysis Notes

This document captures basic packet analysis in a controlled lab environment using Wireshark to observe protocol behavior, troubleshoot connectivity, and identify security-relevant traffic patterns.

## Objective

Use Wireshark to:
- inspect packet-level communication
- understand common protocol behavior
- identify normal versus suspicious traffic patterns
- improve troubleshooting and traffic analysis skills

## Lab Scope

The packet captures in this document are intended for local, private, or otherwise authorized lab environments only.

## 1. DNS Traffic Analysis

### Protocol
`DNS`

### What was observed
- DNS queries from a client to resolve domain names
- DNS responses returning IP address records
- Standard request/response behavior over port 53

### Security Relevance
DNS traffic can reveal which domains a system is trying to reach. Unexpected queries may indicate misconfiguration, malware activity, or unauthorized communication.

## 2. DHCP Traffic Analysis

### Protocol
`DHCP`

### What was observed
- DHCP discovery and offer messages
- Address assignment behavior between client and DHCP server
- Initial network configuration traffic when a host joins the network

### Security Relevance
DHCP helps identify how hosts receive network configuration. Unexpected DHCP behavior can indicate rogue DHCP servers or network misconfiguration.

## 3. HTTP Traffic Analysis

### Protocol
`HTTP`

### What was observed
- Unencrypted web requests and responses
- Visible headers and application-layer data
- Client-server communication over port 80

### Security Relevance
HTTP traffic is readable in transit. This demonstrates why sensitive traffic should not rely on plaintext protocols in production environments.

## 4. HTTPS / TLS Traffic Analysis

### Protocol
`TLS / HTTPS`

### What was observed
- TLS handshake activity
- Encrypted application traffic after session establishment
- Certificate exchange and secure session negotiation

### Security Relevance
TLS reduces exposure by encrypting traffic in transit. Packet analysis still reveals metadata such as destination, timing, and handshake behavior, even when payload data is protected.

## 5. TCP Handshake and Session Behavior

### Protocol
`TCP`

### What was observed
- Three-way handshake (`SYN`, `SYN-ACK`, `ACK`)
- Session establishment and teardown
- Retransmissions or resets when communication issues occurred

### Security Relevance
Understanding normal TCP behavior is important for troubleshooting dropped connections, firewall interference, latency issues, and abnormal session patterns.

## 6. ICMP Traffic Analysis

### Protocol
`ICMP`

### What was observed
- Echo requests and echo replies during connectivity testing
- Basic reachability validation between hosts

### Security Relevance
ICMP is useful for troubleshooting, but unusual ICMP patterns can also indicate network scanning or reconnaissance activity.

## 7. Indicators to Review During Packet Analysis

### Areas to check
- Unexpected destination IP addresses
- Repeated failed connections
- Unusual DNS queries
- Excessive retransmissions
- Plaintext credentials or sensitive data sent over insecure protocols
- Unrecognized services communicating externally

### Security Relevance
Packet analysis becomes more useful when it moves beyond protocol identification and starts validating whether observed traffic matches expected behavior.

## 8. Example Security Takeaways

- Plaintext application traffic increases exposure and should be minimized
- DNS activity can provide strong clues about host behavior
- TLS improves confidentiality but does not hide all metadata
- Repeated retransmissions or resets may indicate filtering, instability, or misconfiguration
- Packet captures are useful for both troubleshooting and security review in controlled environments

## Notes

Wireshark is valuable for understanding protocol behavior, validating expected traffic flows, and identifying anomalies at the packet level. It should be used only in environments where packet capture is authorized.
