# PerplexMath Database Structure

PerplexMath uses Supabase (PostgreSQL) to connect students with tutoring session records.

## `students` table

| Column | Description |
| --- | --- |
| `id` | Auto-generated primary key |
| `student_code` | Unique student identifier used by the form, such as `STU001` |
| `student_name` | Student name |
| `grade_level` | Grade level |
| `course` | Math course |
| `current_unit` | Current unit of study |
| `assigned_tutor` | Tutor assigned to the student |

## `sessions` table

| Column | Description |
| --- | --- |
| `session_id` | Auto-generated primary key |
| `student_id` | Foreign key linking the session to `students.id` |
| `date` | Tutoring session date |
| `session_type` | Focus of the session |
| `topics_covered` | Topics covered during the session |
| `understanding_rating` | Tutor-reported understanding rating |
| `assistance_needed` | Amount of assistance required |
| `tutor_notes` | Tutor observations |

## Relationship

One student can have many session records.

`students.id` → `sessions.student_id`

## How n8n uses these tables

1. Google Sheets receives a new tutor form response.
2. n8n extracts the student code from the `Student` field (for example, `STU001 - Test Student A` → `STU001`).
3. n8n searches the `students` table for the matching `student_code`.
4. If a match is found, n8n inserts a new row into `sessions` using that student's internal `id`.

## Current limitation

The student lookup may return no result if the form's student code does not match a row in `students`. A recent automatic run stopped at this step. Missing-student handling and end-to-end validation are still needed.

## Privacy

Use fictional records for testing and demos. Do not publish real student data or Supabase credentials in GitHub.
