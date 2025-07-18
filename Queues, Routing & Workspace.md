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


## **Routing Profiles and Queue Priorities**

### **What is a Routing Profile?**
A **Routing Profile** in Amazon Connect defines how contacts are routed to agents. It determines:
- **Which queues** an agent can receive contacts from.
- **Priority order** of those queues.
- **Channels** the agent supports (voice, chat, tasks).
- **Concurrency** allowed for each channel.

### **Key Components of a Routing Profile**
| Component         | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| **Queues**        | The list of queues an agent can receive contacts from.                     |
| **Priority**      | Determines the order in which contacts from queues are routed to the agent.|
| **Channel Settings** | Maximum concurrent contacts per channel (e.g., 1 voice + 3 chats).          |
| **Default Outbound Queue** | Queue used for outbound calls when not associated with a flow.         |

---

### **Setting Queue Priorities**
In the routing profile, you can:
- Assign **multiple queues** to an agent.
- Set a **priority number** (lower number = higher priority).
- Define **delay** between receiving contacts from different queues.

| Priority | Queue Name     | Delay (seconds) |
|----------|----------------|-----------------|
| 1        | PremiumSupport | 0               |
| 2        | GeneralSupport | 5               |

This means the agent will first get contacts from `PremiumSupport`. If there are no contacts in that queue for 5 seconds, Amazon Connect will then try `GeneralSupport`.

---

### **Best Practices**
- Group queues logically based on **service type** or **customer segment**.
- Use priority and delay settings to ensure **critical contacts are handled first**.
- Regularly review routing profiles to match **staffing and skill changes**.

Routing profiles help you **control agent workload**, ensure **timely responses**, and maintain **efficient queue management**.


## **Transfer to Queue and Set Queue Behavior**

### **Transfer to Queue**

The **Transfer to Queue** block in Amazon Connect contact flows is used to route a contact to a specific queue. This allows the system to place the contact into a waiting state until an available agent from that queue can answer.

**Common Use Cases:**
- Route customers to specialized departments (e.g., billing, tech support).
- Send calls to language-specific queues.
- Re-route based on customer input or data from Lambda functions.

**Configuration Fields:**
- **Queue**: Choose the specific queue the contact should be transferred to.
- **Timeout**: Define how long to wait before failing over.
- **At Capacity Handling**: Set behavior when the queue is full.
- **Callback**: Enable if the customer should be offered a callback instead of waiting.

---

### **Set Queue Behavior**

The **Set Queue Behavior** block is used **before transferring** a contact to a queue to define how that queue should behave for this particular contact.

**Settings in this Block:**

| Option                    | Description                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| **Disconnect when queue is full** | Ends the call if no agents are available and the queue is at capacity.    |
| **Offer callback**               | Offers the customer a callback instead of waiting in the queue.          |
| **Timeout behavior**             | What happens when a contact waits in queue longer than the defined time. |

**Example Flow Sequence:**
1. Set customer attributes.
2. Use **Set Queue Behavior** to define queue rules.
3. Use **Transfer to Queue** to place contact in queue.

---

### **Best Practices**
- Always configure fallback logic in case the queue is full or times out.
- Use **dynamic routing** by setting queue values via Lambda or attributes.
- Combine **Set Queue Behavior** with **Customer Queue Flow** for a customized experience.
- Test different scenarios (e.g., no agent, full queue, long wait times).

Proper configuration of **Transfer to Queue** and **Set Queue Behavior** ensures smooth routing, reduces customer frustration, and improves first contact resolution.


## **Agent Workspace vs. CCP (Contact Control Panel)**

Amazon Connect offers two interfaces for agents to manage contacts: the **Agent Workspace** and the classic **CCP (Contact Control Panel)**. Understanding the differences helps organizations choose the best tool for their workflows.

---

### **Agent Workspace**

**Agent Workspace** is a modern, customizable interface introduced by Amazon Connect to provide a more integrated experience.

**Key Features:**
- 📋 **Task-based UI**: Manage multiple tasks (calls, chats, tasks) in a single view.
- 🧠 **Step-by-step guides**: Integrated with **wisdom** or custom workflows.
- 🔍 **Context-aware interface**: Shows customer info, previous interactions, and recommended actions.
- 🧩 **Extensibility**: Add custom components using Amazon Connect **UI extensions**.
- 🔄 **Automatic screen pops** based on customer attributes.

**Ideal For:**
- Complex use cases
- Organizations needing unified agent tools
- Multi-channel handling (chat, voice, tasks)

---

### **CCP (Contact Control Panel)**

The **CCP** is the classic dialer-like interface used for basic contact handling.

**Key Features:**
- 📞 Simple call controls: Accept, hold, transfer, and end call.
- 🔁 Transfer to queue or agent
- ✅ Lightweight and easy to embed into CRM systems
- ⛔ No task or workflow automation

**Ideal For:**
- Basic call center needs
- Embedding inside other tools (like Salesforce or Zendesk)
- Lightweight deployments

---

### **Comparison Table**

| Feature                         | Agent Workspace            | CCP (Contact Control Panel) |
|-------------------------------|----------------------------|-----------------------------|
| Interface Type                | Full dashboard             | Lightweight widget          |
| Task Management               | Yes                        | No                          |
| Chat & Voice Support          | Yes                        | Voice only                  |
| Customization & Extensions    | High (with APIs & UI apps) | Limited                     |
| Screen Pops & Automation      | Yes                        | No                          |
| Ideal Use Case                | Complex, modern workflows  | Simple voice-only tasks     |

---

### **Best Practice Tip**
Start with **Agent Workspace** if you want a scalable, modern solution with full visibility and control. Use **CCP** only when a minimal voice interface is sufficient.




