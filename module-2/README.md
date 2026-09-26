# Module 2 - Workflow Automation & APIs

## Overview
Extend the Module 1 pipeline with a live external API
integration and proper error handling. The workflow
must connect to at least one live external service and
gracefully recover from a known failure mode.

## Project
- [n8n - Referral Partner Program v2](./n8n-referral-partner-program-v2/)

## What was added on top of M1
- Live API call to Hunter.io for email verification
- Error branch catching API timeout, bad response,
  and invalid key
- Failure logged to Google Sheets API Error Log
- Slack alert on failure
- Enriched Slack notification with email quality data

## Tech Stack
n8n - Webhook - Hunter.io API - Google Sheets - Slack - Gmail
