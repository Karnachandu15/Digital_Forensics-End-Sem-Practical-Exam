# Experiment : During malware infection use Process Explorer to identify suspicious process activities in the system

## Aim
Describe how Process Explorer aids in isolating suspicious processes during an active infection and documenting findings.

## Forensic Investigation Flow
1. Launch Process Explorer with administrative rights and capture a baseline snapshot.
2. Correlate unfamiliar processes with parent-child relationships, signatures, and virustotal results.
3. Isolate suspect binaries, preserve volatile data, and document observations for reporting.

## Tool Description and Application

### About the tool
Process Explorer is a part of the Microsoft Sysinternals Suite, developed by Mark Russinovich. It provides detailed information about all running processes, threads, and handles on a Windows system — far more than the standard Task Manager. It helps investigators and analysts identify malware, rootkits, or suspicious background tasks that might be hiding in plain sight.

### Application
Process Explorer is a Sysinternals utility that reveals detailed process metadata, thread activity, and DLL usage, helping responders validate trustworthiness and provenance of running components. Its hierarchical view, color-coded status indicators, and integrated VirusTotal lookup streamline triage during volatile acquisition and support post-incident documentation.
Process Explorer continuously updates its data using system-level callbacks. It periodically refreshes every few seconds (user-defined interval) to detect newly spawned processes, terminated ones, or changed process states. This live view allows real-time detection of abnormal process behavior such as repeated spawning, memory spikes, or hidden child processes.
![Execution Screenshot Placeholder 1](<Screenshots\Screenshot 2025-11-12 163050.png>)
Each running process is cross-verified against its executable image file using Windows’ built-in signature verification mechanism. Process Explorer uses APIs like WinVerifyTrust() to check whether the process is signed by a trusted publisher. Unsigned or suspiciously signed processes are highlighted in red or purple, helping analysts quickly spot malware disguised as system processes.
![Execution Screenshot Placeholder 2](<Screenshots\Screenshot (127).png>)
The tool also enumerates all Dynamic Link Libraries (DLLs) loaded by each process using EnumProcessModules(). By comparing these DLLs to standard Windows libraries, the tool helps spot injected or rogue DLLs often used by malware to hijack legitimate processes (e.g., svchost.exe running a non-standard DLL).
VirusTotal Integration 
![Execution Screenshot Placeholder 1](<Screenshots\Screenshot (124).png>)

Process Explorer allows optional integration with VirusTotal, an online malware scanning service. When enabled, it computes a hash (SHA256) of each executable and submits it to VirusTotal’s database to check against known malware samples. The tool then displays a score like “0/70” (clean) or “45/70” (malicious), giving analysts quick threat intelligence.
![Execution Screenshot Placeholder 2](<Screenshots\Screenshot (128).png>)

Color Coding for Quick Identification:
Process Explorer uses colors to categorize processes:
 - Light Blue: New processes created recently.
 - Pink: Services or system processes.
 - Green: New processes just started.
 - Red: Processes that have recently terminated.
 - Purple: Processes running under .NET or special frameworks.
This color visualization helps investigators quickly focus on new or abnormal processes.
![Execution Screenshot Placeholder 2](<Screenshots\Screenshot (126).1.png>)

Process Explorer also allows safe suspension or termination of identified malicious processes. However, during forensic investigations, this is usually avoided to maintain the system's evidence integrity unless the malware poses a live threat.
![Execution Screenshot Placeholder 1](<Screenshots\Screenshots\image.png>)

## Results

Process Explorer successfully identified suspicious processes during the malware infection through color-coded alerts and VirusTotal integration. The tool highlighted unsigned executables and revealed unusual parent-child process relationships, confirming malware presence and enabling effective incident response documentation.



