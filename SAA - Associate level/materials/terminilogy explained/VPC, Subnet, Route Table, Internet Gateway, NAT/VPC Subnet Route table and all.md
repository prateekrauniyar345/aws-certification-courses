## VPC, Subnet, Route Table, Internet Gateway, NAT

This is all about **network design** — how you isolate, connect, and protect your AWS resources from each other and the internet.

---

### The 5 pieces

**VPC (Virtual Private Cloud)** — your own isolated network bubble inside AWS. Like buying a plot of land and putting a fence around it. Nothing enters or leaves unless you explicitly allow it. You define the IP range, e.g. `10.0.0.0/16`.

**Subnet** — you slice your VPC into smaller zones called subnets. Each subnet gets its own IP range. The key decision: **public** (reachable from internet) vs **private** (internal only). Rule of thumb: anything a user directly hits goes in public; everything else goes private.

**Route Table** — every subnet has one. It's a simple list of rules: "where should traffic go?" A public subnet's route table has a rule pointing internet traffic (`0.0.0.0/0`) to the IGW. A private subnet's table has no such rule — so internet traffic simply has nowhere to go.

**Internet Gateway (IGW)** — the single front door of your entire VPC. Attach one IGW per VPC. Only resources in *public subnets* with a route to the IGW can be reached from the internet.

**NAT Gateway** — solves a specific problem: your private EC2/app servers need to *download* something from the internet (OS patches, npm packages) but you don't want the internet able to reach them. NAT sits in the public subnet and acts as a middleman — forwards outbound requests, hides the private IP, blocks all inbound.

---

### Real example

> 3-tier web app:
> - Users hit your **Load Balancer** → public subnet
> - LB forwards to **App Servers** → private subnet (invisible to internet)
> - App servers query **RDS Database** → private subnet (most locked down)
> - App servers use **NAT** to pull software updates — outbound onlyHere's how to read it layer by layer:


---
![VPC, Subnet, Route Table, Internet Gateway, NAT](./VPC,%20Subnet,%20Route%20Table,%20Internet%20Gateway,%20NAT.png)
---

**Internet → IGW** — all public traffic enters through the single Internet Gateway. Two-way arrows because users both send requests and receive responses.

**Public Subnet** — the Load Balancer and Web Servers live here. They have public IPs and a route table pointing to the IGW, so the internet can reach them. The NAT Gateway also sits here — it needs internet access to forward outbound requests on behalf of private servers.

**Private Subnet A (App tier)** — App servers have *no* public IP and *no* route to the IGW. The only way in is from the web servers above. Their route table points outbound traffic to the NAT Gateway (dashed line) — so they can download patches but can't be reached from outside.

**Private Subnet B (DB tier)** — the most locked-down layer. RDS has no internet route at all — not even NAT. Only the app servers in Subnet A can talk to it. The primary and replica sync with each other across AZs for redundancy.

**The golden rule** at the bottom says it all: traffic flows strictly downward — Internet → Public → App → DB. Nothing from a lower layer can initiate upward to the internet.