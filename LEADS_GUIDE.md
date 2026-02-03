# Leads Dashboard - User Guide

## 📊 Overview

The **leads.html** page is your central hub for viewing and managing all student registrations from the admission application.

![Leads Dashboard](preview image shows the beautiful iOS-style interface)

---

## ✨ Features

### 📈 **Statistics Dashboard**

- **Total Registrations**: All-time student registrations
- **Today**: Registrations from today
- **This Week**: Registrations from the last 7 days

### 🔍 **Search & Filter**

- Search by:
  - Student name
  - Phone number
  - University name
  - Message content
- Real-time filtering as you type

### 📇 **Student Cards**

Each registration card displays:

- **Student Name** (in uppercase)
- **Phone Number** (with formatted display)
- **University** they're interested in
- **Message** (auto-generated interest message)
- **Registration Time** (smart relative time: "2 hours ago", etc.)

### 🎯 **Quick Actions**

- **Call Button** (Green): Opens phone dialer to call the student
- **Delete Button** (Red): Removes the registration (with confirmation)

### 🔄 **Refresh**

- Click the "Refresh" button to reload the latest data from Firestore

---

## 🚀 How to Access

### From the Main Page

1. Open `index.html` in your browser
2. Click the **"View Leads"** button in the top-right corner
3. The leads dashboard opens

### Direct Access

- Navigate to: `http://127.0.0.1:5500/leads.html`
- Or open the file directly in your browser

---

## 💡 Usage Examples

### **View All Registrations**

1. Open leads.html
2. All registrations appear automatically
3. Scroll to browse through the list

### **Search for a Student**

1. Type in the search box:
   - Student name: "JOHN"
   - Phone: "998901234567"
   - University: "Hanyang"
2. Results filter instantly

### **Call a Student**

1. Find the student's card
2. Click the green **"Call"** button
3. Confirm the phone number
4. Your device's phone dialer opens

### **Delete a Registration**

1. Find the student's card
2. Click the red **"Delete"** button
3. Confirm the deletion
4. Registration is removed from Firestore

---

## 📱 Mobile Responsive

The leads dashboard is fully responsive and works great on:

- 💻 Desktop computers
- 📱 Tablets
- 📲 Mobile phones

---

## 🔗 Navigation

- **Back to Admissions**: Click the "← Back to Admissions" link at the top
- Returns you to the main admission cards page

---

## 🎨 Design Features

- **iOS-Style Design**: Premium glassmorphic cards
- **Smooth Animations**: Hover effects and transitions
- **Color-Coded Icons**: Blue for phone, purple for university
- **Relative Timestamps**: "2 hours ago" instead of raw dates
- **Smart Stats**: Auto-calculated registration statistics

---

## 🔥 Real-Time Data

- Data is loaded from **Firestore** `savedstudents` collection
- Click **Refresh** to get the latest registrations
- Deletions are instant and permanent

---

## 📊 Data Structure

Each student registration contains:

```
{
  name: "JOHN DOE",
  phoneNumber: "+998-90-123-4567",
  message: "I'm interested in Hanyang University, Please contact me!",
  universityName: "Hanyang University",
  admissionId: "abc123",
  registeredAt: "2026-02-03T18:42:36.000Z",
  timestamp: Firebase Timestamp
}
```

---

## ⚡ Quick Tips

1. **Use Search**: Quickly find students by typing any relevant keyword
2. **Check Today**: Monitor real-time registrations with the "Today" stat
3. **Call Direct**: One-click calling on mobile devices
4. **Keep Clean**: Delete test registrations to keep data organized
5. **Refresh Often**: Click refresh to see new registrations

---

## 🎯 Perfect For

- 📞 **Call Centers**: Quick access to student contact info
- 📊 **Managers**: Monitor registration statistics
- 🎓 **Admissions Team**: Track interested students
- 📈 **Marketing**: Measure campaign effectiveness

---

## 🔐 Security Note

This page is connected to the same Firestore database as your main application. Make sure to:

- Keep your Firebase credentials secure
- Only share this page with authorized team members
- Regular backups of your Firestore data

---

Enjoy your beautiful leads dashboard! 🎉
