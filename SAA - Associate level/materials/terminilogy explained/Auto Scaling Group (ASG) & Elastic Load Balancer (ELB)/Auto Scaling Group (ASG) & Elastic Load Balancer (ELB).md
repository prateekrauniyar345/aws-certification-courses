## Auto Scaling Group (ASG) & Elastic Load Balancer (ELB)

These two always work together. ELB is the traffic director, ASG is the fleet manager. Together they give you **automatic scaling + high availability** without any manual intervention.

---

### The 2 pieces

**ELB (Elastic Load Balancer)** — sits in front of all your EC2 instances. Every incoming request hits the ELB first, and it decides which instance should handle it. It constantly health-checks your instances — if one goes down, it stops sending traffic there automatically. Three flavours: ALB (HTTP/HTTPS, most common), NLB (ultra-low latency TCP), and GLB (network appliances).

**ASG (Auto Scaling Group)** — watches your instances and automatically adds or removes them based on rules you define. You set three numbers: minimum instances (floor), maximum instances (ceiling), and desired capacity (target). When CPU spikes above 70%? Launch 3 more. When traffic drops at night? Terminate the extras and stop paying for them.

Together: **ASG manages how many instances exist, ELB manages which one gets each request.**

---

### Scaling policies

**Target tracking** — simplest. "Keep average CPU at 50%." ASG figures out how many instances to add/remove. Like cruise control.

**Step scaling** — "If CPU > 70%, add 2 instances. If CPU > 90%, add 5 instances." More granular control.

**Scheduled scaling** — "Every Friday at 5pm, scale up to 10 instances." Good for predictable traffic spikes.

---

### Real example

> Your e-commerce site normally runs on 2 EC2 instances. A flash sale starts:
> 1. Traffic spikes → CPU hits 80%
> 2. CloudWatch alarm triggers ASG
> 3. ASG launches 8 more instances (2 → 10)
> 4. ELB detects the new healthy instances and starts routing traffic to them
> 5. Sale ends → traffic drops → ASG terminates extra instances
> 6. Back to 2 instances, back to minimum cost

---
![Auto Scaling Group (ASG) & Elastic Load Balancer (ELB)](./Auto%20Scaling%20Group%20(ASG)%20&%20Elastic%20Load%20Balancer%20(ELB).png)
---
Here's how to read each section:

**Section 1 — ELB in action:** Requests from users hit the Load Balancer first. It fans traffic out to healthy instances only — EC2 #3 is unhealthy so ELB silently stops sending it requests. Users never notice. No manual intervention needed.

**Section 2 — Scale-out event:** Left side is normal — 2 instances, CPU at ~30%, cheap and calm. Then a flash sale hits, CPU spikes to 85%, CloudWatch fires an alarm, and ASG launches 8 more instances. ELB immediately detects the new healthy instances and starts routing to them. CPU drops back to a safe ~40% across all 10.

**Section 3 — The three numbers:** Minimum is your safety net (always at least 2 running for availability). Desired is your normal steady state. Maximum is your cost cap — ASG will never go above this no matter how much traffic comes in. Setting max correctly prevents surprise AWS bills.

**Section 4 — Scaling policies:** Target Tracking is the simplest and should be your default — just say "keep CPU at 50%" and AWS figures out the rest. Step Scaling gives you more control for aggressive spikes. Scheduled is for when you already know when traffic will hit. All three ultimately work through CloudWatch alarms firing at the bottom.