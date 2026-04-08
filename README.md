# Gmail to Docs Summarizer

Automatically summarizes daily emails using Claude AI and saves them to Google Docs.

## What it does

- Monitors emails from one or more senders every day
- Summarizes them using Claude AI (Haiku model)
- Creates a separate Google Doc for each sender
- Saves the docs to a specified Google Drive folder
- Sends a notification email (and optionally Telegram) with links to the summaries

## Setup

### 1. Open Google Apps Script
Go to [script.google.com](https://script.google.com) and create a new project.

### 2. Paste the code
Copy everything from `email_summary_bot.gs` and paste it into the script editor.

### 3. Fill in the CONFIG values

```javascript
const CONFIG = {
  SENDER_EMAILS: [
    'email1@youremail.com',   // Emails to monitor
    'email2@youremail.com',
  ],
  FOLDER_ID:          'YOUR_FOLDER_ID',       // From your Google Drive folder URL
  CLAUDE_API_KEY:     'YOUR_CLAUDE_API_KEY',  // From console.anthropic.com
  NOTIFY_EMAIL:       'yournotifyemail@gmail.com',
  TELEGRAM_BOT_TOKEN: '',                     // Optional
  TELEGRAM_CHAT_ID:   '',                     // Optional
  TRIGGER_HOUR:       12,                     // Run at 12 PM daily
};
```

- **FOLDER_ID** — Open your Google Drive folder, copy the ID from the URL: `drive.google.com/drive/folders/THIS_PART`
- **CLAUDE_API_KEY** — Get it from [console.anthropic.com](https://console.anthropic.com) → API Keys

### 4. Set up the daily trigger
Select `setupDailyTrigger` from the function dropdown and click **Run** (only once).

### 5. Grant permissions
Google will ask you to allow access to Gmail, Drive, Docs, and external URLs. Accept all.

### 6. Test it
Select `runDailySummary` and click **Run**. Check the logs (View → Logs) to confirm it works.

## Notes

- The script runs daily at the hour set in `TRIGGER_HOUR` (24-hour format)
- Each sender gets a separate Google Doc named: `Email Summary - sendername - YYYY-MM-DD`
- Only emails from the last 24 hours are processed
