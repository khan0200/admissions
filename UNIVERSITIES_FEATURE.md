# Universities Management Feature

## Overview
The Universities Management feature allows administrators to manage university options that appear in the admission form's university dropdown.

## Features Implemented

### 1. **Universities Button**
- Added a green "Universities" button in the header next to "View Leads" and "Add Admission"
- Opens the Universities Management modal

### 2. **Universities Modal**
- Displays all universities grouped by education level:
  - LANGUAGE COURSE
  - COLLEGE
  - BACHELOR
  - MASTER NO CERTIFICATE
  - MASTERS

- Each level group shows:
  - Level icon and name
  - Count badge showing number of universities in that level
  - Collapsible list of universities (click header to expand/collapse)

- Features:
  - Click on level header to expand/collapse the list
  - Each university shows its name and a delete button
  - Dark themed UI matching the application design

### 3. **Add University Modal**
- Click "+ Add University" button to open
- Two fields:
  - **University Name** (required)
    - Automatically converts to UPPERCASE
    - Placeholder: "AJOU UNIVERSITY (SUWON, GYEONGGI)"
  - **Education Level** (required)
    - Dropdown with 5 options:
      - LANGUAGE COURSE
      - COLLEGE
      - BACHELOR
      - MASTER NO CERTIFICATE
      - MASTERS

### 4. **Data Storage**
Universities are saved to Firestore collection `universities` with:
- `name`: University name (uppercase)
- `levelId`: Generated ID from level name (e.g., "bachelor", "master_no_cert")
- `levelName`: Full education level name (e.g., "BACHELOR")
- `createdAt`: Timestamp

### 5. **Integration**
- Universities automatically appear in the admission form's university dropdown
- Dropdown is filtered by selected education level
- When adding/editing admissions, only universities matching the selected level are shown

## Usage Instructions

1. **View Universities**:
   - Click the green "Universities" button in the header
   - Browse universities grouped by education level
   - Click on any level header to expand/collapse

2. **Add University**:
   - Click "Universities" button
   - Click "+ Add University" button
   - Enter university name (will be auto-converted to uppercase)
   - Select education level
   - Click "Save University"

3. **Delete University**:
   - Open Universities modal
   - Find the university you want to delete
   - Click the red "Delete" button
   - Confirm deletion

## Technical Details

### Firestore Structure
```javascript
{
  name: "BUSAN UNIVERSITY OF FOREIGN STUDIES (GEUMJEONG, BUSAN)",
  levelId: "bachelor",
  levelName: "BACHELOR",
  createdAt: serverTimestamp()
}
```

### Level ID Mapping
- LANGUAGE COURSE → language_course
- COLLEGE → college
- BACHELOR → bachelor
- MASTER NO CERTIFICATE → master_no_cert
- MASTERS → masters

### Key Functions
- `openUniversitiesModal()` - Opens the universities list modal
- `openAddUniversityModal()` - Opens the add university form
- `renderUniversitiesList()` - Loads and displays grouped universities
- `toggleUniversityLevel(levelId)` - Toggles collapse/expand of level group
- `deleteUniversity(id, name, level)` - Deletes a university
- `generateLevelId(levelName)` - Generates consistent level IDs

## Design Features
- Clean dark theme matching the application
- Smooth animations for expand/collapse
- Hover effects on university items
- Color-coded buttons (green for add, red for delete)
- Loading states while fetching data
- Toast notifications for success/error messages
