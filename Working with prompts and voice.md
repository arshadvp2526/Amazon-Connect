**Working with prompts and voice:**

## 📚 **Topic: Importing and Recording Prompts**

In Amazon Connect, prompts are used to play audio messages to customers during contact flows. These can be greetings, instructions, IVR menus, error messages, or hold announcements. You can either import custom audio files or create prompts using Amazon Polly's text-to-speech (TTS) engine.

---

## 🗂️ **1. Types of Prompts**

There are two main types of prompts in Amazon Connect:

- 🎧 **Pre-recorded Prompts**: Uploaded audio files (e.g., .wav format)
- 🗣️ **Text-to-Speech Prompts**: Generated in real time using Amazon Polly

---

## 🔁 **2. Creating or Importing Prompts**

### 📥 **A. Importing Pre-recorded Prompts**

**Step-by-Step:**
1. Prepare your audio file in **.wav format (8kHz, 16-bit PCM)**.
2. Go to **Amazon Connect Console** → **Routing** → **Prompts**.
3. Click **"Upload prompt"**.
4. Enter a prompt name.
5. Select and upload your audio file.
6. Save the prompt.

**Use Case:**  
Professional voice actors record brand-specific greetings or IVR messages for a consistent brand tone.

---

### 🎙️ **B. Recording Prompts (via External Tool)**

Amazon Connect doesn’t offer in-console recording, so you can record prompts using third-party tools like:

- Audacity (Free, open source)
- GarageBand (Mac)
- Voice recorders on mobile devices

**Tips:**
- Record in a quiet environment.
- Normalize and trim silence from the beginning/end.
- Export as mono `.wav`, 8kHz, 16-bit PCM.

---

### 🗣️ **C. Creating TTS Prompts with Amazon Polly**

Instead of importing audio, you can use **text-to-speech (TTS)** in contact flows:

1. Use the **"Play prompt"** block in a contact flow.
2. Choose **"Text-to-speech"** instead of a prompt file.
3. Enter the message.
4. Select a Polly voice (e.g., Joanna, Matthew, Raveena).
5. Optionally use **SSML** for emphasis, pauses, or language support.

**Use Case:**  
Dynamically speak order numbers, names, or estimated wait times.

---

## 🛠️ **3. Managing Prompts**

- Prompts are reusable across all flows in an Amazon Connect instance.
- You can **rename**, **delete**, or **replace** prompts anytime.
- Organize prompts with clear naming conventions:
  - `welcome_main.wav`
  - `ivr_option1.wav`
  - `error_generic.wav`

---

## 📊 **Comparison: TTS vs Pre-recorded Prompts**

| **Feature**         | **Text-to-Speech (TTS)**       | **Pre-recorded Audio**              |
|---------------------|--------------------------------|-------------------------------------|
| Setup Speed         | Instant                        | Requires recording & upload         |
| Personalization     | Dynamic with attributes        | Static                              |
| Voice Quality       | Robotic (but improving)        | Natural, human voice                |
| Branding Control    | Limited                        | Full control                        |
| Flexibility         | High (can use SSML)            | Low (requires new recording)        |

---

## ✅ **Best Practices**

- 🎙️ Use professional voice actors for brand-critical prompts.
- 🧠 Use TTS for dynamic or personalized messages.
- 🗂️ Maintain a naming convention for easy organization.
- 📁 Store a backup of all .wav files in Amazon S3 or version control.
- 🌍 Use multilingual support with Polly to localize prompts.

---

With Amazon Connect, you can balance TTS speed and flexibility with the polish of pre-recorded prompts, creating a seamless and scalable voice experience.





## 📚 **Topic: Applying Prompts in Scripts**

In Amazon Connect, once prompts are created or imported (via audio files or TTS), they can be applied within contact flows using **“Play prompt”** blocks. These scripts define how and when the audio messages are delivered to the customer or agent during the call journey.

---

## 🧱 **1. Using the “Play Prompt” Block

**🎯 Purpose:**  
To play a message — either a pre-recorded file or dynamic text — at any point in the customer interaction.

**🔧 Configurable Options:**
- Choose **pre-recorded prompt** from your prompt library
- Use **text-to-speech (TTS)** with Amazon Polly
- Insert **contact attributes** (e.g., name, queue wait time)
- Enable **SSML** tags for speech customization

---

## 🗣️ **2. Where Prompts Are Typically Applied in Scripts**

