# n8n - Customer Retention Workflow

## Overview
Two-workflow automated customer health monitoring system
built entirely in n8n with Google Sheets as the data source.
Originally planned with Tasklet - rebuilt in n8n after
Tasklet was discontinued by Gayiti due to credit limitations.

## Workflow 1 - Daily Risk Monitor
**Schedule: Every day at 8:00 AM**

### Data Flow
1. Schedule Trigger fires at 8AM
2. Google Sheets node reads all customer records
3. Split in Batches processes one customer at a time
4. IF Node 1 - Days Since Login >= 30 (No Login Risk)
5. IF Node 2 - NPS Score <= 6 (Low NPS Risk)
6. IF Node 3 - Days Until Renewal <= 60 (Renewal Risk)
7. IF Node 4 - Support Escalated = YES (Support Risk)
8. Set node builds contextualized alert message
9. Slack node sends alert to #referrals channel
10. Google Sheets updates Risk Status, Last Alert Sent,
    and Alert Count for the flagged customer

### Risk Signals Monitored
- No login in 30+ days
- NPS score below 7
- Renewal within 60 days
- Active support escalation

## Workflow 2 - 48h Escalation
**Schedule: Every day at 9:00 AM**

### Data Flow
1. Schedule Trigger fires at 9AM
2. Google Sheets reads customers where Alert Count >= 1
3. Split in Batches processes one by one
4. IF node checks if Last Alert Sent was 48+ hours ago
5. Slack sends escalation notice to #referrals
6. Google Sheets updates Risk Status to Manager Review

## Edge Case Handled
Multi-signal customers - accounts triggering all 4 risk
signals simultaneously - are flagged as critical priority.
The Split in Batches pattern ensures every customer is
evaluated independently regardless of how many records
exist in the database.

## Google Sheets Structure
- Customer Name, Email, Last Login Date
- Days Since Login (formula), NPS Score
- Renewal Date, Days Until Renewal (formula)
- Support Escalated (YES/NO), Risk Status
- Account Manager, Last Alert Sent, Alert Count

## Files
- workflow-1-daily-risk-monitor.json
- workflow-2-48h-escalation.json
- screenshots/

## Tech Stack
n8n - Google Sheets - Slack

## Tech Stack
n8n - Google Sheets - Slack
