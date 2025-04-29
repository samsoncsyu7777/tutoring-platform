Google Drive Structure
This document outlines how the tutoring platform integrates with Google Drive for storage and sharing of session-related materials, screenshots, and reports.

📁 Student Google Drive Folder Structure
Each student has a personal folder, organized by date and topic:

/Student_Name/
  └── [2025-04-29-Algebra-Graphing]/
        ├── Teaching Materials screenshots/
        ├── Your Classwork screenshots/
        ├── Homework screenshots - Due YYYY-MM-DD/
        └── Learning Report.pdf


Teaching Materials screenshots: Captures from the teacher’s shared screen.

Classwork screenshots: Student's work from the session.

Homework screenshots: Snapshots of assigned tasks.

Learning Report: Generated after each session, summarizing progress and focus.

📁 Teacher Google Drive Folder Structure
Each teacher has a folder with subfolders for each session topic:

/Teacher_Name/
  └── [2025-04-29-Algebra-Graphing]/
        ├── Teaching Materials screenshots/
        ├── All Students Classwork screenshots/
        ├── Homework screenshots - Due YYYY-MM-DD/
        └── All Students Learning Reports/

All Students Classwork screenshots: Organized by student name.

All Students Learning Reports: Individual PDFs, named by student.

🔗 Drive Integration Behavior
Google OAuth used to connect and authorize access to Drive.

On login, app checks if folders exist; creates them if missing.

Reports and screenshots are uploaded via Google Drive API.

Folder naming follows [YYYY-MM-DD]-[Topic] for easy organization.