| **Use Case**               | **Block Type**         | **Prompt Purpose**                            |
|----------------------------|------------------------|-----------------------------------------------|
| Welcome Message            | Play Prompt            | Greet the caller when they connect            |
| IVR Menu Options           | Play Prompt            | “Press 1 for Sales, 2 for Support...”         |
| Queue Hold Message         | Customer Queue Flow    | Reassure customer while they wait             |
| Error or Invalid Input     | Play Prompt            | “Sorry, I didn’t understand that.”            |
| Whisper Flow to Agent      | Whisper Flow           | Alert agent with caller info                  |
| Callback Confirmation      | Play Prompt            | “You’ll receive a call shortly.”              |
| Post-call Thank You        | Play Prompt            | End call with a polite closing message        |

---

## 🧩 **3. Using Attributes in Prompts**

You can personalize prompts using **contact attributes** within TTS.

**Example:**
Hello, {CustomerName}. Your order number is {OrderID}.

Use these dynamic values inside Play Prompt blocks with text-to-speech enabled. The values must be set earlier in the contact flow using:
- **Set Contact Attributes**
- **Invoke AWS Lambda**
- **Customer input blocks**

---

## ✨ **4. Enhancing Prompts with SSML (Speech Synthesis Markup Language)**

Amazon Polly supports **SSML**, which allows you to control:
- **Pauses**: `<break time="1s"/>`
- **Emphasis**: `<emphasis level="strong">important</emphasis>`
- **Speech rate & pitch**
- **Language switching**

**Example:**
Example:

```xml
Hello <emphasis>John</emphasis>. Your balance is <break time="500ms"/> $245.
```

Use this format when configuring the text in a **TTS-enabled Play Prompt** block (check the "Use SSML" box).

---

### 📋 Best Practices for Applying Prompts

✅ Use short, clear, and friendly messages  
✅ Avoid long menus; break complex flows into subflows  
✅ Combine static prompts with TTS where personalization is needed  
✅ Always test your flow to ensure prompts play at the correct point  
✅ Store and reuse prompts to maintain consistency across flows  

Applying prompts correctly in Amazon Connect ensures that your contact flows **sound natural**, are **easy to navigate**, and deliver the **right information** to both customers and agents at the right time.


### 🌐 Creating Multilingual Flows Using Text-to-Speech

Amazon Connect allows you to build multilingual contact flows using **Text-to-Speech (TTS)** powered by **Amazon Polly**, which supports dozens of languages and voices.

---

### 🔧 Steps to Create a Multilingual Flow

1. **Identify Language Preferences**
   - Capture the customer’s preferred language using:
     - Menu options (e.g., "Press 1 for English, 2 for Spanish")
     - Stored customer profile attributes
     - Lambda function lookups

2. **Set Contact Attributes**
   - Use the **Set Contact Attributes** block to assign a value like:
     ```text
     Language = "en-US"
     ```
     or
     ```text
     Language = "es-ES"
     ```

3. **Use Play Prompt Blocks with TTS**
   - In **Play Prompt**, enable **Text-to-Speech**.
   - Choose the appropriate **language and voice**.
   - Insert the message to be spoken in the selected language.
   - Example:
     ```text
     Thank you for calling. Please hold while we connect you to an agent.
     ```

4. **Branch Logic Based on Language**
   - Use the **Check Contact Attribute** block to check the value of `Language`.
   - Route the call to different flows or prompts accordingly.

---

### 🌍 Example Language Codes (Amazon Polly)

| Language      | Code    | Voice Examples     |
|---------------|---------|--------------------|
| English (US)  | en-US   | Joanna, Matthew    |
| Spanish (ES)  | es-ES   | Conchita, Enrique  |
| French (FR)   | fr-FR   | Celine, Mathieu    |
| Hindi (IN)    | hi-IN   | Aditi               |
| German (DE)   | de-DE   | Hans, Marlene      |

---

### 🛠 Tips for Multilingual Flow Design

- ✅ Store messages in a central location or external service if scaling to many languages
- ✅ Always test each language flow thoroughly
- ✅ Use SSML to ensure correct pronunciation, pauses, and emphasis in different languages
- ✅ If using Lambda, structure responses to return language-specific text

---

Creating multilingual flows helps deliver a personalized and inclusive experience to customers from diverse linguistic backgrounds.

