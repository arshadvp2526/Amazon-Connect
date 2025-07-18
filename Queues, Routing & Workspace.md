# 🎯 Queues, Routing & Agent Workspace Module

## 🧵 Creating and Configuring Queues

In Amazon Connect, **queues** are used to hold customer contacts (calls, chats, tasks) until an available agent can respond. Each queue represents a **specific service, department, or priority level**.

---

### 🧱 What Is a Queue?

A queue temporarily stores customer interactions when:

- All agents are busy  
- A specific skillset is required  
- Business rules define delays or routing logic  

Contacts remain in the queue until an agent with the appropriate routing profile becomes available.

---

### 🛠️ How to Create a Queue

1. Log in to **Amazon Connect Admin Console**
2. Navigate to **Routing > Queues**
3. Click **Add new queue**
4. Fill in the following details:

| Field                  | Description                                                      |
|------------------------|------------------------------------------------------------------|
| **Queue name**         | Internal name (e.g., `SalesQueue`, `TechSupport`)               |
| **Description**        | Optional explanation for clarity                                |
| **Hours of operation** | Set when this queue is active (refer to business hours config)  |
| **Quick connects**     | Assign shortcuts to other destinations or teams                 |
| **Outbound caller ID** | Optional for outbound calls                                      |

5. Click **Save**

---

### 🧭 Assigning Queues in Contact Flows

Use the **Set Queue** block in a contact flow to determine:

- Where the contact is held  
- What music or prompts are played  
- Which agents can handle the contact  

Example: Route callers who press "1" for billing into the `BillingQueue`.

---

### 🔁 How Queues Work with Routing

When a contact enters a queue:

- It waits until an agent with a matching **routing profile** is available  
- If no agent is available, it continues to wait or triggers fallback logic (e.g., voicemail, callback)

---

### 📊 Monitoring Queues

Use the **Amazon Connect dashboard** to monitor:

- Queue size  
- Wait times  
- Service levels  
- Abandonment rates  

You can also set alerts for long queue times or SLA breaches.

---

### ✅ Best Practices

- Name queues clearly for visibility (e.g., `Support_Level1`, `Escalation_Team`)  
- Align queues with accurate **business hours**  
- Use separate queues for different channels (voice, chat) if needed  
- Assign agents only to queues relevant to their skills  
- Regularly review queue performance and optimize routing logic  

---

Proper queue configuration ensures that customers are routed efficiently, agents are productive, and wait times remain low.
