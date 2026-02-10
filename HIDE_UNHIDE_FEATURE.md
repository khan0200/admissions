# Hide/Unhide Feature - Implementation Guide

## ✅ Feature Overview

Admins can now **hide** admissions from the public page without deleting them. This allows you to:
- Archive closed admissions
- Update dates and information while hidden
- Unhide when ready to reopen
- Keep historical data intact

---

## 🎯 How It Works

### **Admin Panel (`add.html`)**

#### 1. **Action Buttons**
Each admission card now has **4 buttons** in the card-actions area:

| Button | Icon | Color | Function |
|--------|------|-------|----------|
| **View** | 👁️ | Blue | View details |
| **Edit** | ✏️ | Orange | Edit admission |
| **Hide/Unhide** | 👁️‍🗨️/👁️ | Gray/Blue | Toggle visibility |
| **Delete** | 🗑️ | Red | Delete permanently |

#### 2. **"Show Hidden" Filter**
- Located in the filter section (next to search and level dropdown)
- **Unchecked (default):** Hidden admissions are not displayed
- **Checked:** Shows all admissions including hidden ones

#### 3. **Visual Indicators for Hidden Cards**
When an admission is hidden:
- **Opacity reduced** to 60% (faded appearance)
- **Gray badge** displays "👁️‍🗨️ HIDDEN" next to the round badge
- **Eye icon** button shows open eye (ready to unhide)

#### 4. **Workflow Example**

```
1. Admission is live → Students can see it on public page
2. Round closes → Click hide button (eye-slash icon)
3. Confirm hide → Card fades, shows "HIDDEN" badge
4. Update information while hidden → Edit dates, info, etc.
5. Ready to reopen → Click unhide button (eye icon)
6. Confirm unhide → Card visible again on public page
```

---

## 💾 Data Structure

### **Firestore Field Added:**
```javascript
{
    // ... existing fields
    isHidden: true,  // Boolean: true = hidden, false/undefined = visible
    updatedAt: ServerTimestamp
}
```

---

## 🎨 Visual Design

### **Hidden Badge:**
- **Background:** Linear gradient gray (#8e8e93 → #636366)
- **Icon:** `bi-eye-slash`
- **Size:** 9px font, small badge
- **Position:** Next to round badge in card header

### **Hide/Unhide Button:**

**When Visible (Hide button):**
- Background: `#f5f5f7` (light gray)
- Icon: `bi-eye-slash` (crossed eye)
- Color: `#8e8e93`
- Hover: Darker gray

**When Hidden (Unhide button):**
- Background: `#e6f7ff` (light blue)
- Icon: `bi-eye` (open eye)
- Color: `#007aff` (blue)
- Hover: Darker blue

---

## 🔒 Public Page Behavior

### **index.html (Public View)**

**Automatic filtering:**
```javascript
const isNotHidden = !admission.data.isHidden;
return matchesSearch && matchesLevel && isNotHidden;
```

**Students will:**
- ✅ See only visible admissions
- ❌ Never see hidden admissions
- ✅ No indication that hidden admissions exist

---

## 🧪 Testing Checklist

### **Admin Panel Tests:**

- [ ] **Hide Admission**
  - Click eye-slash icon on visible card
  - Confirm dialog shows university name
  - Card fades to 60% opacity
  - "HIDDEN" badge appears
  - Button changes to unhide (open eye)

- [ ] **Unhide Admission**
  - Click eye icon on hidden card
  - Confirm dialog shows university name
  - Card returns to full opacity
  - "HIDDEN" badge disappears
  - Button changes to hide (eye-slash)

- [ ] **Show Hidden Filter**
  - Default: Hidden cards not shown
  - Check "Show Hidden": Hidden cards appear (faded)
  - Uncheck: Hidden cards disappear

- [ ] **Edit Hidden Admission**
  - Hide an admission
  - Click edit button
  - Update dates/info
  - Save successfully
  - Unhide when ready

### **Public Page Tests:**

- [ ] **Visible Admissions**
  - All non-hidden admissions appear
  - Search and filter work normally

- [ ] **Hidden Admissions**
  - Hidden admissions do not appear
  - No trace of hidden records
  - Count doesn't include hidden

---

## 💡 Use Cases

### **1. Seasonal Admissions**
```
September: Create admission with "EXPECTED: Oct - Nov"
November: Open admissions, update dates, unhide
December: Close admissions, hide the card
January: Keep hidden while preparing next year
Next September: Update dates, unhide again
```

### **2. Rolling Admissions**
```
Round 1 closes → Hide
Update for Round 2 → Edit while hidden
Round 2 ready → Unhide with new dates
Round 2 closes → Hide again
```

### **3. Archive Without Delete**
```
Keep 3 years of admission history
Hide old years
Only show current year on public page
Admins can reference old data when needed
```

---

## 🔄 Database Updates

### **Hide an Admission:**
```javascript
await updateDoc(doc(db, 'admissions', id), {
    isHidden: true,
    updatedAt: serverTimestamp()
});
```

### **Unhide an Admission:**
```javascript
await updateDoc(doc(db, 'admissions', id), {
    isHidden: false,
    updatedAt: serverTimestamp()
});
```

---

## 🚨 Important Notes

1. **Non-destructive:** Hiding does NOT delete data
2. **Reversible:** Can unhide anytime
3. **Public safety:** Hidden = invisible to students
4. **Admin control:** Only admins can see/manage hidden cards
5. **Searchable:** Hidden cards still searchable when "Show Hidden" is checked

---

## 🎯 Future Enhancements (Optional)

1. **Bulk Actions:** Hide/unhide multiple admissions at once
2. **Auto-hide:** Automatically hide when announcement date passes
3. **Hide Reasons:** Add optional note explaining why hidden
4. **History Log:** Track when admission was hidden/unhidden
5. **Scheduled Unhide:** Set future date to auto-unhide

---

## 📁 Files Modified

1. **add.html** (Admin Panel)
   - Lines 636-666: Added "Show Hidden" filter
   - Lines 314-336: CSS for hide/unhide buttons
   - Lines 826-929: Card rendering with hidden badge
   - Lines 845-856: Filter function with hidden check
   - Lines 945-989: Toggle hide/unhide function
   - Line 1267: Event listener for showHiddenFilter

2. **index.html** (Public View)
   - Lines 1073-1089: Filter to exclude hidden admissions

---

## ✨ Summary

The hide/unhide feature gives you full control over admission visibility without losing data. Perfect for managing seasonal admissions, updating information privately, and maintaining a clean public interface.

**Workflow in 3 steps:**
1. 👁️‍🗨️ **Hide** when closed
2. ✏️ **Edit** while hidden
3. 👁️ **Unhide** when ready
