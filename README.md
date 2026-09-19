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

## Next Phase 

- Detection Engineering
- Custom Wazuh Rules
- Atomic Red Team
- TheHive
- Shufle SOAR
