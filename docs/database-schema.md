# Database Schema

This document outlines the proposed structure for storing user data, meetings, question bank, and subscriptions using **Firebase Firestore**. All sensitive media (e.g., screenshots, reports, teaching materials) will be stored in **Google Drive**, not in Firestore.

---

## 🧑 Teachers Collection (`teachers`)

| Field           | Type     | Description |
|----------------|----------|-------------|
| uid            | string   | Firebase Auth ID |
| name           | string   | Full name |
| country        | string   | country |
| city           | string   | province or city |
| language       | string   | language |
| email          | string   | Email address |
| students       | array    | List of student IDs |
| parents        | array    | List of parent IDs |
| classrooms     | array    | List of classrooms IDs |
| subscription   | object   | Stripe or PayPal subscription info |
| notifications  | object   | Preferences for reminders, reports, etc. |

---

## 🧑 Students Collection (`students`)

| Field           | Type     | Description |
|----------------|----------|-------------|
| uid            | string   | Firebase Auth ID |
| name           | string   | Full name |
| country        | string   | country |
| city           | string   | province or city |
| language       | string   | language |
| email          | string   | Email address |
| teachers       | array    | List of teacher IDs |
| parent         | string   | parent ID |
| classrooms     | array    | List of classrooms IDs |
| notifications  | object   | Preferences for reminders, reports, etc. |

---

## 🧑 Parents Collection (`parents`)

| Field           | Type     | Description |
|----------------|----------|-------------|
| uid            | string   | Firebase Auth ID |
| name           | string   | Full name |
| country        | string   | country |
| city           | string   | province or city |
| language       | string   | language |
| email          | string   | Email address |
| teachers       | array    | List of teacher IDs |
| students       | array    | List of student IDs |
| classrooms     | array    | List of classrooms IDs |
| notifications  | object   | Preferences for reminders, reports, etc. |

---

## 🗕️ Classrooms Collection (`classrooms`)

| Field           | Type       | Description |
|----------------|------------|-------------|
| id             | string     | Classroom ID |
| teacherId      | string     | Owner of the meeting |
| students       | array      | Object of student ID, Google Drive Folder URL, Screen locked?, email parent when leave full-screen? |
| dateTime       | timestamp  | Start time |
| frequency      | number     | every number of days |
| duration       | number     | Duration in minutes |
| allClassScreenLocked | boolean    | All students Screen locked? |
| teacherDrive   | string      | Google Drive Folder URL to store materials, classwork, and homework |
| majorCountry        | string   | country in the majority |
| majorCity           | string   | province or city in the majority |
| majorLanguage       | string   | language in the majority |

---

## ❓ Question Bank Collection (`questions`)

| Field               | Type     | Description |
|--------------------|----------|-------------|
| id                 | string   | Question ID |
| subject            | string   | e.g., "Math", "Science" |
| country            | string   | country |
| city               | string   | province or city |
| language           | string   | language |
| topic              | string   | e.g., "Algebra", "Calculus" |
| difficulty         | string   | 'easy', 'medium', 'hard' |
| anonymizedQuestion | string   | Modified version with changed names, numbers, and context by AI |
| withGraphs         | number   | Number of graphs |
| typesOfGraphs      | array    | Types (e.g., bar, line) |
| graphData          | array    | Multi-dimensional data (e.g., coordinates) |
| withTables         | number   | Number of tables |
| tableHeadings      | array    | Headings for each table |
| tables             | array    | Table data as 2D arrays |
| withPictures       | number   | Number of images |
| pictures           | array    | [pictureId, OCR text] |
| steps              | array    | Step-by-step solution |
| variables          | object   | Editable variables (e.g., {a: 5, b: 12}) |
| template           | string   | Question format with placeholders |
| hints              | array    | Hints from teachers or AI |
| answer             | string   | Final answer or pattern |
| tags               | array    | Tags for filtering/search |

> ⚠️ All questions must be anonymized before storage to avoid copyright issues.

---

## 💳 Subscriptions Collection (`subscriptions`)

| Field       | Type      | Description |
|------------|-----------|-------------|
| id         | string    | Document ID |
| userId     | string    | Linked user ID |
| provider   | string    | 'stripe' or 'paypal' |
| planType   | string    | e.g., 'basic', 'pro' |
| amount     | number    | Monthly billing amount |
| status     | string    | 'active', 'canceled', etc. |
| createdAt  | timestamp | Start time |

---

## ☁️ Storage Notes (Google Drive)

Instead of storing large media files in the database, each user connects their **Google Drive**, and files are stored as follows:

### 👨‍🏫 Teacher Folder Structure
```
(Date-Topic)/
  ├── Teaching Materials screenshots/
  ├── All Students Classwork screenshots/
  ├── Homework screenshots – [Due Date]/
  └── All Students Learning Reports/
```

### 👩‍🎓 Student Folder Structure
```
(Date-Topic)/
  ├── Teaching Materials screenshots/
  ├── Your Classwork screenshots/
  ├── Homework screenshots – [Due Date]/
  └── Learning Report/
```

> ⚠️ We **do not** store raw screenshots, whiteboard images, or learning reports in Firebase. All files are referenced via Google Drive file IDs.

> ✅ Classwork data (like questions, student answers, durations, etc.) is stored **only in the frontend** memory for generating reports and then cleared.

---

