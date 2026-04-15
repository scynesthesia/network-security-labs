# Linux Server Hardening Guide

This guide documents baseline hardening steps for a fresh Ubuntu or Debian server intended to operate as a secure entry point or internal application host in a lab or cloud environment.

## Objective

Reduce unnecessary exposure, restrict administrative access, and improve the baseline security posture of a Linux server.

## 1. Disable direct root SSH login

**Action**
- Set `PermitRootLogin no` in `/etc/ssh/sshd_config`
- Restart SSH after validating the configuration

**Why it matters**
Direct root login increases risk by exposing the most privileged account to brute-force and credential attacks.

## 2. Disable password-based SSH authentication

**Action**
- Set `PasswordAuthentication no` in `/etc/ssh/sshd_config`
- Require SSH key-based authentication instead

**Why it matters**
SSH keys are significantly harder to brute-force or reuse than weak passwords.

## 3. Create a least-privileged administrative user

**Action**
- Create a named user for administration
- Add the user to the sudo group only if required
- Avoid daily use of privileged accounts

**Why it matters**
This improves accountability and reduces unsafe root usage.

## 4. Configure a host-based firewall

**Action**
- Use UFW to allow only required services such as:
  - `22/tcp` for SSH
  - `80/tcp` for HTTP
  - `443/tcp` for HTTPS
- Deny all other unsolicited inbound traffic

**Why it matters**
Restricting inbound ports reduces attack surface and limits unnecessary exposure.

## 5. Keep the system updated

**Action**
- Run package updates regularly
- Apply security patches promptly
- Enable unattended upgrades where appropriate

**Why it matters**
Unpatched services remain exposed to known vulnerabilities.

## 6. Install brute-force protection

**Action**
- Install and configure Fail2ban for SSH or other exposed services

**Why it matters**
This helps block repeated login attempts from automated attacks.

## 7. Review and disable unnecessary services

**Action**
- Check listening services with `ss -tulpn`
- Disable or remove services that are not required

**Why it matters**
Every unnecessary running service expands the attack surface.

## 8. Monitor authentication and system logs

**Action**
- Review `/var/log/auth.log` and other relevant logs
- Watch for failed logins, sudo usage, and service errors

**Why it matters**
Basic monitoring improves visibility into suspicious access attempts and operational issues.

## 9. Restrict permissions on sensitive files

**Action**
- Secure SSH keys, scripts, and configuration files with appropriate ownership and permissions

**Why it matters**
Weak file permissions can expose credentials or allow privilege misuse.

## 10. Apply layered security in cloud environments

**Action**
- Use cloud security groups in addition to host firewall rules
- Prefer private subnets for internal workloads
- Limit direct public exposure wherever possible

**Why it matters**
Host hardening is stronger when combined with network-level access controls.

## Summary

This baseline hardening guide focuses on reducing attack surface, limiting administrative exposure, and improving visibility. It is intended as a practical lab reference rather than a complete production security standard.
