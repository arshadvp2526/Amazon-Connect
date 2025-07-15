# 🔄 **Amazon Connect – Contact Flows Module**

## 📚 **Topic: Types of Flows in Amazon Connect**

Amazon Connect offers multiple flow types to handle different stages of customer interactions. Each flow is triggered based on where the customer is in their journey — from initial contact to call routing, waiting, or post-interaction handling.

---

## 🧩 **1. Contact Flow**

**🎯 Purpose:**  
The main workflow that handles how inbound contacts (voice/chat) are processed.

**📌 Used For:**
- IVR Menus (e.g., “Press 1 for Support”)
- Lambda integrations (e.g., fetch order status)
- Queue routing
- Authentication & data collection
- Agent connection

**📞 Example Use Case:**  
A customer calls your number → Hears greeting → Presses 2 for billing → Routed to billing queue.

---

## 🧩 **2. Customer Queue Flow**

**🎯 Purpose:**  
Triggered while a customer is waiting in queue after being routed by the Contact Flow.

**📌 Used For:**
- Playing announcements  
- Providing estimated wait times  
- Offering callbacks or alternatives

**⏳ Example Use Case:**  
“Your expected wait time is 4 minutes. Press 1 to request a callback.”

---

## 🧩 **3. Hold Flow**

**🎯 Purpose:**  
Plays when the **agent** puts the customer on hold during an active conversation.

**📌 Used For:**
- Playing hold music  
- Sharing helpful info (e.g., “Stay tuned while we pull up your details”)

**🎧 Example Use Case:**  
The agent places the call on hold → Music or custom message plays for the customer.

---

## 🧩 **4. Whisper Flow**

**🎯 Purpose:**  
Plays to the **agent** before they accept the inbound interaction — not heard by the customer.

**📌 Used For:**
- Sharing customer context  
- VIP alerts  
- Preferred language or script cue

**👂 Example Use Case:**  
“Caller is a returning customer. Last ticket: technical issue.”

---

## 🧩 **5. Outbound Whisper Flow**

**🎯 Purpose:**  
Plays to the **agent** when making outbound calls using Amazon Connect.

**📌 Used For:**
- Presenting script prompts  
- Displaying customer history before the call connects

**📤 Example Use Case:**  
“Calling for post-sale feedback. Customer purchased Laptop X on July 5th.”

---

## 📊 **Summary Table**

| **Flow Type**           | **Plays To**     | **When It Plays**                         | **Purpose**                                |
|-------------------------|------------------|-------------------------------------------|--------------------------------------------|
| Contact Flow            | Customer         | At start of interaction                   | IVR, routing, logic, data collection       |
| Customer Queue Flow     | Customer         | While waiting in queue                    | Messages, wait times, callback options     |
| Hold Flow               | Customer         | When agent places them on hold            | Hold music or reassurance                  |
| Whisper Flow            | Agent            | Before answering an inbound interaction   | Contextual alert or script briefing        |
| Outbound Whisper Flow   | Agent            | Before initiating outbound interaction    | Outbound context or script                 |

---

## ✅ **Best Practices**

- 🌀 **Re-use flow blocks** across types to keep things DRY (Don't Repeat Yourself)  
- 🗣️ Use **dynamic attributes** like customer name or issue to personalize whisper flows  
- 🎼 Choose music or messages that reduce anxiety during queue/hold  
- 🧠 Use **Lambda and Contact Attributes** to pass data across flow types  
- 🔄 Always **test flows** using the built-in Contact Flow test simulator
