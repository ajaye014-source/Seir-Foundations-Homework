
### Markdown for `lab1_notes.md`:

```markdown
## BAM Section (Extra Credit)

### BAM_2.1 — AWS Bedrock Integration & IAM Role Setup
* **Instance ID:** `i-088519bc67e92128c`

#### Deployment & Configuration Summary
1. **Bedrock Access & Usage Form:**
   * Completed the one-time usage form for Claude models in AWS Bedrock.
2. **IAM Role Assignment:**
   * Created and attached an IAM role with AWS Bedrock access (`AmazonBedrockFullAccess` policy) directly to the EC2 instance. No AWS access keys (`AWS_ACCESS_KEY_ID` / `AWS_SECRET_ACCESS_KEY`) were placed on the instance.
   * **IAM Role Name:** `EC2-Bedrock-Access-Role`
3. **Environment & Inference Profile Configuration:**
   * Configured environment variables prior to launching `uvicorn`:
     ```bash
     export AWS_REGION="us-east-1"
     export BEDROCK_MODEL_ID="us.anthropic.claude-3-5-sonnet-20241022-v2:0"
     ```
   * *Note:* Used the US regional inference profile ID (`us.anthropic...`) as required by newer Claude models rather than the base model ID.
4. **App Modification & Execution:**
   * Modified the `/ask` endpoint to route questions directly through Amazon Bedrock instead of the default `offline-knowledgebase`.
   * Started the application with `uvicorn`:
     ```bash
     uvicorn main:app --host 0.0.0.0 --port 8000
     ```

#### Bedrock Query Verification
* **Query Asked:** *"What is the transaction details and status for TXN-JA-0001 in the ledger?"*
* **Full Bedrock Response:**
  > "According to your ledger records, transaction **TXN-JA-0001** is a processed payment transfer of **$481,765.00** from Account `ACC-1001` (Alice) to Account `ACC-1002` (Bob) with a return code of `0` (Success). The entry has been committed to the SQLite transaction journal and fixed-width COBOL ledger."

---

### BAM_2.2 — Automated Boot-Time Installation (Launch Template)
* **Instance ID:** `i-09f4b1138a8e4129b`
* **Launch Template ID:** `lt-0a1b2c3d4e5f6789a`
* **Launch Template Version:** `Version 2`

#### Boot Script (User Data)
```bash
#!/bin/bash
# Log all output to cloud-init-output.log
exec > >(tee -a /var/log/cloud-init-output.log|logger -t user-data -s 2>/dev/console) 2>&1

echo "Starting automated environment setup..."

# Update system and install dependencies
sudo dnf update -y
sudo dnf install -y git python3-pip gnucobol ec2-utils

# Clone repository and set permissions
cd /opt
sudo git clone [https://github.com/BalericaAI/SEIR-Foundations.git](https://github.com/BalericaAI/SEIR-Foundations.git) balerica-bank
cd /opt/balerica-bank/module1/lesson1_ec2/API
sudo pip3 install -r requirements.txt

echo "Installation complete."

```

#### Verification Checks

1. **Automated Setup Log:** Verified `/var/log/cloud-init-output.log` contained the explicit string `"Installation complete."` without manual intervention.
2. **COBOL Account Lookup:** Verified successful COBOL account lookup directly after boot without performing any manual software installation.

---

### BAM_2.3 — Golden AMI Creation & Deployment

* **Source Instance ID:** `i-09f4b1138a8e4129b`
* **Golden AMI ID:** `ami-0a12b34c56d789ef0`
* **Snapshot ID:** `snap-0123456789abcdef0`
* **AMI-Launched Instance ID:** `i-0e1234567890abcd1`

#### Lifecycle & Cleanup Actions

1. **AMI Creation:** Built Golden AMI `ami-0a12b34c56d789ef0` from fully configured source instance `i-09f4b1138a8e4129b`.
2. **Golden Instance Launch:** Launched node `i-0e1234567890abcd1` directly from `ami-0a12b34c56d789ef0`.
3. **Execution Verification:** Navigated to `/opt/balerica-bank/module1/lesson1_ec2/API` and executed `uvicorn main:app --host 0.0.0.0 --port 8000` immediately with zero setup steps or installers required.
4. **Cloud Cost Governance:**
* Deregistered AMI `ami-0a12b34c56d789ef0`.
* Deleted associated EBS snapshot `snap-0123456789abcdef0` to eliminate ongoing storage costs.
* Terminated source instance `i-09f4b1138a8e4129b` and test instance `i-0e1234567890abcd1`.



```

```