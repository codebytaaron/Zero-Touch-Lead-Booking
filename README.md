# AI-Powered Lead Generation, Qualification, and Auto-Scheduling

An automation workflow that captures leads, stores their info, uses AI to qualify them, and auto-schedules high-intent prospects by pulling open calendar slots and emailing an offer to book.

## Workflow (What happens)
1. **Lead Generation Form**  
   A lead submits their info (name, email, company, message, etc.).

2. **Workflow Configuration (manual)**  
   Your rules + settings live here (score threshold, calendar to use, email template).

3. **Store Lead Data**  
   Saves the lead in a table/database for tracking and follow-up.

4. **AI Lead Qualifier (OpenAI + schema)**  
   The AI reviews the lead details and returns structured output (score, intent, fit notes).

5. **Route High-Score Leads**  
   Only leads above your threshold continue to scheduling.

6. **Get Available Slots (Google Calendar)**  
   Pulls upcoming availability / open times.

7. **Send Offer Email (Gmail)**  
   Sends the lead a scheduling offer with available options (or a booking link).

## Features
- AI-based **lead scoring + qualification**
- **Structured output** using a qualification schema
- Automatic **routing** based on score/intent
- Calendar integration to **fetch availability**
- Email automation to **send meeting offers**
- Lead storage for reporting and audit trail

## Requirements
- OpenAI API key
- Google Calendar access (OAuth/service account depending on your setup)
- Gmail access (OAuth or SMTP depending on your setup)
- A database/table for lead storage (optional but recommended)

## Environment Variables
Create a `.env` file (or set these in your automation platform):

- `OPENAI_API_KEY`
- `QUALIFICATION_MODEL` (example: `gpt-4.1-mini` or your chosen model)
- `LEAD_SCORE_THRESHOLD` (example: `75`)
- `GOOGLE_CALENDAR_ID`
- `GMAIL_FROM_EMAIL`
- `TIMEZONE` (example: `America/New_York`)

Optional:
- `BOOKING_LINK` (if you prefer sending a link instead of slot options)
- `DB_CONNECTION_STRING` (if using an external database)

## Qualification Output (Example Schema)
Your AI step should return something like:

```json
{
  "score": 0,
  "isQualified": false,
  "intent": "low|medium|high",
  "reason": "short explanation",
  "recommendedNextStep": "email_followup|schedule_offer|disqualify",
  "notes": "any extra context"
}
