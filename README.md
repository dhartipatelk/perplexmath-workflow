# perplexmath-workflow
## PerplexMath — Tutor Session Automation
Project overview
PerplexMath is a prototype student-progress tracking workflow for a small virtual math tutoring business. It aims to help tutors document sessions consistently and help owners review student progress over time.
Business problem
The business uses diagnostic assessments and personalized workbooks, but tutoring-session observations are not consistently documented in one central location. This makes it difficult to review a student's session history and prepare regular progress updates.
Proposed solution
Tutors complete a brief Google Form after each session. Google Sheets collects responses, and an n8n workflow looks up the corresponding student in Supabase and inserts a session record. Later phases may include a Claude-powered student progress agent, human-reviewed parent updates, and Power BI dashboards.
### Workflow
Google Form → Google Sheets → n8n → Supabase

Planned: Supabase → Claude analysis and Power BI visualization.
### Technology
- Google Forms: tutor-facing session report
- Google Sheets: receives submissions
- n8n: automates student lookup and session insertion
- Supabase: stores linked student and session records
- Claude (planned): investigates trends and drafts summaries for tutor review
- Power BI (planned): visualizes progress
### Current progress
- Created a Google Form and linked Google Sheet.
- Created Supabase students and sessions tables.
- Built the n8n workflow with Google Sheets Trigger, student lookup, and session creation nodes.
- Successfully tested student lookup and session creation manually with fictional data.
- Known issue: a recent automatic execution could not match the selected student, so it did not insert a session. End-to-end automation still needs validation.
### Next steps
1. Fix and test student matching for new form submissions.
2. Handle missing students, duplicate submissions, and invalid values.
3. Preserve tutor identity in session records.
4. Develop AI analysis with human review.
5. Build progress dashboards.
6. Review security and privacy before using any real student data.
### Privacy and security
Use fictional student data for development and demonstrations. Do not commit student records, passwords, API keys, OAuth credentials, or other secrets. The repository may be publicly visible.
   ### Workflow import note:
        The sanitized JSON export omits saved credentials and replaces the original Google Sheet identifier. After importing into n8n, reconnect credentials and choose the         correct Google Sheet before testing.
