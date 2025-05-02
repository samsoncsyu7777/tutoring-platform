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
| payment        | object   | Stripe or PayPal payment info |
| subscription   | object   | annually or monthly? add screen lock? add AI feedback? number of hours left? currency? amount? promotion code?
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
| age            | number   | increase by one automatically at 23:59 August 31 |
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
| students       | array      | Object of student ID, Google Drive Folder URL, Screen locked?, email parent when leave full-screen?, send lesson report?, save materials into student Google Drive Folder? |
| dateTime       | timestamp  | Start time |
| frequency      | number     | every number of days |
| duration       | number     | Duration in minutes |
| lastDate       | timestamp  | Last date of the class |
| allClassScreenLocked | boolean    | All students Screen locked? |
| allClassEmailNotFocus | boolean    | All students email parent when leave full-screen? |
| allClassSendReport | boolean    | All students send lesson report? |
| allClassSaveMaterials | boolean    | All students save materials into student Google Drive Folder? |
| teacherDrive   | string      | Google Drive Folder URL to store materials, classwork, and homework |
| majorCountry        | string   | country in the majority |
| majorCity           | string   | province or city in the majority |
| majorLanguage       | string   | language in the majority |
| sendFeeReminder    | boolean    | Send Tuition Fee reminder Email to parents? |
| sendLessonReminder  | boolean    | Send Next Day Lesson reminder Email to students? |
| sendHomeworkReminder  | boolean  | Send Next Day Homework Deadline reminder Email to students? |

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
| subic              | string   | e.g., "quadratic factoring", "Differentiation Optimization" |
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

## 💳 Subscriptions Collection (`subscriptions`) (Object stored in Teacher's schema)

| Field       | Type      | Description |
|------------|-----------|-------------|
| id         | string    | Subscription ID |
| userId     | string    | Linked user ID |
| provider   | string    | One from the Array of {'stripe' or 'paypal'} |
| planType   | string    | SubscriptionPlan ID {'Free', 'Standard', 'Premium', 'Enterprise'} (Will add new types here in the future) |
| AddOn      | string    | One from the Array of {'Screen Lock', 'AI Feedback', 'Auto Save'} (Will add new add on in the future) |
| frequencyIndex  | number    | get frequency from array in Plans frequencies {1, 12} monthly: 1, annually: 12 (We may have quarterly: 3, semi-annually: 6 in the future) |
| amountIndex     | number    | get amount from array in Plans amounts, billing amount in US$ each time |
| currency   | string    | One from the Array of {US$, CAD$, UK$, EURO$, YUAN$, HK$, YEN$, AUST$} |
| promotionCode | string | Promtion code used this time |
| previousPlanType     | array    | List of all previous Plan types |
| createdAt  | timestamp | Start time |
| lastDate   | timestamp | Last valid date of this payment | 
| timeLimits | array | { int meeting minutes limit (get with SubscriptionPlan ID), int 1st add on minutes limi(get with SubscriptionPlan ID), int 1st add on minutes limit(get with SubscriptionPlan ID)} of a month (will add new add on in the future) |

---

## Subscription Plans Collection (`subscription-plans`)
| Field       | Type      | Description |
|------------|-----------|-------------|
| id         | string    | SubscriptionPlan ID |
| planType   | string    | One from the Array of {'Free', 'Standard', 'Premium', 'Enterprise'} (Will add new types here in the future) |
| frequencies  | array  | allowed frequencies: Array of {1, 12} monthly: 1, annually: 12 (We may have quarterly: 3, semi-annually: 6 in the future) |
| ammounts   | array    | amounts of each frequency eg. {19.9, 199.9} |
| timeLimit  | number   | number of minutes of classroom meeting allowed per month |
| addOnLimits | array   | { 1st add on limit, 2nd add on limit, 3rd add on limit} in minutes (will add new add on in the future) |


--

## Add Ons Collection (`add-ons`)
| Field       | Type      | Description |
|------------|-----------|-------------|
| id         | string    | Add On ID |
| Name       | string    | eg. 'Students' Screen Lock feature' |
| amounts    | array     | prices of each frequency |

--

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

