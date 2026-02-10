# Google Sheets and Telegram Integration Setup Guide

This guide will help you set up automatic data saving to Google Sheets and Telegram notifications when students register.

## 📋 Overview

When a student submits the registration form, the following will happen:
1. ✅ Data saves to **Firestore** (already working)
2. ✅ Data saves to **Google Sheets** (new)
3. ✅ **Telegram notification** sent to you (new)

---

## 🔧 Setup Instructions

### Part 1: Get Your Telegram Chat ID

You need your Chat ID to receive notifications from the bot.

1. **Start a chat with your bot:**
   - Click this link: https://t.me/YOUR_BOT_USERNAME
   - (Replace YOUR_BOT_USERNAME with your actual bot username)
   - Send any message to the bot (e.g., "Hello")

2. **Get your Chat ID:**
   - Open this URL in your browser:
   ```
   https://api.telegram.org/bot8413365425:AAGm07CTjK_5rXVhNj-ehM-JBpGiMA1noNY/getUpdates
   ```
   
3. **Find your Chat ID in the response:**
   - Look for: `"chat":{"id":YOUR_CHAT_ID`
   - Copy that number (e.g., `123456789` or `-987654321`)
   - Save it for the next step

---

### Part 2: Set Up Google Apps Script

1. **Open your Google Sheet:**
   - Go to: https://docs.google.com/spreadsheets/d/1dW9wdxoVdMyGmexJEFwf-Gsy4pH9I8iIpap8r5j94sY/edit

2. **Open Apps Script Editor:**
   - Click: **Extensions** → **Apps Script**

3. **Replace the code:**
   - Delete any existing code in the editor
   - Open the file: `google-apps-script.js` (in your admissionapp folder)
   - Copy ALL the code from that file
   - Paste it into the Apps Script editor

4. **Update the Chat ID:**
   - Find this line in the script:
   ```javascript
   const TELEGRAM_CHAT_ID = 'YOUR_CHAT_ID';
   ```
   - Replace `YOUR_CHAT_ID` with the number you got from Part 1
   - Example:
   ```javascript
   const TELEGRAM_CHAT_ID = '123456789';
   ```

5. **Save the script:**
   - Click the **Save** icon (💾) or press `Ctrl+S`
   - Give it a name like "Student Registration Handler"

6. **Deploy as Web App:**
   - Click: **Deploy** → **New deployment**
   - Click the gear icon ⚙️ next to "Select type"
   - Choose: **Web app**
   - Set the following:
     - **Execute as:** Me (your email)
     - **Who has access:** Anyone
   - Click: **Deploy**
   - **Authorize the app** when prompted (click through all the warnings)

7. **Copy the Web App URL:**
   - After deployment, you'll see a **Web app URL**
   - It looks like: `https://script.google.com/macros/s/ABC123.../exec`
   - **COPY THIS URL** - you'll need it in the next step!

---

### Part 3: Update Your Website

1. **Open** `index.html` in your admissionapp folder

2. **Find this line** (around line 1220):
   ```javascript
   const GOOGLE_SCRIPT_URL = 'PASTE_YOUR_GOOGLE_APPS_SCRIPT_WEB_APP_URL_HERE';
   ```

3. **Replace it** with your Web App URL from Part 2 Step 7:
   ```javascript
   const GOOGLE_SCRIPT_URL = 'https://script.google.com/macros/s/YOUR_ACTUAL_URL/exec';
   ```

4. **Save the file**

---

## 🧪 Testing

### Test the Google Apps Script (Optional but Recommended)

1. In the Apps Script editor, select the `testScript` function from the dropdown
2. Click the **Run** button ▶️
3. Check:
   - ✅ A test row appears in your Google Sheet
   - ✅ You receive a Telegram notification

### Test the Full Integration

1. Open your website: `http://127.0.0.1:5500/index.html`
2. Click the **Apply** button on any university card
3. Fill in the registration form:
   - Name: TEST STUDENT
   - Phone: +998-90-123-4567
4. Click **Submit**
5. Verify:
   - ✅ Success message appears
   - ✅ Data appears in Firestore console
   - ✅ **NEW:** Data appears in Google Sheets "Leads" tab
   - ✅ **NEW:** You receive a Telegram notification

---

## 📊 Google Sheets Format

Your data will be saved in this format:

| TimeStamp | Name | phoneNumber | message |
|-----------|------|-------------|---------|
| 2/3/2026 18:33:09 | JOHN DOE | +998-90-123-4567 | I'm interested in Hanyang University, Please contact me! |

---

## 📱 Telegram Notification Format

You'll receive notifications like this:

```
🎓 New Student Registration!

👤 Name: JOHN DOE
📱 Phone: +998-90-123-4567
💬 Message: I'm interested in Hanyang University, Please contact me!
🏫 University: Hanyang University
⏰ Time: 03/02/2026, 18:33:09
```

---

## ⚠️ Troubleshooting

### "Script failed" or no data in Google Sheets
- Make sure you deployed the script as "Anyone can access"
- Check the Apps Script execution logs: View → Execution log

### No Telegram notification
- Verify your Chat ID is correct (must be a number)
- Make sure you started a chat with the bot first
- Check the Apps Script logs for errors

### CORS errors in browser console
- This is normal! We use `mode: 'no-cors'` which is expected
- The data still gets sent successfully

---

## 🎯 Summary

✅ **Firestore:** Saves student data (existing)
✅ **Google Sheets:** Automatically logs data to "Leads" sheet
✅ **Telegram:** Sends instant notification to you
✅ **Automatic:** All happens when student clicks Submit

---

## 📝 Configuration Summary

**Telegram Bot Token:** `8413365425:AAGm07CTjK_5rXVhNj-ehM-JBpGiMA1noNY`
**Google Sheet:** https://docs.google.com/spreadsheets/d/1dW9wdxoVdMyGmexJEFwf-Gsy4pH9I8iIpap8r5j94sY/edit
**Sheet Name:** `Leads`

You need to configure:
- [ ] Telegram Chat ID (from Part 1)
- [ ] Google Apps Script Web App URL (from Part 2)
