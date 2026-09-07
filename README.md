# Gmail Multi-Label Email Processor (n8n)

Automated n8n workflow that monitors multiple Gmail labels, extracts key email information, logs it into Google Sheets, and organizes attachments into a structured Google Drive folder hierarchy.

---

## Problem Statement

Manually managing emails across multiple labels is time-consuming and error-prone. Important attachments often get lost, sender information is hard to track, and organizing files by label, date, and sender requires constant manual effort. This leads to wasted time and incomplete records.

---

## Solution

This workflow automatically:

- Monitors selected Gmail labels at regular intervals
- Extracts sender name, email address, subject, date, and label information
- Appends structured data to a Google Sheet
- Downloads any attachments
- Creates a clean folder structure in Google Drive: Label → YYYY-MM-DD → Sender Name
- Uploads attachments while preserving their original filenames

---

## Tech Stack

- **n8n** – Workflow automation
- **Gmail API** – Email monitoring and attachment download
- **Google Sheets API** – Data logging
- **Google Drive API** – File storage and folder management
- **OAuth2** – Secure authentication

---

## Architecture / Flow
Gmail Trigger (polls selected labels)
↓
Extract & Clean Data (sender, subject, date, labels)
↓
Append row to Google Sheets
↓
IF email has attachments?
↓ Yes
Split each attachment
↓
Search / Create Label folder
↓
Search / Create Date folder (YYYY-MM-DD)
↓
Search / Create Sender folder
↓
Upload original attachment (keeps original filename)



---

## Features

- Supports multiple Gmail labels
- Automatically creates nested folders only if they don’t already exist
- Preserves original attachment filenames
- Cleans sender names for safe folder naming
- Logs every processed email into Google Sheets
- Fully automated and runs on a schedule

---

## How to Use

1. Import the workflow JSON into your n8n instance
2. Connect the following credentials:
   - Gmail OAuth2
   - Google Sheets OAuth2
   - Google Drive OAuth2
3. Update these values in the workflow:
   - Gmail Label IDs
   - Google Spreadsheet ID
   - Sheet name
4. (Optional) Adjust the polling interval in the Gmail Trigger
5. Activate the workflow

Once activated, any new email under the selected labels will be processed automatically.

---

## Google Sheet Structure (Recommended)

| Date | From Name | From Email | Subject | Label | Message ID | Has Attachments | Attachment Count |
|------|-----------|------------|---------|-------|------------|-----------------|------------------|

---

## Future Improvements

- Add AI-based email classification (using Gemini or GPT) to automatically apply labels
- Implement duplicate detection before writing to Google Sheets
- Add Slack or email notifications for high-priority emails
- Support for larger files and media groups
- Create a simple analytics dashboard in Google Sheets

---

## Notes

- Make sure to replace all credential placeholders before running the workflow
- Test with a single label first before enabling multiple labels
- Folder names are cleaned of special characters to avoid Google Drive errors

---

**Built with n8n**