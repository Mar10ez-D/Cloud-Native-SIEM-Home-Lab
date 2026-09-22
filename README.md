# Cloud-Native-SIEM-Home-Lab - Phase 1

## Overview

This project documents the deployment of a cloud-native SIEM home lab using:

- Wazuh v4.7.5
- Docker Desktop
- Windows 11
- Sysmon
- Wazuh Agent

The goal is to gain hands-on experience in:

- SIEM operations
- Log collection
- Endpoint Monitoring
- Dectection Engineering
- SOC Analyst Workflow

---

## Architecture

```text
Windows 11
    |
    v
Sysmon
    |
    v
Wazuh Agent
    |
    v
Wazuh Manager
    |
    v
Wazuh Indexer
    |
    v
Wazuh Dashboard
```

## Environment

| Component | Version |
|------------|---------|
| Windows 11 Pro | 10.0.26200 |
| Docker Desktop | 29.8.0 |
| Wazuh | 4.7.5 |
| Sysmon | Installed |
| Wazuh Agent | 4.7.5 |

---

## Depolyment Steps

### Step 1

Install Docker Desktop.

### Step 2

Deploy Wazuh Single-node stack.

### Step 3

Genrerate Wazuh certificates.

### Step 4

Start:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

### Step 5 

Install Windows wazuh Agent.

### Step 6

Install Sysmon

### Step 7

Verify telemetry flow.

---

## Telemetry validation

Test commands executed:

```powershell
whoami

hostname

ipconfig

net user

powershell.exe -enc SQBtACAAdABlAHMAdAA=
```

Observed:

- Process Creation Events
- Process Termination Events
- Windows Security Logs
- Sysmon Event ID 1
- Sysmon Event ID 5

---

## Results

### Wazuh Dashboard

* Dashboard Online

### Wazuh Agent

* WIN11-LAB Connected

### Sysmon

* Running

### Events Collection

* 788+ Events Observed

---

## Challenges Encountered

### Issue 1

Wazuh 5.1.0 Alpha repository used accidentally.

Resolution:

- Switched to wazuh Docker 4.7.5

### Issue 2

Certificate generation failures.

Resolution:

- Regenerated certificates using stable repository.

### Issue 3

Agent registration failure.

Root Cause:

Incorrect Manager IP:

```text
172.168.xx.x
```

Correct Manager IP:

```text
192.168.xx.x
```

Resolution:

Updated:

```xml
<address>192.168.xx.x</address>
```

and restarted Wazuh Agent.

---

## Skills Demonstrated

- Docker Administration
- Container Troubleshooting
- SIEM Deployment
- Wazuh Administration
- Windows Endpoint Monitoring
- Symon Telemetry
- Log Analysis
- Incident Troubleshooting

---

# Cloud-Native SIEM Home Lab - Phase 2

# Detection Engineering

---
# Detection Engineering Level 1

## Use Case

Detect PowerShell execution.

## Data Source

Symon Event ID 1

## Wazuh Built-in Rule

Rule ID: 92057

## Custom Rules

Rule ID: 100500

## Detection Logic

Trigger custom alert whenever built-in PowerShell detection Rule 92027 fires.

```xml
<rule id="100500" level="10">
  <if_sid>92027</if_sid>
  <description>Custom Detection - PowerShell Execution Observed</description>
  <mitre>
    <id>T1059.001</id>
  </mitre>
</rule>
```

## Validation

```powershell
powershell.exe
```

## Result

Custom alert successfully generated.

## MITRE Mapping

T1059.001 - powerShell

### What I Learm

## SIEM Engineering
- deploy Wazuh
- Depoly Agent
- Intgrate Sysmon

## Detection Engineering
- Identify event source
- Analyze JSON fields
- Analyze existing dtections
- Build custom rule
- Test custom rule
- Validate alerts

## SOC Operations
- Investigate PowerShell activity
- Verify Sysmon Event ID 1
- Trace telemetry pipeline

# Detection Engineering Level 2

## Use Case 

Detect Encoded PowerShell Execution

## Data Source
Sysmon Event ID 1

## Parent Rule

92057

## Cutom Rule 

100501

## MITRE ATT&CK

T1059.001 - PowerShell

## Validation

powershell.exe -EncodedCommand SQtACAAdABlAHMAdAA=

## Result

Custom alert successfully generated

## Detection Logic

92057
    |
100501

# Detection Engineering Level 3

## Use Case 

Local Account Discovery Detection

## Technique

MITRE ATT&CK T1087.001

## Parrent Rule

92031

## Custom Rule

100502

## Validation

```powershell
net user
```

## Result

Custom alert generated successfully.

## Detection Logic

92031
    |
100502

# Detection Engineering Level 4

## Use Case

Local Administrators Group Discovery

## MITRE ATT&CK

T1069.001

## Parent Rule

92031

## Custom Rule

100503

## Validation

```powershell
net localgroup administrators
```

## Result

Custom alert generated successfully.

# Next 

# Detection Engineering Level 5
# Host Discovery Detection