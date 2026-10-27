# PerplexMath — Tutor Session Form and Field Mapping

## Purpose
After each tutoring session, the tutor completes a Google Form to document what was covered and how the student responded. Google Forms automatically appends each submission to a linked Google Sheet. n8n monitors the sheet for new rows and attempts to create a linked session record in Supabase.

## Google Sheets columns and database mapping

| Google Sheets response column | Purpose | Supabase destination |
| --- | --- | --- |
| `Timestamp` | Time the form was submitted | Not currently stored in `sessions` |
| `Student` | Student dropdown, e.g. `STU001 - Test Student A` | Student code extracted to look up `students.student_code`; matching `students.id` becomes `sessions.student_id` |
| `Tutor` | Tutor completing the report | Not currently stored in `sessions` |
| `Session date` | Date of the tutoring session | `sessions.date` |
| `What did the session focus on?` | Session focus (e.g. workbook or test preparation) | `sessions.session_type` |
| `Topics covered` | Material discussed | `sessions.topics_covered` |
| `Student understanding` | Tutor-rated understanding, such as `1 - Struggling` | Numeric prefix becomes `sessions.understanding_rating` |
| `Level of assistance needed` | How much help the student needed | `sessions.assistance_needed` |
| `Tutor observations` | Free-text session notes | `sessions.tutor_notes` |

## Workflow
1. A tutor submits the Google Form.
2. Google Sheets receives a new response row.
3. The n8n Google Sheets Trigger detects the new row.
4. The Supabase lookup node extracts the student code from the `Student` field and searches `students`.
5. When a student is found, the next node inserts the session in `sessions` using the student's internal ID.

## Current limitations
- The student dropdown must contain a code matching an existing `students.student_code` record.
- The student-code extraction currently expects the format `STU001 - Student Name`.
- A recent automatic execution did not find a matching student and did not insert a session; the full automated path still needs debugging.
- The current workflow does not save the tutor field or form submission timestamp to the session record.
- Add missing-student handling, input validation, and duplicate prevention before production use.

## Privacy
Use fictional student names and codes in public documentation and demonstrations. Do not commit actual student information, spreadsheet response exports, API keys, or OAuth credentials to GitHub.
