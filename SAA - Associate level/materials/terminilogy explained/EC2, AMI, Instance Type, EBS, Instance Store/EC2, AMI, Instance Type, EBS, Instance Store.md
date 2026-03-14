## EC2, AMI, Instance Type, EBS, Instance Store

This is about **compute** — how you rent and configure virtual machines on AWS, and what storage you attach to them.

---

### The 5 pieces

**EC2 (Elastic Compute Cloud)** — a virtual machine running in AWS. You pick the OS, install software, and control everything — just like a real server, but rented by the hour. "Elastic" means you can start/stop/resize it anytime.

**AMI (Amazon Machine Image)** — the blueprint used to launch an EC2 instance. It's a frozen snapshot of an OS + software. Example: an AMI with Ubuntu 22.04 + Nginx pre-installed. You launch 10 instances from one AMI and they're all identical. You can use AWS-provided AMIs or build your own.

**Instance Type** — defines the hardware spec of your EC2. CPU, RAM, network speed. You pick based on your workload:
- `t3.micro` → tiny, cheap, burstable (dev/test)
- `m6i.xlarge` → balanced CPU+RAM (web servers)
- `c6i.2xlarge` → compute-optimized (ML, video encoding)
- `r6g.large` → memory-optimized (databases, caching)

**EBS (Elastic Block Store)** — a persistent hard drive that attaches to your EC2. Survives reboots and even instance termination (if configured). You can detach it from one instance and re-attach to another. Think of it like a USB hard drive — plug it in, plug it out. Use `gp3` for general purpose, `io2` for high-performance databases.

**Instance Store** — temporary storage physically attached to the host machine. Blazing fast, but **completely wiped** when the instance stops or reboots. Use it only for scratch data, caches, or temp files — never for anything you need to keep.

---

### Real example

> Launch a web server:
> 1. Pick AMI → Ubuntu 22.04 with Nginx
> 2. Pick instance type → `t3.medium` (2 vCPU, 4GB RAM)
> 3. Attach EBS `gp3` volume (20GB) → stores your app code and logs
> 4. Instance store → used for temp session cache (wiped on restart, that's fine)

---
![EC2, AMI, Instance Type, EBS, Instance Store](./EC2,%20AMI,%20Instance%20Type,%20EBS,%20Instance%20Store.png)
---

---Here's how to read each section:

**Section 1 — AMI → EC2:** One AMI launches 3 identical EC2 instances. The AMI is the frozen blueprint; EC2s are the live copies running from it. Change the AMI once, re-launch, and every new instance gets the update.

**Section 2 — Instance types:** Four families, each optimized for a different job. `t3` is cheap and burstable for low-traffic workloads. `m6i` is the balanced default for most web servers. `c6i` maximizes CPU for heavy computation. `r6g` maximizes RAM for in-memory databases.

**Section 3 — EBS vs Instance Store:** This is the most important distinction. EBS on the left is like a USB hard drive — plug in, plug out, data always safe. Instance Store on the right is physically glued to the host — blindingly fast, but the data vanishes the moment you stop or reboot the instance. Never store anything important on instance store.

**Section 4 — EBS types:** `gp3` is your default 90% of the time. Use `io2` only when you need extremely high IOPS (e.g. Oracle, MySQL in production). `st1` is cheap spinning-disk storage for large sequential reads like log archives.