n8n Inbox Manager: AI Email Classifier
An intelligent email automation workflow built with n8n that uses OpenAI and Google Gemini to monitor your Gmail inbox, categorize messages into specific buckets, and organize them automatically using Gmail labels.

How It Works
The workflow operates in two modes:

Auto-Categorize New Emails: Triggers every minute to process incoming mail.

Bulk Categorize Existing Emails: A manual trigger to process up to 12 recent emails at once.

Classification Logic
Emails are analyzed based on Subject, Body, and Sender info, then assigned to one of three categories:

PRIORITY: Important communications, specific project updates (Louai-PRIORITY), or trusted senders like contact@techniverge.ca.

Newsletter: High-volume content, marketing updates, or specific senders like hello@alchemy.com.

Subscriptions: Invoices, recurring service updates, or subscription-related keywords.

🛠️ Setup Instructions
1. Prerequisites
An n8n instance (Self-hosted or Cloud).

OpenAI API Key (for the primary Text Classifier).

Google Gemini API Key (as a backup/secondary model).

Gmail OAuth2 Credentials (configured in Google Cloud Console with gmail.modify scopes).

2. Import Workflow
Download the workflows/inbox-manager.json file from this repo.

In n8n, click on the Workflow menu (top right) > Import from File.

Select the downloaded JSON.

3. Critical Node Configuration (OpenAI Fix)
To prevent JSON parsing errors in the Text Classifier node when using OpenAI:

Open the OpenAI Chat Model node.

Ensure Use Responses API is toggled OFF.

This ensures the model returns a "Simple Message" that the Text Classifier can interpret correctly.

4. Categorization Customization
Open the Text Classifier nodes to modify the category descriptions.

Note: Do not add "Return only JSON" or "No Markdown" instructions to the descriptions; the node handles this automatically. Adding them manually can break the output parser.

🔧 Workflow Nodes Breakdown
Gmail Trigger: Polls the inbox every 60 seconds.

Text Classifier: The "Brain" of the workflow. It maps the email data to your predefined categories.

AI Chat Models: Provides the LLM logic (GPT-3.5/4 or Gemini) to the classifier.

Gmail (Add/Remove Labels): Executes the organization by applying labels and removing the "Inbox" label to archive processed mail.

⚠️ Known Issues & Troubleshooting
JSON Parsing Error: If you see Expected object, received array, double-check that the OpenAI node has "Responses API" disabled.

Label Not Found: Ensure the Label IDs in the Gmail nodes match the IDs in your specific Gmail account. You may need to re-select your labels after importing.

📜 License
This project is open-source. Feel free to fork and modify for your own personal inbox management.