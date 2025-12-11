 Home Lab

A controlled environment built for malware analysis, offensive security testing, and system behavior research.  
Each machine in this lab has a defined purpose, and the setup is segmented to prevent cross-contamination or accidental exposure.



 Host Systems

Lenovo Laptop — Dual Boot (Windows + Linux)

Windows Environment — Malware Analysis
Used as the primary system for static and dynamic malware analysis.

Toolchain includes:
- IDA  
- x64dbg  
- PEStudio  
- Procmon / Sysmon  
- Wireshark  

Capabilities:
- Unpacking and debugging  
- Behavior monitoring  
- YARA rule creation and testing  
- Isolated networking for detonations  
- Snapshot/revert workflow to maintain a clean baseline  

---

Linux Environment — Attack & Utility
Debian-based environment used for offensive tooling and general utility work.

Tasks handled:
- Network probing and enumeration  
- Payload logic testing (non-malicious)  
- Automation and scripting  
- Hashing, metadata extraction, and log parsing  

Keeps offensive operations fully separated from the Windows analysis side.

---

Mac (High Sierra, 2010) — Victim System
A real hardware target system used for controlled testing scenarios.

Purpose:
- Observe behavior outside a virtualized environment  
- Test samples and tools that behave differently on bare metal  
- Evaluate older OS attack chains and persistence methods  

Physically and network-isolated to prevent unintended spread.

---

Debian CLI Node
A lightweight command-line environment used for:

- Network services  
- Log collection  
- Analysis utilities  
- Running simulated back-end infrastructure  

Provides a predictable, easily resettable backbone for experiments.

---

Network Structure

- No shared folders, clipboard, or device passthrough between systems  
- Internal-only network segments for malware execution  
- Outbound traffic blocked unless intentionally simulated  
- Physical isolation for the Mac victim machine  
- Strict firewall rules and snapshot-based safeguards  

---

Analysis Workflow

1. Sample Intake  
   Collect → hash → record metadata → initial static checks  

2. Static Analysis 
   Strings, imports, sections, obfuscation artifacts  

3. Dynamic Execution 
   Controlled detonation in the Windows analysis environment  

4. Artifact Capture  
   Registry changes, filesystem modifications, dropped files, network traffic  

5. IOC Extraction  
   Hashes, IPs, domains, filepaths, mutexes, behavior indicators  

6. Reporting  
   Write-up creation, ATT&CK mapping, detection logic, YARA rules  

7. Snapshot Revert  
   Reset the environment to a clean, known state  



Why This Setup Works

The lab is intentionally simple but highly functional:

- Windows handles structured malware analysis.  
- Linux handles offensive scripting and tooling.  
- Mac High Sierra serves as a realistic victim for bare-metal testing.  
- Debian CLI provides back-end services and utilities.  

Every component has a role, nothing is arbitrary, and the environment stays controlled, isolated, and repeatable.



