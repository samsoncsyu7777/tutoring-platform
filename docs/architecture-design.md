# Architecture Design

## 🔧 Technology Stack

| Component            | Technology              |
|---------------------|--------------------------|
| Frontend            | Next.js (React-based)    |
| Backend             | Next.js API Routes + Node.js server |
| Real-Time Meeting   | WebRTC + Socket.IO       |
| Signaling Server    | Node.js on DigitalOcean VPS |
| Authentication      | Firebase Auth            |
| Database            | Firebase Firestore       |
| File Storage        | Firebase Storage + Google Drive integration |
| Payments            | Stripe + PayPal          |
| AI Hints & Feedback | OpenAI API (ChatGPT 3.5 or 4) |
| Whiteboard          | Excalidraw (embedded)    |

---

## 🖼️ System Diagram

[Student Browser] ←→ WebRTC ←→ [Teacher Browser] ↑ ↑ | | └───> Socket.IO Signaling ────────┘ (DigitalOcean VPS)

          ↓           ↓
  [Firebase DB]   [Firebase Storage]
          ↓           ↓
     [AI API (OpenAI)] 
          ↓
    [Google Drive Sync]
          ↓
   [Stripe / PayPal APIs]




---

## 📡 Core Services

### 1. **WebRTC + Signaling Server**
- Peer-to-peer video/audio connection (no Zoom cost).
- A small Node.js server on DigitalOcean handles signaling (e.g., offer/answer exchange).
- Uses Socket.IO for real-time communication.

### 2. **Next.js App**
- Single platform for both frontend and backend logic.
- Uses server-side functions (`pages/api/*`) for email, reminders, and logic.

### 3. **Firebase**
- Firestore stores: users, meetings, classwork, attendance, reports.
- Firebase Auth for user login (with roles: teacher, student, parent).
- Firebase Storage for uploaded teaching files and screenshots.

### 4. **AI Helper**
- OpenAI API (GPT-3.5 or GPT-4).
- Used to give hints, corrections, and feedback on whiteboards.
- Controlled by teacher per student (turn on/off).

### 5. **Google Drive Sync**
- Every student and teacher links their Google Drive.
- All teaching materials and classwork are saved both centrally and on personal drives.

### 6. **Payments**
- Stripe and PayPal support for tutor subscriptions.
- Can support both monthly billing and one-time sessions.

---

## 🔒 Lock Screen + Focus Detection

- App forces fullscreen when student joins.
- If tab loses focus → app detects and notifies parent (if enabled).
- Teacher can lock/unlock focus & alerts per student.

---

## 📦 Hosting Plan

| Service | Host | Notes |
|--------|------|-------|
| Next.js App | Vercel or Firebase Hosting | Easy CI/CD |
| Node.js Signaling Server | DigitalOcean VPS | $5/month plan |
| Firebase (Auth, Firestore, Storage) | Firebase | Scalable and easy |
| Google Drive | Native Google API | User grants permission |
| Stripe/PayPal | Cloud-based APIs | No server required |

---

## 📌 Notes

- All logic is centralized in one Next.js codebase.
- Video calls are free (WebRTC) and customizable.
- Firebase keeps the stack simple for now — can scale to Firestore triggers or functions later.

