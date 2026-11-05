# FUNNOW hotel weekly report

A demo built for the FUNNOW Group AI Management Trainee assignment, using the mock data supplied with it.

Every Monday at 09:00, the system reads last week's hotel data from a Google Sheet, labels each hotel with fixed rules, has an AI model word a short summary, checks the draft with code, and emails it. Needs-improvement results and failed drafts go to a reviewer first. It runs on the builder's own computer and sends test emails only to addresses the builder controls.

- [Test results](TEST_RESULTS.md)
- [Report workflow](workflow/send-weekly-hotel-summary.json)
- [Failure alert workflow](workflow/alert-when-report-fails.json)
- [Privacy policy](PRIVACY.md)

## Run it yourself

You need n8n 2.46.6, a Google account for Sheets and Gmail, and a Gemini API key.

1. Copy the mock sheet and add a `week_start` column. Each hotel needs last week's Monday in `YYYY-MM-DD` format. `target_revenue` is an optional column.
2. Import both workflow files into n8n.
3. In `Read Hotel Sheet`, replace `YOUR_SHEET_ID` with the ID of your copy.
4. In `Send to Reviewer` and `Email Failure Alert`, replace `reviewer@example.com` with your address.
5. Connect your Google Sheets, Gmail and Gemini credentials on each node that needs them.
6. Publish the alert workflow, then choose it as the error workflow in the report workflow's settings.
7. Publish the report workflow.

The owner emails in the mock sheet are `@example.com` addresses. Replace them with addresses you control before you run it, or the emails will be sent to those addresses.
