# Payment simulator demonstration

[MP4 walkthrough](media/walkthrough.mp4) · [Animated preview](media/walkthrough.gif)

Captured **17 November 2026** from commit `450d5f7`, using Python 3.12.14 and
Django 6.0.10. The video is a 24-second sequence of actual UI screenshots with
captions. All funds and account details are fictional.

## Journey and observed results

1. [Dashboard](media/01-dashboard.jpg): `alex_demo` starts with GBP 1000.00.
2. [Send payment](media/02-send-payment.jpg): transfer GBP 50.00 to `sam_demo`.
3. [Confirmation](media/03-payment-confirmed.jpg): the transfer appears in history.
4. [Notifications](media/04-pending-request.jpg): review a seeded GBP 25.00 request.
5. [Accepted request](media/05-request-accepted.jpg): accepting it creates the second
   transfer and records the request as Accepted.
6. [Updated balance](media/06-updated-balance.jpg): GBP 925.00 remains.

The recipient is a USD account; normal application logic called the actual local
conversion endpoint. No external payment provider or real money was involved.
The two users and initial pending request were seeded in a fresh local database.
Sign-in, direct transfer and request acceptance were exercised through the UI.

## Reproduce

Follow the README setup and keep the threaded development server running. Register
two fictional users, send 50 GBP between them, then use the second user to request
25 GBP from the first. Sign back into the first user, accept the request from
Notifications and inspect Transactions and the dashboard balance.

For a port other than 8000, set `INTERNAL_API_BASE` to the actual loopback origin.
This capture used port 8802. Runtime databases and credentials are not included.

## Verification

`python manage.py test --noinput`: **16 tests passed**. Django's system check
reported no issues. The browser journey also confirmed the accepted request and
the expected post-transfer balance. This is demonstration evidence for the local
simulator; the deployment limitations in the README still apply.
