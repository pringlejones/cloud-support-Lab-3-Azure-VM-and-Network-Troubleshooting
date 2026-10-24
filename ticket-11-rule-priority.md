# Ticket #11: Inbound Security Boundary Rule Priority Evaluation Precedence Conflict

## 🚨 Customer Incident Report
- **Symptom:** Network systems drop incoming infrastructure diagnostic links directly at the front boundary edge.
- **Behavior:** Command-line utilities terminate access routines instantly with an explicit `Connection refused` network error code.

## 🔍 Engineering Triage & Diagnostics
1. **Rule Inventory Audit:** Reviewed the active security filtering schema inside the `Linux-Server-01-nsg` portal workspace.
2. **Logic Hierarchy Mapping:** Analyzed the assigned rule weights. Discovered an engineering mismatch where sequential filtering logic nullified existing exceptions.

## 🛠️ Root Cause Analysis (RCA) & Resolution
- **Root Cause:** An administrator deployed a catch-all inbound rule (`Block-All-SSH`) configured to **Deny** traffic over Port 22 at a **Priority assignment of 500**. Because Azure evaluates inbound NSG filters sequentially from lowest numerical value to highest, this rule intercepted and blocked the traffic before the explicit administrative Allow rule (Priority 1000) could be checked.
- **Applied Fix:** Selected the conflicting Priority 500 Deny rule and purged it entirely from the security group settings.

## ✅ Fix Verification
Removing the lower-number block policy restored normal rule hierarchy evaluation, allowing the system to verify and authorize standard administrative entry paths instantly.

### 🖼️ Diagnostic Evidence
**Figure 11.1: Azure Security Rule Workspace Exhibiting Overriding Rule Values**
![Azure NSG Rule Priority Precedence]<img width="816" height="115" alt="case2-nsg-priority" src="https://github.com/user-attachments/assets/22373977-01da-4646-bcf6-4bff98dc32ce" />
<img width="1440" height="900" alt="Screenshot (22)" src="https://github.com/user-attachments/assets/f937d8b2-a9d4-4fed-9b18-9b784d8aec4a" />


