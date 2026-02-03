# Google Apps Script Update Instructions ✅

## 📋 What Changed

Added phone number formatting for Telegram notifications to make them more readable.

### Before Update

```
📱 Phone: 901234567
```

### After Update

```
📱 Phone: +998-90-123-4567
```

---

## 🔄 How to Update

### Step 1: Open Google Apps Script

1. Open your Google Sheet:

   ```
   https://docs.google.com/spreadsheets/d/1dW9wdxoVdMyGmexJEFwf-Gsy4pH9I8iIpap8r5j94sY/edit
   ```

2. Click: **Extensions** → **Apps Script**

---

### Step 2: Update the Code

1. **Select all existing code** (Ctrl+A)
2. **Delete it all**
3. **Open** the file: `google-apps-script.js` (in your admissionapp folder)
4. **Copy all content** from that file
5. **Paste** into the Apps Script editor
6. Click **Save** (💾)

---

### Step 3: Re-deploy

Since the code changed, you need to create a new version:

1. Click **Deploy** → **Manage deployments**
2. Click the **Edit** icon (✏️ pencil) next to your existing deployment
3. Under "Version", select: **New version**
4. Click **Deploy**
5. Click **Done**

**✅ Your Web App URL stays the same - no changes needed in index.html**

---

## 📊 What This Update Does

### 1. Google Sheets

- **No change**: Still saves `901234567` (digits only)
- This is correct ✅

### 2. Telegram Notifications

- **Before**: Shows `901234567` (hard to read)
- **After**: Shows `+998-90-123-4567` (formatted, easy to read)
- Much better! ✅

### 3. New Function Added

```javascript
formatPhoneNumber(phoneNumber)
```

- Takes: `901234567`
- Returns: `+998-90-123-4567`
- Applied only to Telegram message (not to Sheets)

---

## 🧪 Testing

### Quick Test

1. In Apps Script editor, select `testScript` function
2. Click **Run** ▶️
3. Check Telegram notification
4. Phone should show: `+998-90-123-4567` ✅

### Full Test

1. Submit a registration on your website
2. Check Telegram notification
3. Verify phone number is formatted: `+998-XX-XXX-XXXX`
4. Check Google Sheets - should still be: `XXXXXXXXX` (digits only)

---

## ✅ Summary

**What's Updated:**

- [x] Phone number formatting function added
- [x] Telegram notifications now show formatted phone
- [x] Google Sheets still saves raw digits
- [x] Multiple recipients still working (2 chat IDs)

**What Stays Same:**

- [x] Web App URL unchanged
- [x] Google Sheets storage format (digits only)
- [x] Your website code (no changes)
- [x] All other functionality

---

## 📝 Expected Results

After updating and testing:

| Location | Format | Example |
|----------|--------|---------|
| Website Input | +998-XX-XXX-XXXX | +998-90-123-4567 |
| Firestore | XXXXXXXXX | 901234567 |
| Google Sheets | XXXXXXXXX | 901234567 |
| Telegram | +998-XX-XXX-XXXX | +998-90-123-4567 |
| Leads Page | +998XXXXXXXXX | +998901234567 |

---

## 🎯 Benefits of This Update

✅ **Better Readability**: Easy to read phone numbers in Telegram  
✅ **Professional**: Formatted notifications look cleaner  
✅ **Click to Call**: Some Telegram clients can detect formatted numbers  
✅ **Consistent**: Matches user's input format  
✅ **Clean Data**: Database still has clean digits  

---

**Last Updated:** 2026-02-03  
**Status:** Code Ready - Needs Deployment  
**Action Required:** Update and re-deploy Google Apps Script
