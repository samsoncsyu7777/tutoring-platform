Authentication & Roles
This document outlines how authentication is handled across the tutoring platform and the role-based access system that governs user permissions.

🔐 Authentication
Method: Google OAuth 2.0

Library: Firebase Authentication

Flow:

User logs in using Google.

Firebase validates identity and returns a secure token.

On first login, user is prompted to choose or confirm a role.

👥 User Roles

Role	Description
admin	Platform manager with full access to users, settings, analytics
teacher	Can create classes, invite students, access dashboards, assign work
student	Attends live classes, views assignments, interacts with whiteboard
parent	Receives reports, monitors student progress, sets notifications
⚙️ Role-Based Access Control (RBAC)
Access to pages and features is determined by role.

Sensitive actions (e.g., viewing student progress, exporting reports) are restricted.

Each route or API endpoint will check for proper user role before serving data.

🧪 Future Plans
Support for school-wide or organization-wide admin roles

Custom permissions for group tutors (e.g., multiple teachers per class)

Optional 2FA for admins and teachers
