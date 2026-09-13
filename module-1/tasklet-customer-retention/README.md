# Tasklet — Customer Retention Workflow

## Overview
AI-powered customer health monitoring system that
proactively surfaces at-risk accounts before they
churn. Connected to Notion customer database.

## Risk Triggers
- Days Since Login > 30 = NO LOGIN RISK
- NPS Score < 7 = LOW NPS RISK
- Days Until Renewal < 60 = RENEWAL RISK
- Support Escalated = true = SUPPORT RISK

## Automations
1. Daily Risk Scan — 8AM every day
2. Low NPS Alert — immediate trigger
3. Renewal Warning — every Monday 9AM
4. Support Escalation — immediate trigger
5. 48h Escalation — unactioned alerts escalate
   to manager automatically

## Data Flow
Notion database → Tasklet reads daily → detects
risk signals → creates contextualized alert →
Slack notification → 48h escalation if no action

## Edge Case Handled
Multi-signal customers trigger critical priority
flag — accounts with all 4 risk signals active
simultaneously surface first in the alert queue.

## Files
- screenshots/ — automations and Slack alerts

## Tech Stack
Tasklet · Notion · Slack · Gmail
