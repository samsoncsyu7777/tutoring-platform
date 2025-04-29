Google Drive Integration
This document outlines how the tutoring platform integrates with Google Drive to store session-related files for students and teachers efficiently and securely.

📂 Why Google Drive?
Cloud storage costs (e.g., Firebase, AWS) can escalate quickly, especially with screenshots.

Google Drive offers:

Generous free tier per user

Familiar interface

Easy sharing and folder structure

Direct integration with Google APIs

🧑 Folder Structure: Students
Each student has a dedicated Google Drive folder automatically organized by session.
Format: (Date - Topic)
Within each session folder:

Teaching Materials screenshots

Your Classwork screenshots

Homework screenshots - [Due Date]

Learning Report (PDF or HTML snapshot)

👨‍🏫 Folder Structure: Teachers
Teachers have a higher-level folder that collects session folders for each student.
Each folder contains:

Teaching Materials screenshots

All Students Classwork screenshots

Homework screenshots - [Due Date]

All Students Learning Reports

🔐 Permissions & Privacy
Students and teachers grant access via Google OAuth.

The platform uses Drive API to:

Create folders

Upload screenshots

Write reports

Reports are not stored in our database. They live in Google Drive for privacy and cost efficiency.

🔄 Sync & Backup
A local copy of file references (URLs and timestamps) is kept in the Firestore users collection.

No screenshot binary data is saved in Firebase.
