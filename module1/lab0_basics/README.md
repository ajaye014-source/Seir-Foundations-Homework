
# Cloud Server Launch Log & Quick Summary

## 1. Actual Screenshot Data Summary

| Deployment | Server Name / Tag | Instance ID | Public IP | Private IP | Uptime | Memory Used |
| --- | --- | --- | --- | --- | --- | --- |
| **Screenshot 1** | `blackvulcan_23_7` | `i-0bd6017a738515339` | `3.84.212.167` | `172.31.25.157` | 17 minutes | 155 MiB |
| **Screenshot 2** | `blackvulcan_22_7` | `i-0dd2391e3e9e0e490` | `54.89.201.242` | `172.31.27.66` | 6 minutes | 182 MiB |
| **Screenshot 3** | `myEC2review2` | `i-0d9c0462f69b3efc7` | `18.205.25.116` | `172.31.22.25` | 8 minutes | 174 MiB |

---

## 2. What Happened in Plain English

1. **Spinning Up Virtual Computers:**
I launched three separate virtual computers in the Amazon cloud (all using the `t3.micro` size running Amazon Linux 2023 in the `us-east-1c` data center zone).
2. **Connecting & Checking Specs:**
I opened a direct web connection (**EC2 Instance Connect**) to each machine one by one. Once logged in, the system displayed a customized welcome screen showing that each server had its own unique ID numbers and internet addresses:
* **First Machine (`blackvulcan_23_7`):** Had been running for 17 minutes and was using about 155 MB of memory.
* **Second Machine (`blackvulcan_22_7`):** Had been running for 6 minutes and was using about 182 MB of memory.
* **Third Machine (`myEC2review2`):** Had been running for 8 minutes and was using about 174 MB of memory.


3. **Verifying System Health:**
All three machines were idling smoothly with virtually 0% CPU usage and using only a small fraction of their total memory (under 200 MB out of ~913 MB) and hard drive space (1.7 GB used out of 8 GB available).

---

## 3. Key Takeaways

* **Every Cloud Server Gets Unique Badges:** Even when servers are built the exact same way, AWS assigns each one a unique internal ID (like `i-0bd6017a...`) and its own private and public IP addresses so they can be identified and reached over the internet.
* **Low CPU Doesn't Mean Free:** As the screen warning reminds us, just because a server is sitting idle at 1% CPU usage doesn't mean it's free—attached storage drives (EBS volumes) and active running time still incur costs if not cleaned up properly when finished.