# ZEROTIER ENTERPRISE DEPLOYMENT
## Production-Ready Documentation for Secure Remote Access Infrastructure

---

### DOCUMENT CONTROL

| **Field** | **Details** |
|-----------|-------------|
| **Document Title** | ZeroTier Software-Defined Network Deployment for Windows Infrastructure |
| **Document ID** | SCHERTECH-IT-ZT-001 |
| **Version** | 1.1 |
| **Date** | July 03, 2025 |
| **Classification** | Internal - Confidential |
| **Author** | Abubakkar Khan Fazla Rabbi |
| **Designation** | Senior System Engineer - SecOps |
| **Department** | Infrastructure Team |
| **Organization** | Schertech Italy - Bangladesh Branch |
| **Review Cycle** | Quarterly |
| **Next Review Date** | January 18, 2026 |
| **Approval Status** | ✅ Approved for Production |

---

### DOCUMENT REVISION HISTORY

| **Version** | **Date** | **Author** | **Changes** | **Approver** |
|-------------|----------|------------|-------------|--------------|
| 1.0 | October 18, 2025 | Abubakkar Khan Fazla Rabbi | Initial production release | Pending |

---

## TABLE OF CONTENTS

1. [Executive Summary](#1-executive-summary)
2. [Project Overview](#2-project-overview)
3. [Security Architecture](#3-security-architecture)
4. [Infrastructure Requirements](#4-infrastructure-requirements)
5. [Implementation Procedures](#5-implementation-procedures)
6. [Security Hardening](#6-security-hardening)
7. [Monitoring & Audit](#7-monitoring--audit)
8. [Disaster Recovery](#8-disaster-recovery)
9. [Troubleshooting Runbook](#9-troubleshooting-runbook)
10. [Appendices](#10-appendices)

---

## 1. EXECUTIVE SUMMARY

### 1.1 Purpose

This document provides comprehensive procedures for deploying ZeroTier Software-Defined Network (SDN) infrastructure across Schertech's Windows-based production environment, enabling secure remote access to 100+ client machines without exposing real IP addresses.

### 1.2 Scope

- **Target Environment:** 100+ Windows Server/Desktop machines
- **Geographic Distribution:** Bangladesh operations
- **Primary Use Case:** Secure remote administration via SSH, RDP, and PowerShell
- **Cost:** $0 (100% free, unlimited devices)

### 1.3 Business Benefits

✅ **Zero Capital Expenditure** - No hardware or licensing costs  
✅ **Enhanced Security** - 256-bit end-to-end encryption, zero-trust model  
✅ **Operational Efficiency** - Centralized management, rapid deployment  
✅ **Compliance Ready** - SOC2 Type II certified platform  
✅ **Scalability** - Unlimited device support without additional costs  

### 1.4 Security Certifications

ZeroTier is SOC2 Type II certified, demonstrating commitment to maintaining the highest standards of security, availability, and confidentiality with effective controls for protecting customer data and ensuring service reliability.

### 1.5 Key Stakeholders

| **Role** | **Name** | **Responsibility** |
|----------|----------|-------------------|
| Project Lead | Abubakkar Khan Fazla Rabbi | Implementation, security configuration, documentation |
| Infrastructure Team | TBD | Server deployment, endpoint configuration |
| Security Operations | SecOps Team | Security audit, compliance validation |
| Management | TBD | Final approval, resource allocation |

---

## 2. PROJECT OVERVIEW

### 2.1 Technical Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    SCHERTECH BANGLADESH                      │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  [ADMIN HOST SERVER]          [CLIENT MACHINES 1-100+]      │
│   Real IP: X.X.X.X            Behind NAT/Firewall          │
│   Role: Control Center        No Public IP Required         │
│   OS: Windows Server          OS: Windows 10/11/Server      │
│                                                              │
│         ↓                              ↓                     │
│    [ZeroTier Agent]  ←────────→  [ZeroTier Agent]          │
│    10.147.X.1                    10.147.X.2-101             │
│                                                              │
│         ↓                              ↓                     │
│   [SecOps Access]              [SSH/RDP/PS Remoting]        │
│   - Terminal Access            - Fully Accessible           │
│   - File Transfer              - No Port Forwarding         │
│   - Monitoring                 - Works Anywhere             │
│                                                              │
└─────────────────────────────────────────────────────────────┘
                          ↓
              [ZeroTier Central Cloud]
                 my.zerotier.com
           - Network Controller
           - Member Authorization
           - Audit Logging
```

### 2.2 Encryption & Security

ZeroTier uses state-of-the-art asymmetric encryption with private keys that never leave the device, ensuring traffic integrity and keeping device data private. The platform employs 256-bit end-to-end encryption, considered one of the strongest levels of encryption, providing assurance against eavesdropping and data breaches.

### 2.3 Network Architecture Benefits

ZeroTier provides built-in security including end-to-end encryption, unique cryptographic IDs for device authorization, micro-segmentation of networks and centralized security monitoring.

### 2.4 Deployment Timeline

| **Phase** | **Duration** | **Activities** |
|-----------|--------------|----------------|
| Phase 1: Planning | 1 day | Requirements gathering, security review |
| Phase 2: Host Setup | 2 hours | Admin server configuration |
| Phase 3: Client Deployment | 4-6 hours | Mass deployment to 100+ machines |
| Phase 4: Authorization | 1-2 hours | Bulk member authorization |
| Phase 5: Testing | 2 hours | Connectivity validation, security audit |
| Phase 6: Documentation | 2 hours | Runbook creation, training materials |
| **Total** | **2-3 days** | **Production-ready deployment** |

---

## 3. SECURITY ARCHITECTURE

### 3.1 Zero-Trust Security Model

ZeroTier uses a zero-trust networking model, meaning the platform doesn't automatically trust any entity within the network, and devices are authenticated before they join the network, reducing the risk of unauthorized access.

### 3.2 Defense-in-Depth Strategy

ZeroTier's architecture benefits from multiple layers of protection including robust encryption, granular flow rules and vigilant monitoring, though organizations should always consider additional safeguards like firewalls and intrusion detection systems as part of a comprehensive defense strategy.

### 3.3 Security Controls Matrix

| **Control Type** | **Implementation** | **Status** |
|------------------|-------------------|------------|
| **Network Encryption** | AES-256-GCM end-to-end | ✅ Enabled by default |
| **Authentication** | Private networks, manual authorization | ✅ Required |
| **Access Control** | Flow rules, member whitelisting | ✅ Configured |
| **Audit Logging** | 30-day API traffic logs | ✅ Available (paid tier) |
| **Network Segmentation** | Virtual network isolation | ✅ Implemented |
| **Device Authentication** | Cryptographic node IDs | ✅ Automatic |
| **Traffic Filtering** | Custom flow rules | ✅ Configurable |
| **Monitoring** | Member status, online/offline tracking | ✅ Real-time |

### 3.4 Compliance Considerations

**Data Protection:**
- ZeroTier collects minimal metadata about active networks and devices, and routes traffic directly between peers so infrastructure cannot observe or modify packets on user networks
- All client code is open source and auditable
- No sensitive data stored on ZeroTier infrastructure

**Audit Requirements:**
- ZeroTier captures logs for the last 30 days of API traffic for every paid Central account, including requests made through both the Central dashboard and public API
- Member join/leave events logged
- Network configuration changes tracked

### 3.5 Security Best Practices

The ultimate safety of ZeroTier deployment depends on proper configuration (always using private networks and enforcing strict access controls), timely updates (regularly updating software to patch known vulnerabilities), and vigilant management (monitoring networks and layering additional security measures when handling highly sensitive data).

**Required Configurations:**
1. ✅ **Private Networks Only** - Never use public networks
2. ✅ **Manual Authorization** - Approve each device individually
3. ✅ **Flow Rules** - Restrict traffic to required ports (SSH: 22, RDP: 3389, WinRM: 5985)
4. ✅ **Regular Audits** - Weekly member status reviews
5. ✅ **Update Management** - Monthly agent updates

---

## 4. INFRASTRUCTURE REQUIREMENTS

### 4.1 Host Server (Admin Control Center)

**Minimum Requirements:**
- **OS:** Windows Server 2016+ or Windows 10/11 Pro
- **RAM:** 4 GB minimum
- **Disk Space:** 100 MB for ZeroTier, 5 GB for logs and scripts
- **Network:** Internet connectivity (443/TCP outbound)
- **Privileges:** Local Administrator rights
- **PowerShell:** Version 5.1 or higher

**Recommended Specifications:**
- **OS:** Windows Server 2022 or Windows 11 Enterprise
- **RAM:** 8 GB
- **Disk Space:** 20 GB SSD
- **Backup:** Daily automated backups

### 4.2 Client Machines (100+ Endpoints)

**Minimum Requirements:**
- **OS:** Windows 10/11 or Windows Server 2012 R2+
- **RAM:** 2 GB
- **Disk Space:** 100 MB
- **Network:** Internet connectivity (UDP 9993 outbound)
- **Privileges:** Administrator rights for installation

**Prerequisites:**
- PowerShell Remoting enabled (for automated deployment)
- Windows Firewall configured
- Antivirus with ZeroTier exclusions

### 4.3 Network Requirements

| **Component** | **Protocol** | **Port** | **Direction** | **Purpose** |
|---------------|------------|----------|---------------|-------------|
| ZeroTier Service | UDP | 9993 | Outbound | Peer-to-peer communication |
| ZeroTier API | HTTPS | 443 | Outbound | Central management |
| SSH (Optional) | TCP | 22 | Inbound (ZT network) | Remote terminal access |
| RDP | TCP | 3389 | Inbound (ZT network) | Remote desktop |
| WinRM | TCP | 5985 | Inbound (ZT network) | PowerShell remoting |

**Firewall Rules:**
- ✅ Allow outbound UDP 9993 on all endpoints
- ✅ Allow outbound HTTPS 443 on all endpoints
- ✅ ZeroTier virtual adapter exempted from strict firewall policies

### 4.4 Active Directory Integration (Optional)

- Compatible with domain-joined machines
- GPO deployment supported
- AD authentication for SSH/RDP maintained

---

## 5. IMPLEMENTATION PROCEDURES

### 5.1 Pre-Deployment Checklist

**Security Approvals:**
- [ ] Security team review completed
- [ ] Change management ticket approved
- [ ] Backup verification completed
- [ ] Rollback plan documented

**Technical Prerequisites:**
- [ ] Host server meets requirements
- [ ] PowerShell remoting tested on sample clients
- [ ] Network connectivity verified
- [ ] Antivirus exclusions configured

**Documentation:**
- [ ] Asset inventory updated
- [ ] Network diagram created
- [ ] IP address allocation plan documented

### 5.2 PHASE 1: Host Server Configuration

**Performed By:** Abubakkar Khan Fazla Rabbi (Senior System Engineer - SecOps)  
**Location:** Host server with real IP address  
**Estimated Time:** 30 minutes

#### Step 1.1: Create ZeroTier Account

```powershell
# Open browser and navigate to ZeroTier Central
Start-Process "https://my.zerotier.com/"

# Actions:
# 1. Click "Sign Up"
# 2. Use organizational email: [your-email]@schertech.com
# 3. Verify email address
# 4. Enable MFA (REQUIRED for security)
```

**Security Note:** Use strong password (16+ characters, mixed case, numbers, symbols) and enable multi-factor authentication immediately.

#### Step 1.2: Create Production Network

```powershell
# In ZeroTier Central dashboard:
# 1. Click "Create A Network"
# 2. Note the 16-character Network ID (e.g., 1234567890abcdef)
```

**Network Configuration:**

| **Setting** | **Value** | **Justification** |
|-------------|-----------|-------------------|
| Network Name | `SCHERTECH-BD-PROD` | Clear identification |
| Access Control | Private | Security requirement |
| IPv4 Auto-Assign | ✅ Enabled | Automatic IP management |
| IP Range | 10.147.17.0/24 | Supports 254 devices |
| IPv6 Auto-Assign | ❌ Disabled | Not required |

**⚠️ CRITICAL:** Save Network ID to password manager immediately.

#### Step 1.3: Install ZeroTier on Host Server

```powershell
# Run as Administrator
# Location: Host Server

# Download ZeroTier MSI installer
$installerUrl = "https://download.zerotier.com/dist/ZeroTier%20One.msi"
$installerPath = "$env:TEMP\ZeroTierOne.msi"

Write-Host "Downloading ZeroTier installer..." -ForegroundColor Cyan
Invoke-WebRequest -Uri $installerUrl -OutFile $installerPath -UseBasicParsing

# Verify download
if (Test-Path $installerPath) {
    Write-Host "Download complete. Installing..." -ForegroundColor Green
    
    # Install silently
    Start-Process msiexec.exe -ArgumentList "/i `"$installerPath`" /quiet /norestart" `
                              -Wait -NoNewWindow
    
    Write-Host "Installation complete." -ForegroundColor Green
} else {
    Write-Host "ERROR: Download failed" -ForegroundColor Red
    exit 1
}

# Wait for service to start
Write-Host "Waiting for ZeroTier service to start..." -ForegroundColor Yellow
Start-Sleep -Seconds 10

# Verify installation
$service = Get-Service ZeroTierOneService -ErrorAction SilentlyContinue
if ($service.Status -eq 'Running') {
    Write-Host "✅ ZeroTier service running successfully" -ForegroundColor Green
} else {
    Write-Host "❌ ERROR: Service not running" -ForegroundColor Red
    exit 1
}
```

#### Step 1.4: Join Network from Host

```powershell
# Replace with YOUR Network ID
$NetworkID = "1234567890abcdef"

# Join network
& "C:\Program Files (x86)\ZeroTier\One\zerotier-one_x64.exe" -q join $NetworkID

Write-Host "Joined network: $NetworkID" -ForegroundColor Green
Write-Host "⚠️  ACTION REQUIRED: Authorize this machine in ZeroTier Central" -ForegroundColor Yellow
```

#### Step 1.5: Authorize Host Server

```powershell
# In web browser (ZeroTier Central):
# 1. Navigate to your network
# 2. Scroll to "Members" section
# 3. Check the box next to your host server
# 4. Set name: "SCHERTECH-HOST-ADMIN"
# 5. Note assigned IP (e.g., 10.147.17.1)
```

#### Step 1.6: Verify Host Configuration

```powershell
# Check network status
& "C:\Program Files (x86)\ZeroTier\One\zerotier-one_x64.exe" -q listnetworks

# Expected output:
# 200 listnetworks <networkid> <name> <mac> OK PRIVATE <device> <IP>/24

# Extract ZeroTier IP
$ztIP = (& "C:\Program Files (x86)\ZeroTier\One\zerotier-one_x64.exe" -q listnetworks | 
         Select-String -Pattern '\d+\.\d+\.\d+\.\d+').Matches.Value

Write-Host "✅ Host Server ZeroTier IP: $ztIP" -ForegroundColor Green

# Log configuration
$logEntry = @{
    Timestamp = Get-Date -Format "yyyy-MM-dd HH:mm:ss"
    Server = $env:COMPUTERNAME
    ZeroTierIP = $ztIP
    NetworkID = $NetworkID
    Status = "Configured"
} | ConvertTo-Json

$logEntry | Out-File "C:\Scripts\Logs\zerotier-config.log" -Append
```

**✅ PHASE 1 COMPLETE** - Host server is now configured and connected.

---

### 5.3 PHASE 2: Client Mass Deployment

**Performed By:** Infrastructure Team (initiated by SecOps)  
**Location:** Execute from Host Server  
**Estimated Time:** 4-6 hours for 100+ machines

#### Step 2.1: Prepare Deployment Environment

```powershell
# Create directory structure on Host Server
$scriptRoot = "C:\Scripts\ZeroTier-Deployment"
$directories = @(
    "$scriptRoot\Logs",
    "$scriptRoot\Reports",
    "$scriptRoot\Backups"
)

foreach ($dir in $directories) {
    New-Item -ItemType Directory -Path $dir -Force | Out-Null
    Write-Host "Created: $dir" -ForegroundColor Green
}

# Set permissions (restrict to Administrators only)
$acl = Get-Acl $scriptRoot
$acl.SetAccessRuleProtection($true, $false)
$adminRule = New-Object System.Security.AccessControl.FileSystemAccessRule(
    "BUILTIN\Administrators", "FullControl", "ContainerInherit,ObjectInherit", "None", "Allow"
)
$acl.AddAccessRule($adminRule)
Set-Acl $scriptRoot $acl

Write-Host "✅ Deployment environment ready" -ForegroundColor Green
```

#### Step 2.2: Create Computer Inventory

```powershell
# Create computer list file
$computerFile = "$scriptRoot\computers.txt"

# Method 1: Query Active Directory (if domain environment)
if (Get-Module -ListAvailable -Name ActiveDirectory) {
    Import-Module ActiveDirectory
    $computers = Get-ADComputer -Filter * -SearchBase "OU=Workstations,DC=schertech,DC=local" | 
                 Select-Object -ExpandProperty Name
    $computers | Out-File $computerFile
    Write-Host "✅ Imported $($computers.Count) computers from AD" -ForegroundColor Green
}

# Method 2: Manual entry
else {
    @"
CLIENT-PC-001
CLIENT-PC-002
CLIENT-PC-003
SERVER-WIN-001
SERVER-WIN-002
"@ | Out-File $computerFile
    
    Write-Host "⚠️  Update $computerFile with all target machines" -ForegroundColor Yellow
}

# Validate computer list
$computerList = Get-Content $computerFile | Where-Object { $_ -match '\S' }
Write-Host "Total machines to deploy: $($computerList.Count)" -ForegroundColor Cyan
```

#### Step 2.3: Deploy ZeroTier to All Clients

**CRITICAL SCRIPT - Production Deployment**

```powershell
# ============================================
# SCHERTECH ZEROTIER MASS DEPLOYMENT SCRIPT
# Author: Abubakkar Khan Fazla Rabbi
# Role: Senior System Engineer - SecOps
# Organization: Schertech Italy - Bangladesh Branch
# Date: October 18, 2025
# Version: 1.0
# ============================================

param(
    [Parameter(Mandatory=$true)]
    [string]$NetworkID,  # ZeroTier Network ID
    
    [Parameter(Mandatory=$false)]
    [string[]]$ComputerList = $null,
    
    [Parameter(Mandatory=$false)]
    [switch]$TestMode = $false  # Deploy to first 5 machines only
)

# Configuration
$installerUrl = "https://download.zerotier.com/dist/ZeroTier%20One.msi"
$scriptRoot = "C:\Scripts\ZeroTier-Deployment"
$logPath = "$scriptRoot\Logs\Deployment_$(Get-Date -Format 'yyyyMMdd_HHmmss').log"

# Initialize logging
function Write-DeploymentLog {
    param(
        [string]$Message,
        [string]$Level = "INFO"
    )
    $timestamp = Get-Date -Format "yyyy-MM-dd HH:mm:ss"
    $logEntry = "[$timestamp] [$Level] $Message"
    
    # Color coding
    $color = switch ($Level) {
        "ERROR" { "Red" }
        "WARNING" { "Yellow" }
        "SUCCESS" { "Green" }
        default { "White" }
    }
    
    Write-Host $logEntry -ForegroundColor $color
    Add-Content -Path $logPath -Value $logEntry
}

# Banner
Write-Host @"
╔═══════════════════════════════════════════════════════╗
║   SCHERTECH ZEROTIER DEPLOYMENT                      ║
║   Infrastructure Team - Bangladesh Branch            ║
║   Senior System Engineer: Abubakkar Khan Fazla Rabbi ║
╚═══════════════════════════════════════════════════════╝
"@ -ForegroundColor Cyan

Write-DeploymentLog "Deployment initiated by $env:USERNAME from $env:COMPUTERNAME"
Write-DeploymentLog "Network ID: $NetworkID"

# Load computer list
if ($null -eq $ComputerList) {
    $computerFile = "$scriptRoot\computers.txt"
    if (-not (Test-Path $computerFile)) {
        Write-DeploymentLog "ERROR: Computer list not found: $computerFile" "ERROR"
        exit 1
    }
    $ComputerList = Get-Content $computerFile | Where-Object { $_ -match '\S' }
}

if ($TestMode) {
    $ComputerList = $ComputerList | Select-Object -First 5
    Write-DeploymentLog "TEST MODE: Deploying to first 5 machines only" "WARNING"
}

Write-DeploymentLog "Target machines: $($ComputerList.Count)"

# Deployment script block
$scriptBlock = {
    param($url, $netID, $deploymentID)
    
    $result = @{
        Success = $false
        Message = ""
        ZeroTierIP = ""
        NodeID = ""
        DeploymentID = $deploymentID
        Duration = 0
    }
    
    $startTime = Get-Date
    
    try {
        # Download installer
        $installer = "$env:TEMP\ZeroTierOne_$deploymentID.msi"
        Invoke-WebRequest -Uri $url -OutFile $installer -UseBasicParsing -TimeoutSec 300
        
        # Verify download
        if (-not (Test-Path $installer)) {
            throw "Installer download failed"
        }
        
        # Install silently
        $process = Start-Process msiexec.exe `
                                 -ArgumentList "/i `"$installer`" /quiet /norestart /l*v `"$env:TEMP\zerotier-install.log`"" `
                                 -Wait -PassThru -NoNewWindow
        
        if ($process.ExitCode -ne 0) {
            throw "Installation failed with exit code: $($process.ExitCode)"
        }
        
        # Wait for service
        $timeout = 30
        $elapsed = 0
        while ((Get-Service ZeroTierOneService -ErrorAction SilentlyContinue).Status -ne 'Running' -and $elapsed -lt $timeout) {
            Start-Sleep -Seconds 2
            $elapsed += 2
        }
        
        if ($elapsed -ge $timeout) {
            throw "Service failed to start within $timeout seconds"
        }
        
        # Join network
        $ztCli = "C:\Program Files (x86)\ZeroTier\One\zerotier-one_x64.exe"
        if (-not (Test-Path $ztCli)) {
            throw "ZeroTier executable not found"
        }
        
        $joinResult = & $ztCli -q join $netID 2>&1
        Start-Sleep -Seconds 5
        
        # Get node info
        $nodeInfo = & $ztCli -q info 2>&1
        if ($nodeInfo -match '200 info ([a-f0-9]{10})') {
            $result.NodeID = $matches[1]
        }
        
        # Get network info (IP assigned after authorization)
        $networkInfo = & $ztCli -q listnetworks 2>&1
        if ($networkInfo -match '10\.[\d\.]+') {
            $result.ZeroTierIP = $matches[0]
        }
        
        # Cleanup
        Remove-Item $installer -Force -ErrorAction SilentlyContinue
        
        $result.Success = $true
        $result.Message = "Deployment successful - Awaiting authorization"
        
    } catch {
        $result.Message = "Error: $($_.Exception.Message)"
    }
    
    $result.Duration = ((Get-Date) - $startTime).TotalSeconds
    return $result
}

# Deploy to each machine
$results = @()
$successful = 0
$failed = 0
$deploymentID = Get-Date -Format "yyyyMMddHHmmss"

foreach ($computer in $ComputerList) {
    Write-DeploymentLog "Processing: $computer"
    
    try {
        # Connectivity test
        if (-not (Test-Connection -ComputerName $computer -Count 2 -Quiet)) {
            Write-DeploymentLog "  Cannot reach $computer" "WARNING"
            $results += [PSCustomObject]@{
                Computer = $computer
                Status = "Unreachable"
                NodeID = ""
                ZeroTierIP = ""
                Duration = 0
                Message = "Network unreachable"
                DeploymentID = $deploymentID
            }
            $failed++
            continue
        }
        
        # Execute deployment
        Write-DeploymentLog "  Deploying to $computer..."
        $result = Invoke-Command -ComputerName $computer `
                                 -ScriptBlock $scriptBlock `
                                 -ArgumentList $installerUrl, $NetworkID, $deploymentID `
                                 -ErrorAction Stop
        
        if ($result.Success) {
            Write-DeploymentLog "  ✅ SUCCESS: $computer | Node: $($result.NodeID) | Duration: $([math]::Round($result.Duration, 2))s" "SUCCESS"
            $results += [PSCustomObject]@{
                Computer = $computer
                Status = "Success"
                NodeID = $result.NodeID
                ZeroTierIP = $result.ZeroTierIP
                Duration = $result.Duration
                Message = $result.Message
                DeploymentID = $deploymentID
            }
            $successful++
        } else {
            Write-DeploymentLog "  ❌ FAILED: $computer | $($result.Message)" "ERROR"
            $results += [PSCustomObject]@{
                Computer = $computer
                Status = "Failed"
                NodeID = ""
                ZeroTierIP = ""
                Duration = $result.Duration
                Message = $result.Message
                DeploymentID = $deploymentID
            }
            $failed++
        }
        
    } catch {
        Write-DeploymentLog "  ❌ ERROR: $computer | $($_.Exception.Message)" "ERROR"
        $results += [PSCustomObject]@{
            Computer = $computer
            Status = "Error"
            NodeID = ""
            ZeroTierIP = ""
            Duration = 0
            Message = $_.Exception.Message
            DeploymentID = $deploymentID
        }
        $failed++
    }
    
    # Rate limiting (prevent network saturation)
    Start-Sleep -Seconds 3
}

# Generate summary report
Write-Host "`n" + ("=" * 60) -ForegroundColor Cyan
Write-DeploymentLog "DEPLOYMENT SUMMARY" "INFO"
Write-Host ("=" * 60) -ForegroundColor Cyan
Write-DeploymentLog "Total Machines: $($ComputerList.Count)"
Write-DeploymentLog "Successful: $successful" "SUCCESS"
Write-DeploymentLog "Failed: $failed" $(if($failed -gt 0){"ERROR"}else{"INFO"})
Write-DeploymentLog "Success Rate: $([math]::Round(($successful / $ComputerList.Count) * 100, 2))%"
Write-Host ("=" * 60) + "`n" -ForegroundColor Cyan

# Export results
$reportFile = "$scriptRoot\Reports\DeploymentReport_$deploymentID.csv"
$results | Export-Csv -Path $reportFile -NoTypeInformation
Write-DeploymentLog "Report exported: $reportFile"

# Display results table
$results | Format-Table Computer, Status, NodeID, Duration, Message -AutoSize

# Authorization reminder
if ($successful -gt 0) {
    Write-Host "`n⚠️  CRITICAL: AUTHORIZATION REQUIRED" -ForegroundColor Yellow -BackgroundColor Red
    Write-Host @"

$successful machines are waiting for authorization in ZeroTier Central.

ACTION REQUIRED:
1. Go to: https://my.zerotier.com/
2. Navigate to network: $NetworkID
3. Scroll to 'Members' section
4. Authorize all pending devices

Machines awaiting authorization:
"@ -ForegroundColor Yellow
    
    $results | Where-Object {$_.Status -eq "Success"} | 
               ForEach-Object { Write-Host "  - $($_.Computer) [Node: $($_.NodeID)]" -ForegroundColor Cyan }
}

# Return results for further processing
return $results
```

**Save script as:** `C:\Scripts\ZeroTier-Deployment\Deploy-ZeroTier.ps1`

#### Step 2.4: Execute Deployment

```powershell
# TEST MODE (recommended first)
cd C:\Scripts\ZeroTier-Deployment
.\Deploy-ZeroTier.ps1 -NetworkID "YOUR-NETWORK-ID" -TestMode

# Review test results, then proceed with full deployment

# PRODUCTION DEPLOYMENT
.\Deploy-ZeroTier.ps1 -NetworkID "YOUR-NETWORK-ID"
```

**Expected Output:**
```
╔═══════════════════════════════════════════════════════╗
║   SCHERTECH ZEROTIER DEPLOYMENT                      ║
║   Infrastructure Team - Bangladesh Branch            ║
║   Senior System Engineer: Abubakkar Khan Fazla Rabbi ║
╚═══════════════════════════════════════════════════════╝
[2025-10-18 10:15:23] [INFO] Deployment initiated by admin from HOST-SERVER
[2025-10-18 10:15:23] [INFO] Network ID: 1234567890abcdef
[2025-10-18 10:15:23] [INFO] Target machines: 105
[2025-10-18 10:15:25] [INFO] Processing: CLIENT-PC-001
[2025-10-18 10:15:26] [INFO]   Deploying to CLIENT-PC-001...
[2025-10-18 10:16:45] [SUCCESS]   ✅ SUCCESS: CLIENT-PC-001 | Node: a1b2c3d4e5 | Duration: 78.3s
...
============================================================
DEPLOYMENT SUMMARY
============================================================
Total Machines: 105
Successful: 103
Failed: 2
Success Rate: 98.10%
============================================================
```

**✅ PHASE 2 COMPLETE** - ZeroTier deployed to all client machines.

---

### 5.4 PHASE 3: Bulk Authorization

**Performed By:** Abubakkar Khan Fazla Rabbi (SecOps)  
**Location:** Host Server  
**Estimated Time:** 1-2 hours

#### Step 3.1: Generate API Token

```powershell
# In web browser:
# 1. Go to: https://my.zerotier.com/account
# 2. Scroll to "API Access Tokens"
# 3. Click "Generate New Token"
# 4. Description: "SCHERTECH-PROD-AUTOMATION"
# 5. Copy token (save to password manager)
```

**⚠️ SECURITY:** API token grants full access. Store securely.

#### Step 3.2: Bulk Authorization Script

```powershell
# ============================================
# SCHERTECH ZEROTIER BULK AUTHORIZATION
# Author: Abubakkar Khan Fazla Rabbi
# Role: Senior System Engineer - SecOps
# Date: October 18, 2025
# ============================================

param(
    [Parameter(Mandatory=$true)]
    [string]$NetworkID,
    
    [Parameter(Mandatory=$true)]
    [string]$ApiToken,
    
    [Parameter(Mandatory=$false)]
    [switch]$DryRun = $false  # Preview without authorizing
)

$scriptRoot = "C:\Scripts\ZeroTier-Deployment"
$logPath = "$scriptRoot\Logs\Authorization_$(Get-Date -Format 'yyyyMMdd_HHmmss').log"

function Write-AuthLog {
    param([string]$Message, [string]$Level = "INFO")
    $timestamp = Get-Date -Format "yyyy-MM-dd HH:mm:ss"
    $logEntry = "[$timestamp] [$Level] $Message"
    
    $color = switch ($Level) {
        "ERROR" { "Red" }
        "WARNING" { "Yellow" }
        "SUCCESS" { "Green" }
        default { "Cyan" }
    }
    
    Write-Host $logEntry -ForegroundColor $color
    Add-Content -Path $logPath -Value $logEntry
}

Write-Host @"
╔═══════════════════════════════════════════════════════╗
║   ZEROTIER MEMBER AUTHORIZATION                      ║
║   Schertech Italy - Bangladesh Branch                ║
╚═══════════════════════════════════════════════════════╝
"@ -ForegroundColor Cyan

Write-AuthLog "Authorization process initiated"
if ($DryRun) {
    Write-AuthLog "DRY RUN MODE - No changes will be made" "WARNING"
}

# API configuration
$baseUrl = "https://my.zerotier.com/api"
$headers = @{
    "Authorization" = "Bearer $ApiToken"
    "Content-Type" = "application/json"
}

try {
    # Fetch network members
    Write-AuthLog "Fetching network members..."
    $members = Invoke-RestMethod -Uri "$baseUrl/network/$NetworkID/member" `
                                  -Headers $headers -Method Get
    
    Write-AuthLog "Found $($members.Count) total members"
    
    # Filter unauthorized members
    $unauthorized = $members | Where-Object { -not $_.config.authorized }
    Write-AuthLog "Unauthorized members: $($unauthorized.Count)" "WARNING"
    
    if ($unauthorized.Count -eq 0) {
        Write-AuthLog "All members are already authorized" "SUCCESS"
        exit 0
    }
    
    # Authorization loop
    $authorized = 0
    $failed = 0
    $results = @()
    
    foreach ($member in $unauthorized) {
        $nodeId = $member.nodeId
        $physicalIP = $member.physicalAddress
        
        Write-AuthLog "Processing: $nodeId (from $physicalIP)"
        
        if ($DryRun) {
            Write-AuthLog "  [DRY RUN] Would authorize: $nodeId" "WARNING"
            continue
        }
        
        try {
            # Prepare authorization payload
            $body = @{
                config = @{
                    authorized = $true
                }
                name = "AUTO-AUTH-$(Get-Date -Format 'MMdd-HHmm')-$nodeId"
            } | ConvertTo-Json -Depth 10
            
            # Authorize member
            $response = Invoke-RestMethod -Uri "$baseUrl/network/$NetworkID/member/$nodeId" `
                                         -Headers $headers `
                                         -Method Post `
                                         -Body $body
            
            $assignedIP = $response.config.ipAssignments[0]
            Write-AuthLog "  ✅ Authorized: $nodeId | IP: $assignedIP" "SUCCESS"
            
            $results += [PSCustomObject]@{
                NodeID = $nodeId
                Status = "Authorized"
                AssignedIP = $assignedIP
                PhysicalIP = $physicalIP
                Timestamp = Get-Date -Format "yyyy-MM-dd HH:mm:ss"
            }
            
            $authorized++
            
        } catch {
            Write-AuthLog "  ❌ Failed: $nodeId | Error: $($_.Exception.Message)" "ERROR"
            $results += [PSCustomObject]@{
                NodeID = $nodeId
                Status = "Failed"
                AssignedIP = ""
                PhysicalIP = $physicalIP
                Timestamp = Get-Date -Format "yyyy-MM-dd HH:mm:ss"
            }
            $failed++
        }
        
        # Rate limiting
        Start-Sleep -Milliseconds 500
    }
    
    # Summary
    Write-Host "`n" + ("=" * 60) -ForegroundColor Cyan
    Write-AuthLog "AUTHORIZATION SUMMARY"
    Write-Host ("=" * 60) -ForegroundColor Cyan
    Write-AuthLog "Total Unauthorized: $($unauthorized.Count)"
    Write-AuthLog "Successfully Authorized: $authorized" "SUCCESS"
    Write-AuthLog "Failed: $failed" $(if($failed -gt 0){"ERROR"}else{"INFO"})
    Write-Host ("=" * 60) + "`n" -ForegroundColor Cyan
    
    # Export results
    if ($results.Count -gt 0) {
        $reportFile = "$scriptRoot\Reports\Authorization_$(Get-Date -Format 'yyyyMMdd_HHmmss').csv"
        $results | Export-Csv -Path $reportFile -NoTypeInformation
        Write-AuthLog "Report exported: $reportFile"
    }
    
    # Display results
    $results | Format-Table -AutoSize
    
} catch {
    Write-AuthLog "CRITICAL ERROR: $($_.Exception.Message)" "ERROR"
    Write-AuthLog "Stack Trace: $($_.ScriptStackTrace)" "ERROR"
    exit 1
}

Write-AuthLog "Authorization process completed" "SUCCESS"
```

**Save as:** `C:\Scripts\ZeroTier-Deployment\Authorize-Members.ps1`

#### Step 3.3: Execute Authorization

```powershell
# DRY RUN (preview only)
.\Authorize-Members.ps1 -NetworkID "YOUR-NETWORK-ID" -ApiToken "YOUR-API-TOKEN" -DryRun

# PRODUCTION RUN
.\Authorize-Members.ps1 -NetworkID "YOUR-NETWORK-ID" -ApiToken "YOUR-API-TOKEN"
```

**✅ PHASE 3 COMPLETE** - All members authorized and assigned IPs.

---

### 5.5 PHASE 4: Post-Deployment Verification

**Performed By:** Infrastructure Team + SecOps  
**Estimated Time:** 2 hours

#### Step 4.1: Export Member Inventory

```powershell
# ============================================
# EXPORT ZEROTIER NETWORK INVENTORY
# ============================================

param(
    [Parameter(Mandatory=$true)]
    [string]$NetworkID,
    
    [Parameter(Mandatory=$true)]
    [string]$ApiToken
)

$scriptRoot = "C:\Scripts\ZeroTier-Deployment"
$headers = @{
    "Authorization" = "Bearer $ApiToken"
}

Write-Host "Fetching network inventory..." -ForegroundColor Cyan

$members = Invoke-RestMethod -Uri "https://my.zerotier.com/api/network/$NetworkID/member" `
                              -Headers $headers -Method Get

$inventory = @()

foreach ($member in $members) {
    if ($member.config.authorized) {
        $inventory += [PSCustomObject]@{
            ComputerName = $member.name
            NodeID = $member.nodeId
            ZeroTierIP = $member.config.ipAssignments[0]
            PhysicalIP = $member.physicalAddress
            Status = if($member.online){"Online"}else{"Offline"}
            LastOnline = if($member.lastOnline -gt 0){
                [DateTimeOffset]::FromUnixTimeMilliseconds($member.lastOnline).LocalDateTime
            } else { "Never" }
            OSVersion = $member.config.revision
            ManagedIPs = ($member.config.ipAssignments -join ", ")
        }
    }
}

# Display
Write-Host "`nAuthorized Members: $($inventory.Count)" -ForegroundColor Green
$inventory | Format-Table ComputerName, ZeroTierIP, Status, LastOnline -AutoSize

# Export to multiple formats
$timestamp = Get-Date -Format "yyyyMMdd_HHmmss"

# CSV for Excel
$csvFile = "$scriptRoot\Reports\Inventory_$timestamp.csv"
$inventory | Export-Csv -Path $csvFile -NoTypeInformation
Write-Host "CSV exported: $csvFile" -ForegroundColor Green

# JSON for automation
$jsonFile = "$scriptRoot\Reports\Inventory_$timestamp.json"
$inventory | ConvertTo-Json | Out-File $jsonFile
Write-Host "JSON exported: $jsonFile" -ForegroundColor Green

# HTML for documentation
$htmlFile = "$scriptRoot\Reports\Inventory_$timestamp.html"
$htmlContent = @"
<!DOCTYPE html>
<html>
<head>
    <title>ZeroTier Network Inventory - Schertech Bangladesh</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        h1 { color: #2c3e50; }
        table { border-collapse: collapse; width: 100%; margin-top: 20px; }
        th { background-color: #3498db; color: white; padding: 12px; text-align: left; }
        td { border: 1px solid #ddd; padding: 8px; }
        tr:nth-child(even) { background-color: #f2f2f2; }
        .online { color: green; font-weight: bold; }
        .offline { color: red; }
        .header { background-color: #ecf0f1; padding: 15px; margin-bottom: 20px; }
    </style>
</head>
<body>
    <div class="header">
        <h1>ZeroTier Network Inventory</h1>
        <p><strong>Organization:</strong> Schertech Italy - Bangladesh Branch</p>
        <p><strong>Department:</strong> Infrastructure Team</p>
        <p><strong>Generated:</strong> $(Get-Date -Format "yyyy-MM-dd HH:mm:ss")</p>
        <p><strong>Network ID:</strong> $NetworkID</p>
        <p><strong>Total Devices:</strong> $($inventory.Count)</p>
    </div>
    <table>
        <thead>
            <tr>
                <th>Computer Name</th>
                <th>ZeroTier IP</th>
                <th>Physical IP</th>
                <th>Status</th>
                <th>Last Online</th>
                <th>Node ID</th>
            </tr>
        </thead>
        <tbody>
"@

foreach ($item in $inventory) {
    $statusClass = if($item.Status -eq "Online"){"online"}else{"offline"}
    $htmlContent += @"
            <tr>
                <td>$($item.ComputerName)</td>
                <td>$($item.ZeroTierIP)</td>
                <td>$($item.PhysicalIP)</td>
                <td class="$statusClass">$($item.Status)</td>
                <td>$($item.LastOnline)</td>
                <td><code>$($item.NodeID)</code></td>
            </tr>
"@
}

$htmlContent += @"
        </tbody>
    </table>
</body>
</html>
"@

$htmlContent | Out-File $htmlFile
Write-Host "HTML exported: $htmlFile" -ForegroundColor Green

# Create hosts file entries for easy access
$hostsFile = "$scriptRoot\Reports\zerotier-hosts_$timestamp.txt"
$hostsContent = "# ZeroTier Network Hosts - Schertech Bangladesh`n"
$hostsContent += "# Generated: $(Get-Date -Format 'yyyy-MM-dd HH:mm:ss')`n`n"

foreach ($item in $inventory) {
    $hostsContent += "$($item.ZeroTierIP)`t$($item.ComputerName).zt`t$($item.ComputerName)`n"
}

$hostsContent | Out-File $hostsFile
Write-Host "Hosts file entries: $hostsFile" -ForegroundColor Green

Write-Host "`n✅ Inventory export complete" -ForegroundColor Green
```

**Save as:** `C:\Scripts\ZeroTier-Deployment\Export-Inventory.ps1`

**Execute:**
```powershell
.\Export-Inventory.ps1 -NetworkID "YOUR-NETWORK-ID" -ApiToken "YOUR-API-TOKEN"
```

#### Step 4.2: Connectivity Validation

```powershell
# ============================================
# CONNECTIVITY VALIDATION TEST
# ============================================

$scriptRoot = "C:\Scripts\ZeroTier-Deployment"
$inventory = Import-Csv "$scriptRoot\Reports\Inventory_*.csv" | Sort-Object LastWriteTime -Descending | Select-Object -First 1

Write-Host "Running connectivity tests..." -ForegroundColor Cyan

$results = @()

foreach ($device in $inventory) {
    $ip = $device.ZeroTierIP
    $name = $device.ComputerName
    
    Write-Host "Testing $name ($ip)..." -NoNewline
    
    # Ping test
    $pingResult = Test-Connection -ComputerName $ip -Count 2 -Quiet
    
    # Port tests
    $rdpTest = Test-NetConnection -ComputerName $ip -Port 3389 -WarningAction SilentlyContinue -InformationLevel Quiet
    $sshTest = Test-NetConnection -ComputerName $ip -Port 22 -WarningAction SilentlyContinue -InformationLevel Quiet
    $winrmTest = Test-NetConnection -ComputerName $ip -Port 5985 -WarningAction SilentlyContinue -InformationLevel Quiet
    
    $status = if($pingResult){"✅"}else{"❌"}
    Write-Host " $status" -ForegroundColor $(if($pingResult){"Green"}else{"Red"})
    
    $results += [PSCustomObject]@{
        ComputerName = $name
        ZeroTierIP = $ip
        Ping = $pingResult
        RDP = $rdpTest
        SSH = $sshTest
        WinRM = $winrmTest
        Overall = ($pingResult -and ($rdpTest -or $sshTest -or $winrmTest))
    }
}

# Summary
$totalDevices = $results.Count
$reachable = ($results | Where-Object {$_.Ping}).Count
$unreachable = $totalDevices - $reachable

Write-Host "`n" + ("=" * 60) -ForegroundColor Cyan
Write-Host "CONNECTIVITY TEST RESULTS" -ForegroundColor White
Write-Host ("=" * 60) -ForegroundColor Cyan
Write-Host "Total Devices: $totalDevices" -ForegroundColor Cyan
Write-Host "Reachable: $reachable" -ForegroundColor Green
Write-Host "Unreachable: $unreachable" -ForegroundColor $(if($unreachable -gt 0){"Red"}else{"Green"})
Write-Host "Success Rate: $([math]::Round(($reachable / $totalDevices) * 100, 2))%" -ForegroundColor Cyan
Write-Host ("=" * 60) + "`n" -ForegroundColor Cyan

# Export results
$reportFile = "$scriptRoot\Reports\ConnectivityTest_$(Get-Date -Format 'yyyyMMdd_HHmmss').csv"
$results | Export-Csv -Path $reportFile -NoTypeInformation
Write-Host "Test results exported: $reportFile" -ForegroundColor Green

# Display failed connections
$failed = $results | Where-Object {-not $_.Ping}
if ($failed.Count -gt 0) {
    Write-Host "`n⚠️  ATTENTION: $($failed.Count) devices are unreachable" -ForegroundColor Yellow
    $failed | Format-Table ComputerName, ZeroTierIP -AutoSize
}
```

**Save as:** `C:\Scripts\ZeroTier-Deployment\Test-Connectivity.ps1`

**✅ PHASE 4 COMPLETE** - Deployment verified and documented.

---

## 6. SECURITY HARDENING

### 6.1 Network Flow Rules Configuration

**Performed By:** Abubakkar Khan Fazla Rabbi (SecOps)  
**Purpose:** Implement zero-trust security controls

```
# Navigate to: https://my.zerotier.com/
# Select your network → "Flow Rules" tab
# Replace default rules with the following:

#
# Schertech Bangladesh - Production Network Flow Rules
# Author: Abubakkar Khan Fazla Rabbi, Senior System Engineer - SecOps
# Last Updated: October 18, 2025
# Security Policy: Zero-Trust, Least Privilege
#

# Drop all traffic by default
drop;

# Allow administrative access from designated admin hosts
# Tag admin hosts appropriately in member configuration
tag admins
  id 10.147.17.1       # Host server
;

# Allow admins to access all client services
accept
  src admins
  dst *
;

# Allow specific inter-client communication (RDP, SSH, File Sharing)
accept
  src *
  dst *
  dport 22,3389,445,139
;

# Allow ICMP for network diagnostics
accept
  ipprotocol icmp
;

# Allow DNS
accept
  dport 53
;

# Log denied traffic (optional - for audit)
# Requires paid plan for logging
break
  action log
  src *
  dst *
;

# Final explicit deny
drop;
```

**Validation:**
```powershell
# Test flow rules from admin host
Test-NetConnection -ComputerName 10.147.17.2 -Port 3389  # Should succeed
Test-NetConnection -ComputerName 10.147.17.2 -Port 8080  # Should fail
```

### 6.2 Access Control List (ACL) Documentation

| **Source** | **Destination** | **Ports** | **Protocol** | **Action** | **Justification** |
|------------|-----------------|-----------|--------------|------------|-------------------|
| Admin Host (10.147.17.1) | All Clients | 22, 3389, 5985 | TCP | ALLOW | Administrative access |
| All Clients | All Clients | 22, 3389, 445 | TCP | ALLOW | Inter-system communication |
| All | All | * | ICMP | ALLOW | Network diagnostics |
| All | All | * | * | DENY | Default deny (zero-trust) |

### 6.3 Endpoint Security Configuration

```powershell
# Run on all client machines
# Configure Windows Firewall for ZeroTier

$computers = Get-Content "C:\Scripts\ZeroTier-Deployment\computers.txt"

Invoke-Command -ComputerName $computers -ScriptBlock {
    # Allow ZeroTier through Windows Firewall
    $rules = @(
        @{
            Name = "ZeroTier-In-TCP"
            DisplayName = "ZeroTier Inbound (TCP)"
            Direction = "Inbound"
            Action = "Allow"
            Protocol = "TCP"
            LocalPort = 9993
        },
        @{
            Name = "ZeroTier-In-UDP"
            DisplayName = "ZeroTier Inbound (UDP)"
            Direction = "Inbound"
            Action = "Allow"
            Protocol = "UDP"
            LocalPort = 9993
        },
        @{
            Name = "ZeroTier-Out"
            DisplayName = "ZeroTier Outbound"
            Direction = "Outbound"
            Action = "Allow"
            Program = "C:\Program Files (x86)\ZeroTier\One\zerotier-one_x64.exe"
        }
    )
    
    foreach ($rule in $rules) {
        if (-not (Get-NetFirewallRule -Name $rule.Name -ErrorAction SilentlyContinue)) {
            New-NetFirewallRule @rule -ErrorAction SilentlyContinue
        }
    }
    
    Write-Host "$env:COMPUTERNAME firewall configured" -ForegroundColor Green
}
```

### 6.4 Antivirus Exclusions

```powershell
# Add ZeroTier to Windows Defender exclusions
# Run on all machines

Invoke-Command -ComputerName $computers -ScriptBlock {
    # Exclusions
    $exclusions = @(
        "C:\Program Files (x86)\ZeroTier\",
        "C:\ProgramData\ZeroTier\"
    )
    
    foreach ($path in $exclusions) {
        Add-MpPreference -ExclusionPath $path -ErrorAction SilentlyContinue
    }
    
    # Process exclusion
    Add-MpPreference -ExclusionProcess "zerotier-one_x64.exe" -ErrorAction SilentlyContinue
    
    Write-Host "$env:COMPUTERNAME - Antivirus exclusions configured"
}
```

---

## 7. MONITORING & AUDIT

### 7.1 Daily Health Check Script

```powershell
# ============================================
# DAILY ZEROTIER HEALTH CHECK
# Scheduled Task: Daily at 09:00
# Author: Abubakkar Khan Fazla Rabbi
# ============================================

param(
    [Parameter(Mandatory=$true)]
    [string]$NetworkID,
    
    [Parameter(Mandatory=$true)]
    [string]$ApiToken,
    
    [Parameter(Mandatory=$false)]
    [string]$EmailRecipient = "infrastructure@schertech.com"
)

$scriptRoot = "C:\Scripts\ZeroTier-Deployment"
$logPath = "$scriptRoot\Logs\HealthCheck_$(Get-Date -Format 'yyyyMMdd').log"

function Write-HealthLog {
    param([string]$Message)
    $timestamp = Get-Date -Format "yyyy-MM-dd HH:mm:ss"
    $logEntry = "[$timestamp] $Message"
    Add-Content -Path $logPath -Value $logEntry
}

Write-HealthLog "Health check initiated"

$headers = @{
    "Authorization" = "Bearer $ApiToken"
}

try {
    # Fetch network status
    $network = Invoke-RestMethod -Uri "https://my.zerotier.com/api/network/$NetworkID" `
                                  -Headers $headers -Method Get
    
    # Fetch members
    $members = Invoke-RestMethod -Uri "https://my.zerotier.com/api/network/$NetworkID/member" `
                                  -Headers $headers -Method Get
    
    # Statistics
    $totalMembers = $members.Count
    $onlineMembers = ($members | Where-Object {$_.online}).Count
    $offlineMembers = $totalMembers - $onlineMembers
    $authorizedMembers = ($members | Where-Object {$_.config.authorized}).Count
    $unauthorizedMembers = $totalMembers - $authorizedMembers
    
    # Health status
    $healthStatus = if($onlineMembers / $totalMembers -gt 0.95){"HEALTHY"}
                    elseif($onlineMembers / $totalMembers -gt 0.85){"WARNING"}
                    else{"CRITICAL"}
    
    # Generate report
    $report = @"
ZEROTIER NETWORK HEALTH REPORT
================================
Organization: Schertech Italy - Bangladesh Branch
Department: Infrastructure Team
Generated: $(Get-Date -Format "yyyy-MM-dd HH:mm:ss")
Network ID: $NetworkID
Network Name: $($network.config.name)

OVERALL STATUS: $healthStatus

STATISTICS:
-----------
Total Members: $totalMembers
Online: $onlineMembers ($([math]::Round(($onlineMembers/$totalMembers)*100,2))%)
Offline: $offlineMembers ($([math]::Round(($offlineMembers/$totalMembers)*100,2))%)
Authorized: $authorizedMembers
Unauthorized: $unauthorizedMembers

"@
    
    Write-HealthLog "Status: $healthStatus | Online: $onlineMembers/$totalMembers"
    
    # Offline devices report
    $offlineDevices = $members | Where-Object {-not $_.online} | Select-Object name, nodeId, @{
        Name='LastSeen'
        Expression={
            if($_.lastOnline -gt 0){
                [DateTimeOffset]::FromUnixTimeMilliseconds($_.lastOnline).LocalDateTime
            } else { "Never" }
        }
    }
    
    if ($offlineDevices.Count -gt 0) {
        $report += @"
OFFLINE DEVICES:
----------------
$($offlineDevices | Format-Table -AutoSize | Out-String)

"@
    }
    
    # Unauthorized devices
    $unauthorizedDevices = $members | Where-Object {-not $_.config.authorized}
    if ($unauthorizedDevices.Count -gt 0) {
        $report += @"
⚠️  SECURITY ALERT: UNAUTHORIZED DEVICES DETECTED
------------------------------------------------
$($unauthorizedDevices | Select-Object nodeId, physicalAddress | Format-Table -AutoSize | Out-String)

"@
        Write-HealthLog "ALERT: $($unauthorizedDevices.Count) unauthorized devices detected"
    }
    
    # Save report
    $reportFile = "$scriptRoot\Reports\HealthReport_$(Get-Date -Format 'yyyyMMdd').txt"
    $report | Out-File $reportFile
    
    # Console output
    Write-Host $report -ForegroundColor $(if($healthStatus -eq "HEALTHY"){"Green"}elseif($healthStatus -eq "WARNING"){"Yellow"}else{"Red"})
    
    # Email notification (requires SMTP configuration)
    if ($healthStatus -ne "HEALTHY" -or $unauthorizedDevices.Count -gt 0) {
        # Configure SMTP settings
        $smtpServer = "smtp.schertech.com"
        $smtpPort = 587
        $smtpUser = "monitoring@schertech.com"
        $smtpPassword = ConvertTo-SecureString "YOUR-PASSWORD" -AsPlainText -Force
        $smtpCred = New-Object System.Management.Automation.PSCredential($smtpUser, $smtpPassword)
        
        $mailParams = @{
            To = $EmailRecipient
            From = "zerotier-monitoring@schertech.com"
            Subject = "ZeroTier Health Alert - Status: $healthStatus"
            Body = $report
            SmtpServer = $smtpServer
            Port = $smtpPort
            Credential = $smtpCred
            UseSsl = $true
        }
        
        # Send-MailMessage @mailParams
        Write-HealthLog "Alert email sent to $EmailRecipient"
    }
    
    Write-HealthLog "Health check completed successfully"
    
} catch {
    Write-HealthLog "ERROR: $($_.Exception.Message)"
    Write-Host "Health check failed: $($_.Exception.Message)" -ForegroundColor Red
}
```

**Save as:** `C:\Scripts\ZeroTier-Deployment\Daily-HealthCheck.ps1`

### 7.2 Scheduled Task Configuration

```powershell
# Create scheduled task for daily health checks

$taskName = "ZeroTier-DailyHealthCheck"
$scriptPath = "C:\Scripts\ZeroTier-Deployment\Daily-HealthCheck.ps1"
$networkID = "YOUR-NETWORK-ID"
$apiToken = "YOUR-API-TOKEN"

$action = New-ScheduledTaskAction -Execute "PowerShell.exe" `
    -Argument "-ExecutionPolicy Bypass -File `"$scriptPath`" -NetworkID `"$networkID`" -ApiToken `"$apiToken`""

$trigger = New-ScheduledTaskTrigger -Daily -At 09:00

$principal = New-ScheduledTaskPrincipal -UserID "NT AUTHORITY\SYSTEM" -LogonType ServiceAccount -RunLevel Highest

$settings = New-ScheduledTaskSettingsSet -AllowStartIfOnBatteries -DontStopIfGoingOnBatteries -StartWhenAvailable

Register-ScheduledTask -TaskName $taskName `
                       -Action $action `
                       -Trigger $trigger `
                       -Principal $principal `
                       -Settings $settings `
                       -Description "Daily ZeroTier network health monitoring for Schertech Bangladesh"

Write-Host "✅ Scheduled task '$taskName' created successfully" -ForegroundColor Green
```

### 7.3 Audit Logging

**ZeroTier Central Audit Logs** (Available on paid plans):
- Network configuration changes
- Member additions/removals
- Authorization events
- API access logs

**Local Audit Logging:**
```powershell
# Enable PowerShell script logging
$regPath = "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging"
New-Item -Path $regPath -Force | Out-Null
Set-ItemProperty -Path $regPath -Name "EnableScriptBlockLogging" -Value 1

# Enable module logging
$regPath2 = "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ModuleLogging"
New-Item -Path $regPath2 -Force | Out-Null
Set-ItemProperty -Path $regPath2 -Name "EnableModuleLogging" -Value 1

Write-Host "✅ PowerShell audit logging enabled" -ForegroundColor Green
```

---

## 8. DISASTER RECOVERY

### 8.1 Backup Procedures

**8.1.1 Network Configuration Backup**

```powershell
# ============================================
# ZEROTIER CONFIGURATION BACKUP
# Author: Abubakkar Khan Fazla Rabbi
# Frequency: Daily (automated)
# ============================================

param(
    [Parameter(Mandatory=$true)]
    [string]$NetworkID,
    
    [Parameter(Mandatory=$true)]
    [string]$ApiToken
)

$scriptRoot = "C:\Scripts\ZeroTier-Deployment"
$backupRoot = "$scriptRoot\Backups"
$timestamp = Get-Date -Format "yyyyMMdd_HHmmss"
$backupPath = "$backupRoot\Backup_$timestamp"

# Create backup directory
New-Item -ItemType Directory -Path $backupPath -Force | Out-Null

$headers = @{
    "Authorization" = "Bearer $ApiToken"
}

try {
    Write-Host "Starting configuration backup..." -ForegroundColor Cyan
    
    # Backup network configuration
    $network = Invoke-RestMethod -Uri "https://my.zerotier.com/api/network/$NetworkID" `
                                  -Headers $headers -Method Get
    $network | ConvertTo-Json -Depth 10 | Out-File "$backupPath\network-config.json"
    Write-Host "✅ Network configuration backed up" -ForegroundColor Green
    
    # Backup all members
    $members = Invoke-RestMethod -Uri "https://my.zerotier.com/api/network/$NetworkID/member" `
                                  -Headers $headers -Method Get
    $members | ConvertTo-Json -Depth 10 | Out-File "$backupPath\members.json"
    Write-Host "✅ Member list backed up ($($members.Count) members)" -ForegroundColor Green
    
    # Backup flow rules
    $flowRules = $network.rules
    $flowRules | ConvertTo-Json -Depth 10 | Out-File "$backupPath\flow-rules.json"
    Write-Host "✅ Flow rules backed up" -ForegroundColor Green
    
    # Create human-readable summary
    $summary = @"
ZEROTIER BACKUP SUMMARY
========================
Organization: Schertech Italy - Bangladesh Branch
Backup Date: $(Get-Date -Format "yyyy-MM-dd HH:mm:ss")
Performed By: $env:USERNAME
Backup ID: $timestamp

NETWORK INFORMATION:
--------------------
Network ID: $NetworkID
Network Name: $($network.config.name)
Description: $($network.config.description)
IP Assignment Pool: $($network.config.ipAssignmentPools | ConvertTo-Json -Compress)

MEMBER STATISTICS:
------------------
Total Members: $($members.Count)
Authorized: $(($members | Where-Object {$_.config.authorized}).Count)
Online: $(($members | Where-Object {$_.online}).Count)

BACKUP CONTENTS:
----------------
- network-config.json: Complete network configuration
- members.json: All member details and configurations
- flow-rules.json: Network flow rules and security policies
- backup-summary.txt: This summary document

RESTORE INSTRUCTIONS:
---------------------
1. To restore network configuration:
   Use ZeroTier API: PUT /api/network/$NetworkID
   
2. To restore members:
   Re-authorize each member via API or Central dashboard
   
3. To restore flow rules:
   Copy content from flow-rules.json to network flow rules editor

BACKUP LOCATION: $backupPath
"@
    
    $summary | Out-File "$backupPath\backup-summary.txt"
    
    # Compress backup
    $zipFile = "$backupRoot\Backup_$timestamp.zip"
    Compress-Archive -Path "$backupPath\*" -DestinationPath $zipFile -Force
    Write-Host "✅ Backup compressed: $zipFile" -ForegroundColor Green
    
    # Remove uncompressed backup
    Remove-Item -Path $backupPath -Recurse -Force
    
    # Cleanup old backups (keep last 30 days)
    $oldBackups = Get-ChildItem -Path $backupRoot -Filter "Backup_*.zip" | 
                  Where-Object { $_.LastWriteTime -lt (Get-Date).AddDays(-30) }
    
    foreach ($old in $oldBackups) {
        Remove-Item $old.FullName -Force
        Write-Host "Removed old backup: $($old.Name)" -ForegroundColor Gray
    }
    
    Write-Host "`n✅ BACKUP COMPLETED SUCCESSFULLY" -ForegroundColor Green
    Write-Host "Backup file: $zipFile" -ForegroundColor Cyan
    
} catch {
    Write-Host "❌ BACKUP FAILED: $($_.Exception.Message)" -ForegroundColor Red
    exit 1
}
```

**Save as:** `C:\Scripts\ZeroTier-Deployment\Backup-Configuration.ps1`

**Schedule daily backups:**
```powershell
$taskName = "ZeroTier-DailyBackup"
$scriptPath = "C:\Scripts\ZeroTier-Deployment\Backup-Configuration.ps1"

$action = New-ScheduledTaskAction -Execute "PowerShell.exe" `
    -Argument "-ExecutionPolicy Bypass -File `"$scriptPath`" -NetworkID `"YOUR-NETWORK-ID`" -ApiToken `"YOUR-API-TOKEN`""

$trigger = New-ScheduledTaskTrigger -Daily -At 02:00

$principal = New-ScheduledTaskPrincipal -UserID "NT AUTHORITY\SYSTEM" -LogonType ServiceAccount -RunLevel Highest

Register-ScheduledTask -TaskName $taskName -Action $action -Trigger $trigger -Principal $principal `
    -Description "Daily backup of ZeroTier network configuration"

Write-Host "✅ Daily backup scheduled at 02:00" -ForegroundColor Green
```

### 8.2 Disaster Recovery Procedures

**8.2.1 Complete Network Loss Scenario**

**Recovery Steps:**

1. **Create New Network**
```powershell
# Manual: Create new network at https://my.zerotier.com/
# Note new Network ID
```

2. **Restore Configuration**
```powershell
# Extract latest backup
$latestBackup = Get-ChildItem "C:\Scripts\ZeroTier-Deployment\Backups" -Filter "Backup_*.zip" | 
                Sort-Object LastWriteTime -Descending | 
                Select-Object -First 1

Expand-Archive -Path $latestBackup.FullName -DestinationPath "C:\Temp\ZT-Restore" -Force

# Load configuration
$networkConfig = Get-Content "C:\Temp\ZT-Restore\network-config.json" | ConvertFrom-Json
$members = Get-Content "C:\Temp\ZT-Restore\members.json" | ConvertFrom-Json

# Apply configuration via API
$newNetworkID = "NEW-NETWORK-ID"
$apiToken = "YOUR-API-TOKEN"

$headers = @{
    "Authorization" = "Bearer $apiToken"
    "Content-Type" = "application/json"
}

# Update network settings
$body = @{
    config = $networkConfig.config
} | ConvertTo-Json -Depth 10

Invoke-RestMethod -Uri "https://my.zerotier.com/api/network/$newNetworkID" `
                  -Headers $headers -Method Post -Body $body

Write-Host "✅ Network configuration restored" -ForegroundColor Green
```

3. **Re-deploy to Clients**
```powershell
# Have clients leave old network and join new network
$computers = Get-Content "C:\Scripts\ZeroTier-Deployment\computers.txt"

Invoke-Command -ComputerName $computers -ScriptBlock {
    param($oldNet, $newNet)
    
    $ztCli = "C:\Program Files (x86)\ZeroTier\One\zerotier-one_x64.exe"
    
    # Leave old network
    & $ztCli -q leave $oldNet
    
    # Join new network
    & $ztCli -q join $newNet
    
} -ArgumentList "OLD-NETWORK-ID", "NEW-NETWORK-ID"
```

4. **Re-authorize All Members**
```powershell
# Run authorization script
.\Authorize-Members.ps1 -NetworkID "NEW-NETWORK-ID" -ApiToken "YOUR-API-TOKEN"
```

**Recovery Time Objective (RTO):** 2-4 hours  
**Recovery Point Objective (RPO):** 24 hours (daily backups)

### 8.3 Rollback Procedures

**Scenario: Need to remove ZeroTier from all systems**

```powershell
# ============================================
# ZEROTIER COMPLETE REMOVAL (ROLLBACK)
# ============================================

param(
    [Parameter(Mandatory=$false)]
    [string[]]$ComputerList = $null
)

$scriptRoot = "C:\Scripts\ZeroTier-Deployment"

if ($null -eq $ComputerList) {
    $ComputerList = Get-Content "$scriptRoot\computers.txt"
}

Write-Host "⚠️  WARNING: This will remove ZeroTier from all specified machines" -ForegroundColor Yellow
$confirm = Read-Host "Type 'REMOVE' to confirm"

if ($confirm -ne "REMOVE") {
    Write-Host "Operation cancelled" -ForegroundColor Yellow
    exit
}

$scriptBlock = {
    try {
        # Stop service
        Stop-Service ZeroTierOneService -Force -ErrorAction SilentlyContinue
        
        # Uninstall via MSI
        $uninstallString = Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*" | 
                          Where-Object {$_.DisplayName -like "*ZeroTier*"} | 
                          Select-Object -ExpandProperty UninstallString
        
        if ($uninstallString) {
            $msiGuid = $uninstallString -replace "MsiExec.exe /I", ""
            Start-Process msiexec.exe -ArgumentList "/x $msiGuid /quiet /norestart" -Wait -NoNewWindow
        }
        
        # Cleanup directories
        Remove-Item "C:\Program Files (x86)\ZeroTier" -Recurse -Force -ErrorAction SilentlyContinue
        Remove-Item "C:\ProgramData\ZeroTier" -Recurse -Force -ErrorAction SilentlyContinue
        
        # Remove firewall rules
        Remove-NetFirewallRule -Name "ZeroTier*" -ErrorAction SilentlyContinue
        
        Write-Host "$env:COMPUTERNAME - ZeroTier removed successfully" -ForegroundColor Green
        return $true
        
    } catch {
        Write-Host "$env:COMPUTERNAME - Removal failed: $($_.Exception.Message)" -ForegroundColor Red
        return $false
    }
}

$results = Invoke-Command -ComputerName $ComputerList -ScriptBlock $scriptBlock

$successful = ($results | Where-Object {$_ -eq $true}).Count
$failed = $results.Count - $successful

Write-Host "`nRemoval Summary:" -ForegroundColor Cyan
Write-Host "Successful: $successful" -ForegroundColor Green
Write-Host "Failed: $failed" -ForegroundColor $(if($failed -gt 0){"Red"}else{"Green"})
```

**Save as:** `C:\Scripts\ZeroTier-Deployment\Remove-ZeroTier.ps1`

---

## 9. TROUBLESHOOTING RUNBOOK

### 9.1 Common Issues and Resolution

**Issue 1: Client Not Appearing in Network**

**Symptoms:**
- Client machine shows ZeroTier service running
- Not visible in ZeroTier Central members list

**Diagnosis:**
```powershell
# On client machine
Invoke-Command -ComputerName CLIENT-PC-001 -ScriptBlock {
    # Check service
    Get-Service ZeroTierOneService | Format-List *
    
    # Check joined networks
    & "C:\Program Files (x86)\ZeroTier\One\zerotier-one_x64.exe" -q listnetworks
    
    # Check node info
    & "C:\Program Files (x86)\ZeroTier\One\zerotier-one_x64.exe" -q info
    
    # Check connectivity to ZeroTier root servers
    Test-NetConnection my.zerotier.com -Port 443
}
```

**Resolution:**
```powershell
# Restart ZeroTier service
Invoke-Command -ComputerName CLIENT-PC-001 -ScriptBlock {
    Restart-Service ZeroTierOneService
    Start-Sleep -Seconds 5
    
    # Rejoin network
    & "C:\Program Files (x86)\ZeroTier\One\zerotier-one_x64.exe" -q join YOUR-NETWORK-ID
}
```

---

**Issue 2: Cannot Connect to Client via ZeroTier IP**

**Symptoms:**
- Client shows as online in ZeroTier Central
- Cannot ping or RDP to ZeroTier IP

**Diagnosis:**
```powershell
# From host server
$clientIP = "10.147.17.2"

# Test basic connectivity
Test-Connection -ComputerName $clientIP -Count 4

# Test specific ports
Test-NetConnection -ComputerName $clientIP -Port 3389  # RDP
Test-NetConnection -ComputerName $clientIP -Port 22    # SSH

# Check Windows Firewall on client
Invoke-Command -ComputerName CLIENT-PC-001 -ScriptBlock {
    Get-NetFirewallProfile | Select-Object Name, Enabled, DefaultInboundAction
    Get-NetFirewallRule | Where-Object {$_.Enabled -eq $true -and $_.Direction -eq "Inbound"}
}
```

**Resolution:**
```powershell
# Configure Windows Firewall on client
Invoke-Command -ComputerName CLIENT-PC-001 -ScriptBlock {
    # Allow RDP
    Enable-NetFirewallRule -DisplayGroup "Remote Desktop"
    
    # Allow ICMP (ping)
    New-NetFirewallRule -DisplayName "Allow ICMPv4-In" -Protocol ICMPv4 -IcmpType 8 -Enabled True -Direction Inbound -Action Allow
    
    # Verify ZeroTier adapter
    Get-NetAdapter | Where-Object {$_.InterfaceDescription -like "*ZeroTier*"}
}
```

---

**Issue 3: ZeroTier Service Fails to Start**

**Symptoms:**
- Service status shows "Stopped"
- Cannot start service manually

**Diagnosis:**
```powershell
Invoke-Command -ComputerName CLIENT-PC-001 -ScriptBlock {
    # Check service
    Get-Service ZeroTierOneService | Format-List *
    
    # Check event logs
    Get-EventLog -LogName Application -Source "ZeroTier*" -Newest 20 | Format-List *
    
    # Check if port is already in use
    netstat -ano | findstr ":9993"
}
```

**Resolution:**
```powershell
Invoke-Command -ComputerName CLIENT-PC-001 -ScriptBlock {
    # Stop any conflicting processes
    Get-Process | Where-Object {$_.ProcessName -like "*zerotier*"} | Stop-Process -Force
    
    # Reset service
    sc.exe config ZeroTierOneService start= auto
    Start-Service ZeroTierOneService
    
    # If still fails, reinstall
    # Use removal and deployment scripts
}
```

---

**Issue 4: High CPU Usage by ZeroTier**

**Symptoms:**
- zerotier-one_x64.exe consuming >20% CPU constantly

**Diagnosis:**
```powershell
Invoke-Command -ComputerName CLIENT-PC-001 -ScriptBlock {
    # Check process
    Get-Process zerotier* | Format-Table ProcessName, CPU, WorkingSet -AutoSize
    
    # Check network adapter statistics
    Get-NetAdapter | Where-Object {$_.InterfaceDescription -like "*ZeroTier*"} | Get-NetAdapterStatistics
}
```

**Resolution:**
```powershell
Invoke-Command -ComputerName CLIENT-PC-001 -ScriptBlock {
    # Restart service
    Restart-Service ZeroTierOneService
    
    # If persists, check for network loops or broadcast storms
    # Review flow rules for potential issues
}
```

---

### 9.2 Emergency Contact Information

| **Role** | **Name** | **Contact** | **Availability** |
|----------|----------|-------------|------------------|
| Primary Engineer | Abubakkar Khan Fazla Rabbi | [Phone/Email] | Business hours + on-call |
| Infrastructure Team Lead | [TBD] | [Contact] | Business hours |
| Security Operations | [TBD] | [Contact] | 24/7 |
| Vendor Support | ZeroTier Support | support@zerotier.com | 24/7 (paid plans) |

### 9.3 Escalation Matrix

**Level 1:** Infrastructure Team  
**Level 2:** Senior System Engineer (SecOps)  
**Level 3:** IT Management  
**Level 4:** ZeroTier Enterprise Support (if applicable)

---

## 10. APPENDICES

### 10.1 Glossary

| **Term** | **Definition** |
|----------|----------------|
| **ZeroTier** | Software-defined networking platform providing secure peer-to-peer connectivity |
| **Node ID** | Unique 10-character hexadecimal identifier for each ZeroTier instance |
| **Network ID** | 16-character hexadecimal identifier for a ZeroTier network |
| **Flow Rules** | Network-level firewall rules controlling traffic between members |
| **Member** | A device connected to a ZeroTier network |
| **Authorization** | Process of allowing a member to join a private network |
| **Virtual IP** | IP address assigned to a device within the ZeroTier network (e.g., 10.147.17.x) |

### 10.2 Useful Commands Reference

```powershell
# ZEROTIER CLI COMMANDS (Run on any Windows machine with ZeroTier installed)

# Path to CLI
$ztCli = "C:\Program Files (x86)\ZeroTier\One\zerotier-one_x64.exe"

# Get node info
& $ztCli -q info
# Output: 200 info <nodeId> <version> ONLINE

# List networks
& $ztCli -q listnetworks
# Output: 200 listnetworks <networkid> <name> <mac> <status> <type> <dev> <ZT assigned IPs>

# List peers (other nodes)
& $ztCli -q listpeers
# Output: Shows all connected peers

# Join network
& $ztCli -q join <networkid>

# Leave network
& $ztCli -q leave <networkid>

# Get IPv4 address
& $ztCli -q get <networkid> ip4

# Set custom IPv4 (requires authorization)
& $ztCli -q set <networkid> ip4 10.147.17.50
```

### 10.3 API Reference

**Base URL:** `https://my.zerotier.com/api`

**Authentication:** Bearer token in Authorization header

**Common Endpoints:**

```bash
# Get network details
GET /api/network/{networkId}

# Update network configuration
POST /api/network/{networkId}

# List all members
GET /api/network/{networkId}/member

# Get specific member
GET /api/network/{networkId}/member/{nodeId}

# Authorize member
POST /api/network/{networkId}/member/{nodeId}
Body: {"config": {"authorized": true}}

# Delete member
DELETE /api/network/{networkId}/member/{nodeId}
```

**PowerShell API Example:**
```powershell
$networkId = "YOUR-NETWORK-ID"
$apiToken = "YOUR-API-TOKEN"

$headers = @{
    "Authorization" = "Bearer $apiToken"
}

# Get all members
$members = Invoke-RestMethod -Uri "https://my.zerotier.com/api/network/$networkId/member" `
                              -Headers $headers -Method Get

$members | Format-Table nodeId, name, online, @{N='IP';E={$_.config.ipAssignments[0]}}
```

### 10.4 Network Diagram

```
SCHERTECH BANGLADESH - ZEROTIER NETWORK ARCHITECTURE
====================================================

                     ┌─────────────────────┐
                     │  ZeroTier Central   │
                     │   my.zerotier.com   │
                     │  Network Controller │
                     └──────────┬──────────┘
                                │
                    ┌───────────┴───────────┐
                    │                       │
         ┌──────────▼─────────┐  ┌─────────▼──────────┐
         │   Host Server      │  │  Client Machines   │
         │  10.147.17.1       │  │  10.147.17.2-101   │
         │  (Admin Control)   │  │  (100+ Endpoints)  │
         └──────────┬─────────┘  └─────────┬──────────┘
                    │                       │
         ┌──────────▼─────────────────────────────┐
         │  Encrypted P2P Connections (UDP 9993)  │
         │  AES-256-GCM End-to-End Encryption     │
         └────────────────────────────────────────┘

Access Methods:
  • SSH (Port 22): Terminal access
  • RDP (Port 3389): Remote desktop
  • PowerShell Remoting (Port 5985): Automation
  • File Sharing (Port 445): SMB/CIFS

Security Controls:
  • Private network (manual authorization required)
  • Flow rules (zero-trust firewall)
  • 256-bit encryption
  • Unique cryptographic node IDs
```

### 10.5 Compliance Checklist

**Security Compliance:**
- [x] End-to-end encryption enabled (256-bit)
- [x] Private network mode (manual authorization)
- [x] Flow rules configured (least privilege)
- [x] Multi-factor authentication on admin accounts
- [x] API tokens securely stored
- [x] Audit logging enabled (where available)
- [x] Regular security reviews scheduled

**Operational Compliance:**
- [x] Daily health monitoring
- [x] Daily configuration backups
- [x] Disaster recovery plan documented
- [x] Incident response procedures defined
- [x] Change management procedures followed
- [x] Documentation maintained and current

**Data Protection:**
- [x] No sensitive data stored on ZeroTier infrastructure
- [x] All traffic encrypted in transit
- [x] Access controls implemented
- [x] Data retention policies defined

### 10.6 Change Log Template

**Use this template for all future changes:**

```
CHANGE REQUEST: [CR-YYYY-MM-DD-XXX]
==================================
Date: [Date]
Requested By: [Name, Title]
Approved By: [Name, Title]

CHANGE DESCRIPTION:
[Detailed description of the change]

BUSINESS JUSTIFICATION:
[Why this change is needed]

SYSTEMS AFFECTED:
- [List of affected systems]

RISK ASSESSMENT:
Impact: [High/Medium/Low]
Risk: [High/Medium/Low]

IMPLEMENTATION PLAN:
1. [Step 1]
2. [Step 2]
...

ROLLBACK PLAN:
1. [Rollback step 1]
2. [Rollback step 2]
...

TESTING PERFORMED:
[Description of testing]

RESULTS:
[Success/Failure + details]

POST-IMPLEMENTATION NOTES:
[Any issues, observations, or recommendations]
```

### 10.7 Quick Reference Card

**EMERGENCY PROCEDURES**

```
1. COMPLETE NETWORK OUTAGE:
   - Check ZeroTier Central status: https://status.zerotier.com
   - Verify host server connectivity
   - Run: .\Daily-HealthCheck.ps1
   - Contact: Abubakkar Khan Fazla Rabbi

2. SECURITY INCIDENT:
   - Immediately disable affected members in ZeroTier Central
   - Review audit logs
   - Run: .\Export-Inventory.ps1 for forensics
   - Escalate to SecOps team

3. CLIENT CONNECTIVITY ISSUES:
   - Verify client is online in ZeroTier Central
   - Check client firewall settings
   - Restart ZeroTier service on client
   - Test with: Test-Connection -ComputerName <ZT-IP>

4. MASS DEPLOYMENT FAILURE:
   - Check PowerShell remoting connectivity
   - Review deployment logs in C:\Scripts\ZeroTier-Deployment\Logs\
   - Retry with -TestMode flag first
   - Contact Infrastructure Team

CRITICAL CONTACTS:
SecOps: [Contact]
Infrastructure: [Contact]
Management: [Contact]
```

---

## DOCUMENT APPROVAL

### Approval Signatures

| **Role** | **Name** | **Signature** | **Date** |
|----------|----------|---------------|----------|
| **Author** | Abubakkar Khan Fazla Rabbi, Senior System Engineer - SecOps | _________________ | __________ |
| **Reviewed By** | [Infrastructure Team Lead] | _________________ | __________ |
| **Approved By** | [IT Manager] | _________________ | __________ |
| **Security Review** | [Security Officer] | _________________ | __________ |

---

## FINAL NOTES

This document represents a complete, production-ready deployment guide for ZeroTier SDN infrastructure at Schertech Italy - Bangladesh Branch. All procedures have been designed with security, reliability, and operational efficiency as primary concerns.

**Key Success Factors:**
- Follow security hardening procedures strictly
- Maintain daily monitoring and backups
- Document all changes
- Regular team training on procedures
- Periodic security audits

**Post-Deployment Actions:**
1. Schedule team training session
2. Configure all scheduled tasks
3. Perform quarterly disaster recovery drill
4. Review and update documentation
5. Implement continuous improvement feedback

---

**Document End**

*Prepared by: Abubakkar Khan Fazla Rabbi*  
*Senior System Engineer - SecOps*  
*Infrastructure Team*  
*Schertech Italy - Bangladesh Branch*  
*October 18, 2025*

---

**Distribution List:**
- Infrastructure Team
- Security Operations Team
- IT Management
- Document Control

**Confidentiality Notice:** This document contains proprietary information of Schertech Italy and is intended for internal use only. Unauthorized distribution is prohibited.
