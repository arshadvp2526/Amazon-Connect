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
