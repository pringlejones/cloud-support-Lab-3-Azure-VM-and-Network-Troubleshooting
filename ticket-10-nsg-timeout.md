# Ticket #10: Azure VM Remote Secure Shell (SSH) Connection Timeout

## 🚨 Customer Incident Report
- **Symptom:** External engineering associates report full communication loss when attempting to establish an out-of-band management session with `Linux-Server-01`.
- **Behavior:** Remote client environments hang indefinitely during terminal handshakes before dropping out with an explicit error: `Connection timed out`.

## 🔍 Engineering Triage & Diagnostics
1. **Compute Status Verification:** Confirmed via the Microsoft Azure Portal that the target virtual instance engine is in an active `Running` allocation state.
2. **Connectivity Isolation:** Verified that the host platform responds normally internally, indicating a perimeter stateful security block filtering incoming data streams.

## 🛠️ Root Cause Analysis (RCA) & Resolution
- **Root Cause:** A review of the platform's **Network Security Group (NSG)** properties revealed that the explicit default rule authorizing inbound TCP communication over **Port 22** had been completely dropped or purged from the control matrix.
- **Applied Fix:** Injected an explicit inbound security filter rule to safely clear a communication path:
  - **Source Type:** IP Addresses | **Source IP:** restricted exclusively to the administrator's desktop public IP address (Security Best Practice).
  - **Destination Port:** 22 | **Protocol:** TCP | **Action:** Allow | **Priority:** 1000

## ✅ Fix Verification
Following rule deployment, remote validation utilities executed perfectly, establishing secure communication links instantly.

### 🖼️ Diagnostic Evidence
**Figure 10.1: Local Terminal Reflecting Core Security Group Timeout Exception**
![Azure NSG Timeout Error]<img width="1110" height="617" alt="case1-azure-nsg-timeout" src="https://github.com/user-attachments/assets/e8bfc919-78be-4e5a-af10-dfccd5d768a2" />

**Figure 10.2: Successful System Authentication Following Path Restoration**
![Azure NSG Resolved]<img width="1440" height="900" alt="case1-azure-nsg-fixed" src="https://github.com/user-attachments/assets/518bde98-87dd-4a1b-b4ed-096b5700af2b" />

