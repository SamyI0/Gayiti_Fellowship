# n8n - Referral Partner Program v2
# Live API Integration + Error Handling

## API Choice
Hunter.io Email Verifier API. When a referral arrives,
the prospect email is sent to Hunter.io for real-time
verification before the lead is saved or any
notification is sent. Hunter returns a deliverability
result, a confidence score from 0 to 100, and a flag
indicating whether the email is disposable. This
enriches every lead record with signal quality data
the sales team can act on immediately.

## What changed from M1
The workflow now inserts an HTTP Request node between
partner validation and Google Sheets persistence.
On success, the enriched payload flows forward with
three new fields: email_verified, email_score, and
email_disposable. The Slack notification and Google
Sheets row both carry this enrichment data.

## Failure Modes Tested
Two failure modes were tested. First, the API key was
disabled to simulate an authentication failure. The
error branch caught the empty response, logged the
failure to a dedicated API Error Log sheet with
timestamp and raw response, and sent a Slack alert
to the referrals channel. The lead continued through
the workflow without enrichment so no referral was
lost. Second, a malformed email payload was sent to
trigger a bad Hunter.io response. The same error
branch handled it identically.

## Recovery Behavior
The workflow never fails silently. Every API failure
surfaces in two places: the Google Sheets error log
and a Slack alert. The main referral pipeline
continues regardless of API status so no lead is
dropped due to third-party failure.
