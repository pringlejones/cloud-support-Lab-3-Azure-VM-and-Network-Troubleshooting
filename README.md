# cloud-support-Lab-3-Azure-VM-and-Network-Troubleshooting
## ☁️ Lab 3: Azure Virtual Machines & Network Infrastructure Analysis

This module evaluates cross-platform cloud competency by tracing network security filters, sequential evaluation rule priority matrix structures, and out-of-band kernel console data diagnostic pipelines within Microsoft Azure.

### 📋 Documented Engineering Incidents (Troubleshooting Tickets)

| Ticket Reference | Azure Platform Service | Observed System Symptom | Applied Resolution Strategy |
| :--- | :--- | :--- | :--- |
| **[Ticket #10: NSG Communication Drop](./lab3-azure-network-faults/ticket-10-nsg-timeout.md)** | Network Security Groups (NSG) | Secure connection channels freeze at initiation and return a standard `Connection timed out` error status. | Injected explicit inbound transport protocol exceptions scoped exclusively to target proxy IP nodes. |
| **[Ticket #11: Priority Logic Conflict](./lab3-azure-network-faults/ticket-11-rule-priority.md)** | Network Security Groups (NSG) | Incoming data packets are rejected instantly with an explicit `Connection refused` terminal warning message. | Purged the high-priority sequential block override entry to restore appropriate rule evaluation layers. |
| **[Ticket #12: Out-of-Band OS Recovery](./lab3-azure-network-faults/ticket-12-boot-diagnostics.md)** | Boot Diagnostics / Serial Console | Operating systems lock up mid-boot cycle, dropping network visibility. Telemetry logs flag mounting failures. | Leveraged the direct Azure Serial Console pipeline interface to cleanly remove the corrupt fstab lines. |
