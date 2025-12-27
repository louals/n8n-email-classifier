# 📧 n8n Inbox Manager: AI Email Classifier

An intelligent **email automation workflow built with n8n** that uses **OpenAI (GPT)** and **Google Gemini** to:

- Monitor your Gmail inbox in real time
- Categorize emails into smart buckets
- Automatically organize them using Gmail labels

---

## ⚙️ How It Works

The workflow runs in **two modes**:

### 🔄 1. Auto-Categorize New Emails
- Runs **every minute**
- Processes new incoming emails automatically

### 📦 2. Bulk Categorize Existing Emails
- Manual trigger
- Processes **up to 12 recent emails at once**

---

## 🧠 Classification Logic

Each email is analyzed using:

- **Subject**
- **Body content**
- **Sender information**

Then it gets assigned to one of these 3 categories:

| Category | Description |
|---|---|
| **PRIORITY** | Important messages, project updates *(Louai-PRIORITY)*, or trusted senders like `contact@techniverge.ca` |
| **Newsletter** | Marketing content, high-volume updates, or senders like `hello@alchemy.com` |
| **Subscriptions** | Invoices, recurring services, and subscription-related keywords |

---

## 🛠️ Setup Instructions

### 1. Prerequisites
Make sure you have:

- An **n8n instance** (Cloud or Self-hosted)
- **OpenAI API Key**
- **Google Gemini API Key**
- **Gmail OAuth2 Credentials** with `gmail.modify` scopes enabled

> OAuth must be configured in **Google Cloud Console** using the `gmail.modify` permission.

---

### 2. Import Workflow

1. Download `workflows/inbox-manager.json` from the repo
2. In n8n, go to:
Workflow Menu (top-right) → Import from File

3. Select the downloaded JSON

---

### 3. Critical OpenAI Node Fix

To avoid JSON parsing issues in the classifier:

1. Open the **OpenAI Chat Model node**
2. Ensure:

- **Use Responses API → OFF**

This ensures the classifier receives a **simple message output** instead of JSON arrays that break parsing.

---

### 4. Customize Your Categories

- Open the **Text Classifier nodes**
- Edit the **category descriptions** freely
- **Do NOT manually add instructions like:**


(The node already handles formatting internally and adding them manually can break parsing.)

---

## 🔧 Workflow Nodes Breakdown

| Node | Purpose |
|---|---|
| **Gmail Trigger** | Checks inbox every 60 seconds |
| **Text Classifier** | Assigns category using AI |
| **OpenAI/Gemini Models** | Provide LLM reasoning |
| **Add/Remove Gmail Labels** | Applies labels and archives email |

---

## ⚠️ Known Issues & Troubleshooting

### ❗ JSON Parsing Error
If you see:


→ Disable **Responses API** in the OpenAI node *(see Step 3 above)*

### 🏷️ Label Not Found
→ Re-select labels after importing and ensure Label IDs match your Gmail account

---

## 📜 License

This project is **open-source** — fork it, remix it, modify it, it’s your inbox kingdom 👑
