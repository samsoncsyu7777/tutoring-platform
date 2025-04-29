AI Integration
This document outlines how the platform integrates AI features to assist students and teachers in real-time and asynchronous learning.

🤖 AI Use Cases
1. Hint Generation
When students are stuck, AI can provide context-sensitive hints based on the question being solved.

Teachers can pre-approve or edit AI hints.

2. Answer Validation
Students receive instant feedback on whether their answers are correct or need revision.

AI can highlight common mistakes and suggest review topics.

3. Follow-Up Questions
Based on the student's performance, the AI generates follow-up questions to reinforce learning.

These questions are adapted from the original question template with varied difficulty.

4. Progress Feedback
AI provides summaries of student strengths and areas for improvement.

Teachers can include this AI-generated insight in reports to parents.

5. AI Report Drafting
The platform drafts learning reports after each session using:

Student attempts

Time spent

Types of mistakes

Teachers can review and edit before sending.

⚙️ Implementation Details
Model: OpenAI ChatGPT-3.5 (initially). May upgrade or integrate math-specific models later.

API Usage: Optimized to minimize token cost and improve speed.

Safety: AI outputs are filtered and reviewed for accuracy before being shown to students.

Customization: Teachers can define prompt templates or request AI silence in certain sessions.
