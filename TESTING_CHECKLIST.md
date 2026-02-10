# Integration Test Checklist ✅

## Google Apps Script Web App Integration

**Deployment URL:**

```
https://script.google.com/macros/s/AKfycbyD4XbAASJDg0NlmEcs2tNEewgN7m0egdjHuWqDePN8lPqg3I_9PdWoHbUztJhxj7QI/exec
```

---

## 🧪 Testing Steps

### 1. Test Registration Form

- [ ] Open `http://127.0.0.1:5500/index.html`
- [ ] Click **"Apply"** on any university card
- [ ] Fill in the registration form:
  - Name: TEST STUDENT
  - Phone: +998-90-123-4567
  - Message: (auto-filled)
- [ ] Click **"Submit"**
- [ ] Verify success message appears

### 2. Verify Firestore

- [ ] Open Firebase Console
- [ ] Navigate to Firestore Database
- [ ] Check `savedstudents` collection
- [ ] Find document named "TEST STUDENT"
- [ ] Verify all fields are present

### 3. Verify Google Sheets

- [ ] Open: <https://docs.google.com/spreadsheets/d/1dW9wdxoVdMyGmexJEFwf-Gsy4pH9I8iIpap8r5j94sY/edit>
- [ ] Go to "Leads" sheet
- [ ] Check for new row with test data
- [ ] Verify columns: TimeStamp, Name, phoneNumber, message

### 4. Verify Telegram Notification

- [ ] Check your Telegram app
- [ ] Look for message from your bot
- [ ] Verify it contains:
  - Student name
  - Phone number
  - Message
  - University name
  - Timestamp

### 5. Test Leads Dashboard

- [ ] Open `http://127.0.0.1:5500/leads.html`
- [ ] Verify test student appears
- [ ] Check statistics update (Total, Today, This Week)
- [ ] Test search functionality
- [ ] Test "Call" button (should open phone dialer)
- [ ] Test "Delete" button (with confirmation)

---

## 🔧 Troubleshooting

### If Google Sheets doesn't update

1. Check Apps Script execution logs:
   - Open Apps Script editor
   - Click "Executions" (clock icon)
   - Look for errors
2. Verify deployment:
   - Should be deployed as "Web app"
   - "Who has access" should be "Anyone"
3. Check browser console for errors

### If Telegram doesn't send

1. Verify `TELEGRAM_CHAT_ID` is set correctly in Apps Script
2. Make sure you've sent at least one message to the bot
3. Check bot token is correct
4. Review Apps Script logs

### If nothing happens

1. Open browser DevTools (F12)
2. Go to Network tab
3. Submit form again
4. Look for POST request to Google Script URL
5. Check for CORS errors (these are normal with `no-cors` mode)

---

## ✅ Expected Results

When everything works correctly:

1. **Firestore** ✓
   - Document created in `savedstudents`
   - All fields saved correctly

2. **Google Sheets** ✓
   - New row added to "Leads" sheet
   - Timestamp, Name, Phone, Message populated

3. **Telegram** ✓
   - Notification received
   - Contains all student details

4. **Leads Dashboard** ✓
   - Student appears in list
   - Statistics update
   - Actions work (Call, Delete)

---

## 🎯 Integration Status

- [x] Firebase/Firestore - **READY**
- [x] Google Apps Script URL - **CONFIGURED**
- [ ] Telegram Chat ID - **NEEDS SETUP** (if not done yet)
- [x] Google Sheets Structure - **READY**
- [x] Leads Dashboard - **READY**

---

## 📝 Notes

- The integration uses `mode: 'no-cors'` which is required for Google Apps Script
- You may see CORS warnings in console - this is normal and expected
- Data is sent even if you see the CORS warning
- For production, consider using a backend API instead of direct client calls

---

## 🚀 Production Checklist

Before going live:

- [ ] Remove test registrations from Firestore
- [ ] Clear test data from Google Sheets
- [ ] Verify all URLs are correct
- [ ] Test on different devices (desktop, mobile, tablet)
- [ ] Verify Telegram notifications work reliably
- [ ] Set up data backup strategy
- [ ] Document the process for your team

---

**Last Updated:** 2026-02-03  
**Status:** Integration URL Configured ✅
