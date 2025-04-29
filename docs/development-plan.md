# Development Plan

This document outlines the phased development roadmap for the tutoring platform, from MVP to full-feature release.

---

## Phase 1: Foundation (Weeks 1–3)

- ✅ Set up GitHub repository and documentation structure
- ✅ Choose core technologies: Next.js, Firebase, Excalidraw, Zoom (temporary), Stripe, PayPal
- ✅ Establish base project structure (monorepo or modular layout)
- ✅ Set up authentication (Google OAuth)
- ✅ Build landing page with pricing and subscription options
- ✅ Configure database schema in Firebase
- ✅ Set up Stripe and PayPal integration (basic payment flow)
- ✅ Implement role-based access system (admin/teacher/student/parent)

---

## Phase 2: Core Platform (Weeks 4–7)

- 🧑‍🏫 Build teacher dashboard: class creation, student management
- 🧑‍🎓 Build student dashboard: class list, whiteboard access
- 🧠 Integrate Excalidraw with custom whiteboards per student
- 🔄 Add real-time syncing using Firebase or WebSockets
- 🎥 Develop custom video meeting system (WebRTC-based), using MediaSoup or Jitsi – no Zoom integration
- 📦 Setup PWA behavior and fullscreen enforcement
- 📩 Implement email notification system (attendance, alerts, reminders)

---

## Phase 3: Classwork & AI (Weeks 8–11)

- ✍️ Build question creation module for teachers
- 📊 Track student attempts, time, and success rate per key skill
- 🧠 Add AI support (ChatGPT 3.5) for hints, feedback, and follow-up questions
- 🔒 Implement screen lock and focus detection + parental alerts
- 🖼️ Add ability to crop & paste screen snippets into whiteboards

---

## Phase 4: Post-Class Tools & Analytics (Weeks 12–14)

- 📋 Session report generation for teachers
- 📬 Email reports to parents
- 📁 Google Drive integration for storing classwork
- 📊 Usage analytics dashboard for admins
- 💬 Feedback system for teachers to edit and annotate reports

---

## Phase 5: Polish & Launch (Weeks 15–16)

- 🧪 Testing and bug fixes (cross-device, PWA, security, load)
- 🚀 Deploy to DigitalOcean with CI/CD
- 🌐 Finalize domain, SEO, and social media integration
- 📖 Write user guides and onboarding material
- 💼 Prepare promotional materials for tutors and parents

---

## Ongoing / Optional

- // No more Zoom integration in our development🎥 Replace Zoom with self-hosted video (e.g. MediaSoup, Jitsi)
- 🧠 Upgrade AI model or add math-specific AI APIs
- 🌍 Support for multiple languages and time zones
- 📱 Develop dedicated mobile version (if later desired)

