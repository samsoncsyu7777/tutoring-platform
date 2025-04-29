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

## 📄 Classwork Collection (`classwork`)

| Field           | Type     | Description |
|----------------|----------|-------------|
| id             | string   | Classwork ID |
| assignedBy     | string   | Teacher UID |
| assignedTo     | array    | Student UIDs |
| createdAt      | timestamp| Creation time |
| questions      | array    | List of `questionId`s |
| meetingId      | string   | Optional link to a meeting |
| isHomework     | boolean  | True if homework |
| editableTemplate | boolean| True if numbers/names randomized |

---

## ❓ Questions Collection (`questions`)

| Field           | Type     | Description |
|----------------|----------|-------------|
| id             | string   | Question ID |
| subject        | string   | e.g., "Math", "Science" |
| topic          | string   | e.g., "Algebra", "Calculus" |
| difficulty     | string   | 'easy', 'medium', 'hard' |
| steps          | array    | Breakdown of the solution |
| variables      | object   | Editable variables (e.g., {a: 5, b: 12}) |
| template       | string   | Question with placeholders |
| answer         | string   | Final answer or pattern |
| tags           | array    | For search/filtering |

---

## 🧑‍🎓 Student Work (`classworkSubmissions`)

| Field           | Type     | Description |
|----------------|----------|-------------|
| id             | string   | Submission ID |
| studentId      | string   | Who submitted |
| questionId     | string   | From which question |
| attempts       | array    | List of answers and timestamps |
| aiFeedback     | array    | List of AI comments |
| timeSpent      | number   | Total time in seconds |
| isCorrect      | boolean  | Final result |
| hintTriggered  | boolean  | Did the student need a hint? |

---

## 📊 Reports (`reports`)

| Field           | Type     | Description |
|----------------|----------|-------------|
| id             | string   | Report ID |
| meetingId      | string   | Optional link |
| studentId      | string   | Reported student |
| summary        | string   | Final summary by teacher or AI |
| skillStats     | object   | Breakdown by skill or step |
| submittedAt    | timestamp| Finalized time |
| sharedWithParent | boolean| Sent to parent? |

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

- Screenshots, teaching materials → Firebase Storage
- Whiteboard JSON → Saved as downloadable files
- Google Drive backup copies synced per user

Thank you, Open AI
