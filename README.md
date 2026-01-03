Home Lab

A controlled environment built for malware analysis, offensive security testing, and system behavior research. Each system in the lab has a defined role, and the setup is segmented to prevent cross-contamination or accidental exposure.

Host Systems
Lenovo Laptop — Dual Boot (Windows + Linux)
Windows Environment — Malware Analysis

Primary platform for dynamic malware analysis and reverse engineering.

Tools:

IDA

x64dbg

PEStudio

Procmon / Sysmon

Wireshark

Capabilities include malware unpacking and debugging, runtime behavior monitoring, API call tracing, YARA rule creation and validation, controlled detonation, and a snapshot/revert workflow to maintain a clean baseline. This environment is used strictly for executing and debugging Windows malware samples.

Linux Environment — Attack & Utility

A Debian-based environment used for offensive tooling and general-purpose security tasks. It handles network probing and enumeration, payload logic testing (non-malicious), automation and scripting, and hashing, metadata extraction, and log parsing. Offensive tooling is kept fully isolated from malware execution environments.

REMnux Virtual Machine — Malware Analysis & Triage

A dedicated REMnux VM running on VirtualBox, used for static analysis, malware triage, and network artifact extraction. It is the first stage of analysis before escalation to dynamic execution.

Primary uses include strings and import analysis, entropy and packing detection, IOC extraction (IPs, domains, URLs, mutexes, file paths), unpacking and format inspection, PCAP analysis, and tooling such as peframe, floss, capa, radare2, and YARA.

Mac Hardware (Debian Linux) — Bare-Metal Victim & Infrastructure

A repurposed Mac system with macOS wiped and replaced with Debian Linux. This system serves as both a bare-metal victim and a lightweight infrastructure node.

It is used to observe behavior that differs from virtualized environments, evaluate persistence techniques and system-level changes on real hardware, host simulated backend or C2 services, and collect logs and network traffic. The system is physically and network-isolated to prevent unintended spread.

Network Structure

There are no shared folders, clipboards, or device passthroughs between systems. Malware execution occurs only on internal-only network segments. Outbound traffic is blocked unless intentionally simulated. The bare-metal Debian system is physically isolated, and strict firewall rules and snapshot-based safeguards are enforced throughout the lab.

Analysis Workflow

Samples are collected, hashed, and documented before undergoing initial triage in REMnux. Static analysis follows, focusing on strings, imports, entropy, packing indicators, and IOC extraction. Dynamic execution is performed in the Windows analysis environment, with artifacts captured including registry changes, filesystem modifications, dropped files, and network traffic. Indicators of compromise are consolidated, and reports are produced with ATT&CK mapping, detection logic, and YARA rules. All systems are then reverted to a known clean state.

Why This Setup Works

This lab is intentionally simple but highly effective. REMnux provides safe static analysis and early triage. Windows handles execution, debugging, and behavioral analysis. Linux supports offensive tooling and automation. The bare-metal Debian system enables realistic victim testing and infrastructure simulation. Every component has a defined role, nothing is redundant, and the environment remains controlled, isolated, and repeatable.
