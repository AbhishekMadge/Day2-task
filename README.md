# AWS EC2 — Day 2 Tasks

Vertical scaling of an EC2 instance, launching a Windows EC2 instance with RDP access, and connecting to a Linux EC2 instance using PuTTYgen + PuTTY.

All screenshots are in the [`Task_screenshots/`](./Task_screenshots) folder.

---

## Task 1 — Vertical Scaling of EC2 (t3.micro → t3.medium)

**Objective:** Scale up an existing EC2 instance's compute capacity by changing its instance type, and verify the change.

| Step | Action | Result | Screenshot |
|---|---|---|---|
| 1 | Open EC2 console, identify instance `Task_convert_to_t3.medium` | Instance ID `i-00ad4f4c3de4ea863`, current type `t3.micro`, state Running | `01_task1_before_scaling_t3micro.png` |
| 2 | Stop the instance, then open **Actions → Instance settings → Change instance type** | Instance stopped; "Change instance type" menu accessed | `02_task1_actions_change_instance_type.png` |
| 3 | Select the new instance type on the Change Instance Type page | New type selected and compared against current (`t3.micro` vs new type) | `03_task1_change_instance_type_page.png` |
| 4 | Start the instance again and verify | Instance Running, new instance type confirmed, new public IP assigned | `04_task1_after_scaling_verified.png` |

**Result:**
- **Instance ID:** `i-00ad4f4c3de4ea863`
- **Before:** `t3.micro`
- **After:** instance type updated and instance verified Running with new configuration

> **Note:** Instance type must be **stopped** before it can be changed — AWS does not allow changing the instance type of a running instance. Once changed, the instance was started again and confirmed healthy via status checks.

---

## Task 2 — Launch a Windows EC2 Instance and Connect Using RDP

**Objective:** Launch a Windows EC2 instance, configure security group access, and connect via RDP.

| Step | Action | Result | Screenshot |
|---|---|---|---|
| 1 | Launched EC2 instance using a Windows Server AMI | Instance created — Hostname `EC2AMAZ-NV7TGIH`, size `t3.micro`, AZ `us-east-1c` | `06_task2_windows_rdp_connection.png` |
| 2 | Configured Security Group to allow RDP (TCP port 3389) from permitted source | Inbound rule added for RDP | — |
| 3 | Retrieved Windows administrator password using the EC2 console + key pair | Credentials obtained | — |
| 4 | Connected using Remote Desktop Connection (RDP client) | Successful RDP session to Windows desktop | `06_task2_windows_rdp_connection.png` |

**Instance details (from RDP session):**

| Property | Value |
|---|---|
| Hostname | EC2AMAZ-NV7TGIH |
| Private IPv4 | 172.31.18.99 |
| Public IPv4 | 98.89.31.73 |
| Instance size | t3.micro |
| Availability Zone | us-east-1c |
| Architecture | AMD64 |

**Result:** RDP connection successful — Windows desktop accessible remotely using the public IP and Windows administrator credentials.

---

## Task 3 — Connect to a Linux EC2 Instance Using PuTTYgen + PuTTY

**Objective:** Launch a Linux EC2 instance, convert the `.pem` private key to `.ppk` using PuTTYgen, and connect via SSH using PuTTY.

| Step | Action | Result | Screenshot |
|---|---|---|---|
| 1 | Launched Linux EC2 instance (Amazon Linux 2023 AMI) with a new key pair (`.pem`) | Instance running, public IP/DNS recorded | — |
| 2 | Configured Security Group to allow SSH (TCP port 22) from permitted source | Inbound rule added for SSH | — |
| 3 | Opened PuTTYgen, loaded the `.pem` file, exported it as `.ppk` | Private key converted successfully | — |
| 4 | Opened PuTTY, entered public IP/DNS, selected the `.ppk` key under SSH → Auth, connected | SSH session established | `05_task3_putty_ssh_connection.png` |
| 5 | Verified connection with `whoami` | Returned `ec2-user`, confirming successful login | `05_task3_putty_ssh_connection.png` |

**Result:**
- **Host:** `ip-172-31-18-112`
- **User:** `ec2-user`
- **Authentication:** Public key (`imported-openssh-key`)
- **Command run:** `whoami` → `ec2-user`

✅ PuTTY SSH session confirmed working using the PuTTYgen-converted `.ppk` key.

---

## Repository Structure

```
Task_screenshots/
├── 01_task1_before_scaling_t3micro.png
├── 02_task1_actions_change_instance_type.png
├── 03_task1_change_instance_type_page.png
├── 04_task1_after_scaling_verified.png
├── 05_task3_putty_ssh_connection.png
├── 06_task2_windows_rdp_connection.png
└── README.md
```

---

## Submission Checklist

- [x] Task 1 completed — EC2 instance type changed and verified
- [x] Task 1 screenshots attached
- [x] Task 2 completed — Windows EC2 launched and connected via RDP
- [x] Task 2 screenshot attached
- [x] Task 3 completed — Linux EC2 launched, `.pem` converted to `.ppk`, connected via PuTTY
- [x] Task 3 screenshot attached
- [x] No private keys, passwords, or sensitive credentials visible in screenshots

---

*Prepared for Fortune Cloud Technologies — Day 2 Task Submission (AWS EC2).*
