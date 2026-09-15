### Project 2 - n8n: Customer Retention Workflow

Built a two-workflow automated customer health monitoring
system entirely in n8n. Originally planned with Tasklet,
rebuilt in n8n after Tasklet was discontinued by Gayiti
due to credit limitations.

**Workflow 1 - Daily Risk Monitor (runs at 8AM)**
- Reads all customers from Google Sheets
- Processes each customer through 4 risk signal checks:
  no login in 30+ days, NPS below 7, renewal within
  60 days, support escalation active
- Sends contextualized Slack alert for each at-risk account
- Updates customer Risk Status and Alert timestamp
  in Google Sheets

**Workflow 2 - 48h Escalation (runs at 9AM)**
- Reads customers flagged in the last 48 hours
- Checks if any alert went unactioned
- Escalates to manager review via Slack
- Updates Risk Status to Manager Review in Google Sheets

**Tech stack:** n8n - Google Sheets - Slack
