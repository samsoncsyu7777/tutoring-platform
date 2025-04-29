# Database Schema

This document outlines the proposed structure for storing user data, meetings, classwork, homework, whiteboards, reports, and subscriptions using **Firebase Firestore**.

---

## 🧑 Users Collection (`users`)

| Field           | Type     | Description |
|----------------|----------|-------------|
| uid            | string   | Firebase Auth ID |
| name           | string   | Full name |
| email          | string   | Email address |
| role           | string   | 'student', 'teacher', or 'parent' |
| studentOf      | array    | Teacher IDs (for parents/students) |
| driveLinked    | boolean  | Whether Google Drive is connected |
| googleDriveId    | string  | Google Drive ID for storing class materials and student work |
| subscription   | object   | Stripe or PayPal subscription info |
| notifications  | object   | Preferences for reminders, reports, etc. |

---

## 📅 Meetings Collection (`meetings`)

| Field           | Type       | Description |
|----------------|------------|-------------|
| id             | string     | Meeting ID |
| teacherId      | string     | Owner of the meeting |
| studentIds     | array      | Attendees |
| dateTime       | timestamp  | Start time |
| duration       | number     | Duration in minutes |
| classworkId    | string     | Linked classwork ID |
| isLocked       | boolean    | Screen locked? |
| emailOnBlur    | object     | Map of student ID → boolean |
| screenshots    | array      | List of image URLs (classwork or lecture) |

---

## ❓ Question Bank Collection (`questions`)

| Field               | Type     | Description |
|----------------    |----------|-------------|
| id                 | string   | Question ID |
| subject            | string   | e.g., "Math", "Science" |
| topic              | string   | e.g., "Algebra", "Calculus" |
| difficulty         | string   | 'easy', 'medium', 'hard' |
| anonymizedQuestion | string   | The modified question with anonymized numbers, names, and context |
| withGraphs         | number   | Number of graphs in the question |
| typesOfGraphs      | array    | Types of each Graph |
| graphaData         | array    | multiple dimension of array to store the anonymized data or x,y coordinates of each graph |
| withTables         | number   | number of tables in the question |
| tablesHeadings     | array    | Headings of tables |
| tables             | array    | arrays of two dimension arrays to store all anonymized cells of each table |
| withPictures       | number   | number of pictures in the question |
| pictures           | array    | [pictureId, image to text] Please create a new image and convert into text and store here|
| steps              | array    | Breakdown of the solution |
| variables          | object   | Editable variables (e.g., {a: 5, b: 12}) |
| template           | string   | Question with placeholders |
| hints              | array    | All hints written by teachers or AI |
| answer             | string   | Final answer or pattern |
| tags               | array    | For search/filtering |


> **Note:** All questions that are stored in the question bank will be anonymized to avoid any copyright violations. This will include modifying any real names, places, numbers, or contexts before storing them in the database.

---


## 💳 Subscriptions (`subscriptions`)

| Field           | Type     | Description |
|----------------|----------|-------------|
| id             | string   | Firebase doc ID |
| userId         | string   | Linked to user |
| provider       | string   | 'stripe' or 'paypal' |
| planType       | string   | 'basic', 'pro', etc. |
| amount         | number   | Monthly cost |
| status         | string   | 'active', 'canceled', etc. |
| createdAt      | timestamp| Start time |

---

## ☁️ Storage Notes

- Screenshots, teaching materials, reports → Google Drive
- Whiteboard JSON → Saved as downloadable files
- Google Drive backup copies synced per user

Thank you, Open AI
