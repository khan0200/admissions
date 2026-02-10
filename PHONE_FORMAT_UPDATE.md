# Phone Number Format Update ✅

## 📱 Phone Number Storage Change

### Previous Format

- **Input:** `+998-XX-XXX-XXXX`
- **Saved to Database:** `+998-XX-XXX-XXXX`
- **Saved to Google Sheets:** `+998-XX-XXX-XXXX`

### New Format

- **Input:** `+998-XX-XXX-XXXX` (with auto-formatting)
- **Saved to Database:** `XXXXXXXXX` (only digits, no prefix)
- **Saved to Google Sheets:** `XXXXXXXXX` (only digits, no prefix)
- **Display in Leads:** `+998XXXXXXXXX` (prefix added for display)

---

## 🔄 How It Works

### 1. User Input

- User sees: `+998-XX-XXX-XXXX` in the input field
- Auto-formatting adds dashes as they type
- Looks exactly the same as before

### 2. Data Processing

When user clicks "Submit":

```javascript
// Original: +998-90-123-4567
// After removing prefix: 90-123-4567
// After removing dashes: 901234567
```

### 3. Storage

**Firestore:**

```json
{
  "phoneNumber": "901234567"  // No +998, no dashes
}
```

**Google Sheets:**

```
| phoneNumber  |
|--------------|
| 901234567    |
```

### 4. Display

When viewing in `leads.html`:

```
Stored: 901234567
Displayed: +998901234567
```

---

## ✨ Benefits

✅ **Cleaner Data**: No formatting in database  
✅ **Flexible**: Easy to add different country codes later  
✅ **Consistent**: All numbers stored the same way  
✅ **Easy to Process**: Pure digits easier to work with  
✅ **User-Friendly**: Still shows +998 when displaying  

---

## 📊 Examples

| User Input | Saved to DB | Displayed |
|------------|-------------|-----------|
| +998-90-123-4567 | 901234567 | +998901234567 |
| +998-91-456-7890 | 914567890 | +998914567890 |
| +998-99-888-7777 | 998887777 | +998998887777 |

---

## 🔍 Where to See Changes

### Firestore

1. Open Firebase Console
2. Go to Firestore Database
3. Open `savedstudents` collection
4. Phone numbers now show as: `901234567`

### Google Sheets

1. Open your Google Sheet
2. Go to "Leads" tab
3. Column C (phoneNumber) shows: `901234567`

### Telegram Notifications

Phone numbers in notifications will show the number as stored (without +998)

### Leads Dashboard

- Automatically adds +998 prefix for display
- Shows: `+998901234567`

---

## ⚙️ Technical Details

### Code Changes

**index.html (Registration):**

```javascript
// Strip +998 prefix from phone number before saving
const phoneNumber = phoneInput.value.replace('+998-', '').replace(/-/g, '');
```

**leads.html (Display):**

```javascript
// Add +998 prefix for display if not already present
let phoneFormatted = data.phoneNumber || 'N/A';
if (phoneFormatted !== 'N/A' && !phoneFormatted.startsWith('+998')) {
    phoneFormatted = '+998' + phoneFormatted;
}
```

---

## 🧪 Testing

### Test the New Format

1. **Submit a new registration:**
   - Input: `+998-90-123-4567`
   - Expected in Firestore: `901234567`
   - Expected in Google Sheets: `901234567`
   - Expected in Leads page: `+998901234567`

2. **Verify Call Functionality:**
   - Phone dialer should receive: `+998901234567`
   - Should work correctly on mobile devices

---

## 📝 Migration Note

**For Existing Data:**
Old registrations with `+998-XX-XXX-XXXX` format will still work:

- Will display correctly in leads dashboard
- Call functionality works with both formats
- No data migration needed

**For New Registrations:**

- All new submissions use the new format
- Only digits saved (no prefix, no dashes)

---

## ✅ Status

- [x] Input formatting unchanged (user experience same)
- [x] Database storage updated (digits only)
- [x] Google Sheets updated (digits only)
- [x] Display formatting added (shows +998 prefix)
- [x] Call functionality maintained
- [x] Backward compatible with old data

---

**Last Updated:** 2026-02-03  
**Status:** Phone Number Format Updated ✅
