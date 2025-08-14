# microsoft-dct-demo-t1


# Microsoft: Data Center Technician – Deployment, Break/Fix & Operations Demo

**Your Name · Data Center Technician (CO+I)** · **[Google Docs Version](https://docs.google.com/)**

![Replace with your banner image](assets/rack_elevation.png)

---

## Introduction & Methodology

### Introduction
This project simulates real-world **Microsoft Data Center Technician (DCT)** workflows across **staging, deployment, troubleshooting, decommissioning, and KPI reporting**. Using mock assets, SOPs, and diagrams, it demonstrates how a DCT operates within **CO+I** standards—prioritizing **safety (EHS)**, **process rigor (SOPs)**, **data protection (DBD handling)**, and **clear shift handoffs**.

### Methodology
A practical seven-phase lifecycle that mirrors how deployments and operations run in a Microsoft data center.

| Phase | Objective | Key Actions |
|---|---|---|
| 1. Intake & Approvals | Control change risk | Validate work order, change window, approvals, and dependencies |
| 2. Staging | Prepare gear | Firmware/BIOS baselines, asset tags → CMDB, pre-checks |
| 3. Rack & Cable | Build cleanly | Mount per NDT, A/B power, color/port mapping, strain relief |
| 4. Configure & Test | Prove readiness | iDRAC/iLO config, mgmt VLAN, health & network checks |
| 5. Incident (Break/Fix) | Restore fast | Remote diagnostics → FRU swap → verify → document |
| 6. Decommission & DBD | Protect data | Approved wipe, logs, chain of custody, recycle/dispose |
| 7. Review & KPIs | Improve reliability | SLA/MTTR review, safety observations, lessons learned |

---

## Initial Posture

A new two-server build is scheduled for **Rack C-12 (U20–U21)** with **A/B power redundancy** and **TOR1/TOR2 network** patching.

**Pre-deployment checks to tighten:**
- Confirm **firmware baselines** on both hosts  
- Validate **PDU capacity** and **thermal headroom** in Aisle C  
- Ensure **management VLAN** assignment is ready before test window

> **Target outcomes:** zero safety incidents, no SLA breaches, successful health checks, and a documented handoff.

---

## Maps & Build Artifacts

### Rack Elevation (Planned vs. As-Built)
![Rack elevation](assets/rack_elevation.png)

- **U20–U21** reserved for **Lenovo SR650** (staged)  
- Cable dressing and strain relief per SOP  
- Asset tags scanned to CMDB: `S12345`, `S67890`

### Network Topology (A/B Pathing)
![Network topology](assets/network_topology.png)

- Dual NICs to **TOR1/TOR2**  
- Management VLAN on port profiles **MGT-A / MGT-B**  
- Power: **PDU-A Left**, **PDU-B Right**

---

# Procedures & Evidence

## 1) Staging & Deployment
**Key documents**
- `docs/Server_Staging_Checklist.md` – PPE/THA, firmware, asset, cabling, config  
- `docs/Sample_Ticket_ServiceNow.md` – change window & approvals

**Highlights**
- Firmware & BIOS set to **approved baselines**  
- **Asset tags** applied and scanned into CMDB  
- **iDRAC/iLO** configured with mgmt IPs and NTP

---

## 2) Diagnostics & Troubleshooting (Break/Fix)
- `docs/Incident_Troubleshooting_Workflow.md` – triage → isolation → FRU swap → verify  
- `scripts/Check-ServiceHealth.ps1` – quick remote health probe

```powershell
.\scripts\Check-ServiceHealth.ps1 -Hosts "SRV-C12-U20","SRV-C12-U21" -ServiceName "WinRM"
```

If fault detected
- Review iDRAC Lifecycle Logs
- Replace FRU (DIMM/NIC/PSU), re-run health checks
- Update ticket with serials, photos, and resolution

---

## 3) Decommissioning & DBD Handling
- docs/Decommissioning_SOP.md – wipe → remove → record → recycle
- docs/DBD_Chain_of_Custody_Form.md – serials + wipe method + signatures

---

Controls
- Approved erasure (BitLocker secure erase / DoD wipe)
- Two-person verification for DBD counts
- CMDB updated to Retired

---

## Analysis & Operational Assessment
Change Ticket: CHG-2209 – Rack C-12 (U20–U21)
Window: 02:00–04:00
What we validated
1. A/B power continuity and correct PDU loading
2. Network path redundancy (TOR1/TOR2)
3. Thermals within tolerance after burn-in
4. Service health via PowerShell probe and ping

✅ Result: Systems passed post-deployment checks; no safety events; no SLA breaches.

---

## Post-Deployment Review
### Metrics Snapshot (Demo)

| Metric                            | Value      |
| --------------------------------- | ---------- |
| Deployment Success Rate           | **99.5%**  |
| Avg MTTR (Break/Fix)              | **45 min** |
| Preventive Maintenance Compliance | **100%**   |
| SLA Breaches                      | **0**      |

Improvements for next window
- Pre-stage mgmt VLANs earlier to reduce idle time
- Auto-export iDRAC health to the ticket on completion

---

VLAN & Cabling Reference (Examples)
> Replace with your own annotated screenshots from switch configs, cabling maps, or monitoring views.
- Mgmt VLAN: VLAN 110 (example)
- Port profiles: TOR1-Gi1/0/10, TOR2-Gi1/0/10
- Color map: Blue = Mgmt, White = Data, Red = iSCSI (example)

---

📂 Project Structure — microsoft-dct-demo

<details>
<summary>📂 Project Structure — <code>microsoft-dct-demo</code></summary>

```plaintext
microsoft-dct-demo/
│
├── docs/
│   ├── Server_Staging_Checklist.md
│   ├── Incident_Troubleshooting_Workflow.md
│   ├── Decommissioning_SOP.md
│   ├── DBD_Chain_of_Custody_Form.md
│   ├── Shift_Handoff_Template.md
│   └── Sample_Ticket_ServiceNow.md
│
├── assets/
│   ├── rack_elevation.png
│   ├── network_topology.png
│   └── your_banner_or_photo.png
│
├── data/
│   ├── device_serial_list.csv
│   └── KPI_Dashboard.csv
│
├── scripts/
│   ├── Check-ServiceHealth.ps1
│   └── Inventory-AssetTag.ps1
│
└── reports/
    ├── KPI_dashboard.png
    └── Completion_Report_CHG-2209.md
```
</details> ```


---
---

📂 Project Structure — <code>microsoft-dct-demo</code>

```plaintext
microsoft-dct-demo/
│
├── docs/
│   ├── Server_Staging_Checklist.md
│   ├── Incident_Troubleshooting_Workflow.md
│   ├── Decommissioning_SOP.md
│   ├── DBD_Chain_of_Custody_Form.md
│   ├── Shift_Handoff_Template.md
│   └── Sample_Ticket_ServiceNow.md
│
├── assets/
│   ├── rack_elevation.png
│   ├── network_topology.png
│   └── your_banner_or_photo.png
│
├── data/
│   ├── device_serial_list.csv
│   └── KPI_Dashboard.csv
│
├── scripts/
│   ├── Check-ServiceHealth.ps1
│   └── Inventory-AssetTag.ps1
│
└── reports/
    ├── KPI_dashboard.png
    └── Completion_Report_CHG-2209.md
```

---

| Metric                            | Value      |
| --------------------------------- | ---------- |
| Deployment Success Rate           | **99.5%**  |
| Avg MTTR (Break/Fix)              | **45 min** |
| Preventive Maintenance Compliance | **100%**   |
| SLA Breaches                      | **0**      |

---

| Metric                         | Value      |
| ------------------------------ | ---------- |
| Uptime (Critical Systems)      | **99.99%** |
| Average CPU Utilization        | **54%**    |
| Average Memory Utilization     | **63%**    |
| Storage Utilization Efficiency | **92%**    |

---

| Metric                          | Value      |
| ------------------------------- | ---------- |
| Critical Incidents Resolved     | **100%**   |
| Average Response Time (P1/P2)   | **12 min** |
| Mean Time to Contain (MTTC)     | **20 min** |
| Post-Incident Review Completion | **100%**   |

---

Improvements for Next Window
- Pre-stage mgmt VLANs earlier to reduce idle time
- Add auto-export of iDRAC health to the ticket on completion

VLAN & Cabling Reference (Examples)
> Replace with your own annotated screenshots from switch configs, cabling maps, or monitoring views.
- Mgmt VLAN: VLAN 110 (example)
- Port Profiles: TOR1-Gi1/0/10, TOR2-Gi1/0/10
- Color Map: Blue = Mgmt, White = Data, Red = iSCSI (example)

---

## 📂 Project Structure — `microsoft-dct-demo`

microsoft-dct-demo/

---

**Legend:**
- **`docs/`** → Written procedures, workflows, and templates.  
- **`assets/`** → Diagrams, visual documentation, and banners for the project page.  
- **`data/`** → Example CSV datasets for mock tracking and KPI reporting.  
- **`scripts/`** → PowerShell automation scripts for health checks and inventory.  
- **`reports/`** → Generated dashboards and completion reports.  

---

### Conclusion

This Microsoft Data Center Technician (CO+I) Demo illustrates the complete operational lifecycle of staging, deployment, troubleshooting, and secure decommissioning within a controlled, standards-based framework. By combining SOP-driven processes, accurate visual documentation, and measurable KPIs, it mirrors the discipline, safety, and efficiency expected in a real Microsoft CO+I environment.

The mock artifacts—ranging from rack elevations to incident workflows—showcase your ability to plan meticulously, execute precisely, and communicate clearly under operational constraints. Whether used in an interview, a portfolio review, or a training exercise, this demo conveys readiness to handle complex data center tasks while maintaining zero safety incidents, SLA adherence, and continuous improvement.

