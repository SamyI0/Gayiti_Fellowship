# n8n - Referral Partner Program

## Trigger
A POST webhook receives referral data containing
partner_code, prospect details, and intent. Fires
automatically when a partner submits a referral
through any integrated form or system.

## Data Flow
1. Webhook receives POST request with referral payload
2. First IF node validates required fields are present
3. Second IF node validates partner_code against
   known partner list
4. Valid referrals persisted to Google Sheets with
   full attribution tracking
5. Sales team receives instant Slack notification
   with lead context
6. Two emails dispatch automatically - one confirming
   the referral to the partner, one welcoming
   the prospect

## Edge Case Handled
Unknown or invalid partner codes are rejected
immediately with a clear 400 error message before
any data is saved or any notification is sent.
Missing required fields trigger a separate validation
error at entry point, preventing incomplete records
from entering the system.

## Tech Stack
n8n - Webhook - Google Sheets - Slack - Gmail
