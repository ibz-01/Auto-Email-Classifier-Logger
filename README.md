# 📧 AI Email Identifier (n8n + Google Gemini)

Automatically analyzes incoming Gmail messages using Google Gemini AI and identifies potential spam or promotional emails by applying a Gmail label.

This workflow demonstrates AI-powered email classification using **n8n**, **Gmail**, **Google Gemini**, and **Google Sheets**.

---

## Features

- 📥 Monitors new Gmail messages
- 🤖 Uses Google Gemini AI to classify each email
- 🏷️ Applies a **"Potential Spam"** Gmail label to emails classified as promotional or unnecessary
- ✅ Leaves important emails unchanged
- 📝 Logs every AI decision to Google Sheets, including:
  - Sender
  - Time processed
  - AI reasoning
- ⚡ Runs automatically using the Gmail Trigger

---

## Workflow

```
Gmail Trigger
      │
      ▼
Google Gemini AI
      │
      ▼
Structured Output Parser
      │
      ▼
IF (DELETE?)
     │
 ┌───┴────┐
 │        │
 ▼        ▼
Apply      Log as Keep
"Potential
Spam" Label
 │
 ▼
Log to Google Sheets
```

---

## How It Works

Every new email is sent to Google Gemini with instructions to classify it.

If the email is determined to be:

- Advertisement
- Promotion
- Newsletter
- Marketing
- Social notification
- Coupon
- Product update
- Other low-value automated email

the workflow **adds the "Potential Spam" Gmail label**.

Otherwise, the email is left untouched.

Every decision is also logged to Google Sheets for review.

---

## Setup

1. Import `workflow.json` into n8n.
2. Connect your Gmail OAuth2 credentials.
3. Connect your Google Gemini API credentials.
4. Connect your Google Sheets credentials.
5. Create a Gmail label named **Potential Spam** (or update the workflow to use your preferred label).
6. Activate the workflow.

---

## Example

**Incoming Email**

> 🎉 Save 60% on our Summer Collection!

**AI Response**

```json
{
  "action": "DELETE",
  "reason": "Promotional marketing email advertising a sale."
}
```

**Workflow Result**

- ✅ Applies the **Potential Spam** label in Gmail.
- ✅ Records the sender, timestamp, and AI reason in Google Sheets.
- ✅ Does not permanently delete the email.

---

## Future Improvements

- Move labeled emails to Trash automatically.
- Automatically unsubscribe from newsletters.
- Support Outlook and Microsoft 365.
- User-configurable whitelist and blacklist.
- Daily AI summary of processed emails.
