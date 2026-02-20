# Network Reconnaissance & Port Scan Detection Lab

## Objective
Simulate attacker-style reconnaissance against a Windows 10 virtual machine, identify exposed services, assess associated risks, and implement system hardening measures to reduce attack surface.

---

## Lab Environment

- Attacker Machine: Ubuntu Linux (VirtualBox)
- Target Machine: Windows 10 (VirtualBox)
- Tool Used: Nmap
- Network Configuration: VirtualBox internal network

---

## Initial Reconnaissance

### Command Used

```bash
sudo nmap -sS -sV -T4 <target-ip>
```

### Initial Findings

- 139/tcp open  netbios-ssn
- 445/tcp open  microsoft-ds

The scan revealed exposed SMB and NetBIOS services on the Windows 10 host.

---

## Security Risk Assessment

**Port 445 (SMB)**
- Commonly exploited for lateral movement.
- Frequently targeted by ransomware campaigns.
- Can expose file shares and authentication mechanisms.

**Port 139 (NetBIOS)**
- Legacy protocol used for name resolution and file sharing.
- Can allow network enumeration and information disclosure.

Risk Level: Moderate to High depending on authentication configuration and network segmentation.

---

## Remediation Actions

The following defensive measures were implemented:

- Disabled File and Printer Sharing firewall inbound rules.
- Disabled network discovery and file sharing services.
- Verified firewall policy enforcement through follow-up testing.

---

## Validation

A follow-up Nmap scan was conducted after remediation:

```bash
sudo nmap -sS -sV -T4 <target-ip>
```

Result:
- All scanned ports reported as filtered (no-response).
- Previously exposed SMB and NetBIOS services were no longer externally accessible.

This confirmed successful reduction of the system’s attack surface.

---

## Skills Demonstrated

- Network reconnaissance using Nmap
- Service enumeration and exposure identification
- Security risk assessment
- Windows firewall configuration and hardening
- Remediation validation through re-scanning
- Basic attack surface reduction methodology

---

## Key Takeaway

This lab demonstrates the full defensive lifecycle:
1. Simulate attacker reconnaissance
2. Identify exposed services
3. Assess security risk
4. Implement hardening measures
5. Validate remediation effectiveness

Minimizing unnecessary service exposure is critical to reducing lateral movement opportunities in enterprise environments.
