## 🛡️ Compliance, Security, and Cost Management

Amazon Connect provides several features to ensure that your contact center meets compliance requirements, protects sensitive data, and remains cost-efficient.

---

### 🔐 KMS Integration and Encryption of Call Data

Amazon Connect supports encryption using **AWS Key Management Service (KMS)**, ensuring that sensitive data—such as call recordings and transcripts—are protected both at rest and in transit.

---

### 🔧 Enabling KMS for Amazon Connect

1. **Create or Select a Customer Managed Key (CMK):**
   - Go to the **KMS Console**
   - Create a new CMK or use an existing one
   - Enable key rotation for enhanced security

2. **Attach KMS Key to Amazon Connect:**
   - In **Amazon Connect Console**, go to **Data Storage**
   - Under **Call Recordings**, choose to **encrypt with KMS**
   - Select the desired CMK
   - Grant permissions to Amazon Connect using an IAM policy

---

### 📦 What Gets Encrypted?

| Data Type                  | Encryption Applied? |
|----------------------------|---------------------|
| Call Recordings            | ✅ Yes               |
| Chat Transcripts           | ✅ Yes               |
| Contact Trace Records (CTRs) | ✅ Yes            |
| Contact Lens Analytics     | ✅ Yes               |

---

### 🔄 How It Works

- When a call is recorded, the audio file is automatically encrypted using the selected KMS key.
- Only users or services with **Decrypt** permissions on the CMK can access the data.
- Access logs for key usage are recorded in **AWS CloudTrail** for auditing.

---

### 🔐 IAM Permissions Example

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "kms:Encrypt",
        "kms:Decrypt",
        "kms:GenerateDataKey"
      ],
      "Resource": "arn:aws:kms:region:account-id:key/key-id"
    }
  ]
}
