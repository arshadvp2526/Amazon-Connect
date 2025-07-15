
## 📚 Types of Flows in Amazon Connect**

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



## 📚 Using and Understanding Flow Blocks**

Amazon Connect provides a wide set of drag-and-drop blocks to visually design contact flows. Each block performs a specific function, such as playing a message, checking conditions, routing calls, or invoking AWS services.

---

## 🧱 **1. Play Prompt**

**📝 Purpose:**  
Plays a recorded or text-to-speech message to the customer or agent.

**🔧 Configurable Options:**
- Use pre-recorded audio files (stored in Amazon S3)
- Use text-to-speech using Amazon Polly
- Add dynamic attributes (e.g., "Hello, {CustomerName}")

**📌 Use Case:**  
Greet customer with "Welcome to ABC Support."

---

## 🧱 **2. Set Queue**

**📝 Purpose:**  
Assigns the contact to a specific queue before placing it on hold or transferring it.

**🔧 Configurable Options:**
- Choose queue based on department, skill, or language
- Set dynamically using contact attributes or Lambda

**📌 Use Case:**  
Route billing queries to the Billing Queue.

---

## 🧱 **3. Check Attribute**

**📝 Purpose:**  
Evaluates contact, system, or user-defined attributes to control flow logic.

**🔧 Configurable Options:**
- Compare string, number, or boolean values
- Route contacts based on values like language, account status, etc.

**📌 Use Case:**  
If `language` = "es", route to Spanish-speaking agent.

---

## 🧱 **4. Loop**

**📝 Purpose:**  
Repeats a section of the flow until a condition is met or maximum attempts are reached.

**🔧 Configurable Options:**
- Maximum iterations
- Exit loop after success or failure

**📌 Use Case:**  
Repeat menu until valid input is received.

---

## 🧱 **5. Invoke AWS Lambda Function**

**📝 Purpose:**  
Calls a backend Lambda function to fetch or process data.

**🔧 Configurable Options:**
- Send contact attributes as input
- Receive results and store in new attributes

**📌 Use Case:**  
Fetch order status from an external system.

---

## 🧱 **6. Transfer to Queue**

**📝 Purpose:**  
Transfers the contact to the previously set queue.

**🔧 Configurable Options:**
- Timeout behavior
- Whisper prompt before transfer

**📌 Use Case:**  
Connect the customer to the next available agent.

---

## 🧱 **7. Disconnect / Hang Up**

**📝 Purpose:**  
Ends the contact flow for the customer.

**📌 Use Case:**  
After playing "Thanks for calling, goodbye!"

---

## 📊 **Summary Table of Common Blocks**

| **Block**                   | **Purpose**                                   | **Example Use**                               |
|-----------------------------|-----------------------------------------------|-----------------------------------------------|
| Play Prompt                 | Speak or play message to caller               | "Welcome to our support line"                 |
| Set Queue                  | Assign queue for routing                      | Set to "Technical Support"                    |
| Check Attribute            | Route flow based on variables                 | Language, customer type, priority             |
| Loop                       | Repeat part of flow                           | Menu retry on invalid input                   |
| Invoke AWS Lambda          | Get or process external data                  | Fetch user info from database                 |
| Transfer to Queue          | Connect contact to queue                      | Transfer to support after info gathered       |
| Disconnect / Hang Up       | End interaction                               | "Thank you, goodbye!"                         |

---



## 📚 **Contact Flow Best Practices**

Designing efficient and effective contact flows in Amazon Connect is essential for delivering a smooth customer experience. Well-structured flows improve call handling, reduce wait times, and empower agents with the right context.

---

## ✅ **1. Keep It Simple**

**🎯 Why:**  
Overly complex flows can lead to confusion, errors, and difficult maintenance.

**🛠️ How:**  
- Use clear naming for each block and flow
- Minimize branching and nesting
- Use reusable modules (subflows) for common tasks

---

## ✅ **2. Use Dynamic Attributes**

**🎯 Why:**  
Personalization improves customer satisfaction and context-aware routing.

**🛠️ How:**  
- Store values using “Set Contact Attributes”
- Retrieve from Lambda, Lex, or previous inputs
- Use in prompts: “Hello, {CustomerName}”

---

## ✅ **3. Always Handle Errors Gracefully**

**🎯 Why:**  
Unexpected errors can cause frustration and call drops.

**🛠️ How:**  
- Add error branches to every key block (e.g., Lambda, Transfer)
- Provide fallback messages like “We’re sorry, something went wrong.”

---

## ✅ **4. Use Lambda Functions Wisely**

**🎯 Why:**  
Lambda can make flows intelligent, but overuse can increase latency.

**🛠️ How:**  
- Use Lambda for essential lookups (account info, verification)
- Avoid calling Lambda repeatedly in loops or menus

---

## ✅ **5. Optimize Queues and Routing**

**🎯 Why:**  
Proper routing ensures the right agent handles the call efficiently.

**🛠️ How:**  
- Set Queue based on attributes like language or priority
- Use skills-based routing via Routing Profiles

---

## ✅ **6. Test Thoroughly Before Publishing**

**🎯 Why:**  
Small mistakes in logic can block entire call paths.

**🛠️ How:**  
- Use the built-in Contact Flow test simulator
- Simulate edge cases like silence, invalid inputs, errors

---

## ✅ **7. Document and Version Your Flows**

**🎯 Why:**  
Tracking changes and reasons helps teams maintain flows.

**🛠️ How:**  
- Add description in the flow editor
- Use naming conventions and dates (e.g., “Billing-IVR-v2”)
- Store exported JSON flow files in GitHub or backup systems

---

## ✅ **8. Reuse Common Prompts and Flows**

**🎯 Why:**  
Avoid duplicating content and reduce maintenance work.

**🛠️ How:**  
- Store audio in Amazon S3
- Create shared flows for greetings, authentication, or error handling

---

## ✅ **9. Use Whisper Flows for Agent Context**

**🎯 Why:**  
Giving agents information before the call improves efficiency and personalization.

**🛠️ How:**  
- Include customer name, issue type, VIP flag, etc.
- Combine with CRM integrations for deeper insights

---

## 📋 **Checklist for Well-Designed Contact Flows**

- [x] Clear and intuitive flow structure  
- [x] Proper queue and routing configuration  
- [x] Dynamic attributes for personalization  
- [x] All errors handled gracefully  
- [x] Tested with multiple scenarios  
- [x] Audio files stored in S3 and reused  
- [x] Flow documented and versioned

---

Following these best practices will help ensure that your Amazon Connect contact flows are scalable, maintainable, and deliver a world-class customer experience.

