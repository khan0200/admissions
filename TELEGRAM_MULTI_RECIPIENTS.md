# Multiple Telegram Recipients Configuration ✅

## 📱 Telegram Configuration

### Recipients Configured

Notifications will be sent to **2 chat IDs**:

1. **Chat ID:** `1438936922`
2. **Chat ID:** `1426320861`

---

## 🔄 How It Works

When a student submits a registration:

1. Data saves to **Firestore**
2. Data saves to **Google Sheets**
3. **Telegram notifications** sent to **BOTH** recipients simultaneously

---

## 📊 Notification Details

**Both recipients will receive:**

```
🎓 New Student Registration!

👤 Name: STUDENT NAME
📱 Phone: +998-XX-XXX-XXXX
💬 Message: I'm interested in...
🏫 University: University Name
⏰ Time: 03/02/2026, 18:51:44
```

---

## ✅ Setup Steps

### 1. Update Google Apps Script

**IMPORTANT:** You need to update the script in Google Sheets:

1. Open: <https://docs.google.com/spreadsheets/d/1dW9wdxoVdMyGmexJEFwf-Gsy4pH9I8iIpap8r5j94sY/edit>
2. Click: **Extensions** → **Apps Script**
3. **Delete all existing code**
4. Copy the entire content from: `google-apps-script.js`
5. Paste it into the Apps Script editor
6. Click **Save** (💾)
7. **Re-deploy**: Click **Deploy** → **Manage deployments**
8. Click the **Edit** icon (pencil) on your existing deployment
9. Change "Version" to **New version**
10. Click **Deploy**

**Note:** The Web App URL will remain the same, no need to update index.html

---

## 🧪 Testing

### Test the Script (Recommended)

1. In Apps Script editor, select `testScript` from the dropdown
2. Click **Run** ▶️
3. Check:
   - ✅ Both recipients receive Telegram notification
   - ✅ Data added to Google Sheets
4. Check execution logs for any errors

### Test Full Integration

1. Open: `http://127.0.0.1:5500/index.html`
2. Click "Apply" on any card
3. Fill and submit the form
4. Verify:
   - ✅ Success message appears
   - ✅ Data in Firestore
   - ✅ Data in Google Sheets
   - ✅ **BOTH users** receive Telegram notification

---

## 📋 Success Indicators

After submission, the script will report:

```
"Sent to 2 out of 2 recipients"
```

If one fails:

```
"Sent to 1 out of 2 recipients"
```

Check Apps Script logs for details if not all recipients receive the notification.

---

## ⚠️ Important Notes

### Recipient Requirements

- Both chat IDs must have **started a chat** with your bot
- If a recipient hasn't messaged the bot, their notification will fail
- The script will still succeed if at least 1 recipient gets the message

### Error Handling

- If one recipient fails, the other will still receive the notification
- Errors are logged in Apps Script execution logs
- The overall operation succeeds if at least one notification is sent

---

## 🔍 Troubleshooting

### If a recipient doesn't receive notifications

1. **Verify they started the bot:**
   - Each person must send at least one message to the bot first
   - Visit: <https://t.me/YOUR_BOT_USERNAME>

2. **Verify Chat ID is correct:**
   - Each user should check their own chat ID
   - Visit: <https://api.telegram.org/bot8413365425:AAGm07CTjK_5rXVhNj-ehM-JBpGiMA1noNY/getUpdates>
   - Look for their chat ID in the response

3. **Check Apps Script logs:**
   - Open Apps Script editor
   - Click **Executions** (clock icon)
   - Look for errors related to specific chat IDs

---

## 📝 Summary

**Configuration:**

- ✅ 2 Telegram recipients configured
- ✅ Chat IDs: 1438936922, 1426320861
- ✅ Notifications sent simultaneously
- ✅ Error handling for individual failures

**Next Step:**

- Update the Google Apps Script (follow steps above)
- Test with a registration
- Verify both recipients receive notifications

---

**Last Updated:** 2026-02-03  
**Status:** Configuration Ready - Needs Script Update
