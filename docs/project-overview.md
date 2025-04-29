Tutoring Platform: Project Overview

🎯 Purpose

To build a professional online tutoring platform tailored for teachers and tutors that offers:

video-based live teaching with parental controls

Per-student whiteboards using Excalidraw

AI-powered feedback on student classwork

A full teaching workflow for managing meetings, students, homework, and analytics

🧩 Core Components

1. Video Meetings

created by ourselves (teacher-student sessions)

Lock screen control (fullscreen enforced, focus detection)

Parent email alerts when student leaves tab

Teacher control panel for locking/unlocking each student screen

2. Whiteboard System

Based on Excalidraw API (1 whiteboard per student)

Teacher can paste content to all boards (via screen crop)

All whiteboards visible to teacher

Navigation controls for switching boards

'Back to Lecture' button refocuses all students

3. AI Classwork Feedback

AI gives hints if student is idle for 8s

AI gives step-by-step feedback (correctness, advice)

Teacher can toggle AI assistance per student

AI can give extended/follow-up questions

4. Student Analytics and Reports

Track trial count, time spent, skills per question

Auto-generate post-session reports for teachers

Allow teachers to edit & finalize reports

Send reports to parents

5. Document and Storage System

Questions stored in Firebase with editable metadata

Screenshots of student work and teacher board

All teaching materials + whiteboards stored in Google Drive (teacher + student accounts)

6. Reminders and Email Notifications

Reminder emails for tuition and meeting attendance

Absence submission links for students/parents

7. Payments & Subscriptions

Tutor/teacher subscriptions handled via PayPal & Stripe

Student tuition reminders triggered monthly

🛠️ Tech Stack

Frontend & Backend: Next.js (React + API Routes)

Database: Firebase (Firestore, Storage)

Authentication: Firebase Auth

Video: Created by ourselves

Whiteboard: Excalidraw

Payments: PayPal + Stripe

AI Features: OpenAI (option to switch to cheaper math APIs if needed)

⚠️ Device & Platform Support

Chrome browser only

iPad and Laptop (no phones)

PWA enabled to hide browser UI (like nav bar, home button)

✅ Current Status

Repo created: tutoring-platform

Planning documents now tracked in /docs

GitHub + Google Drive will hold all documents moving forward
