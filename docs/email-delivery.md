# Email delivery with Brevo

AuthKit uses Brevo transactional email for password-reset messages. Brevo is an external email delivery service: AuthKit creates a short-lived signed link, and Brevo delivers a styled email containing that link.

## Setup

1. Create a Brevo account and generate an API key.
2. Verify the sender address or domain in Brevo.
3. Put the API key and verified sender in `.env`:

```text
BREVO_API_KEY=your-brevo-api-key
MAIL_FROM_EMAIL=noreply@your-domain.example
MAIL_FROM_NAME=Flask AuthKit
```

4. Install dependencies with `pip install -r requirements.txt`.
5. Submit the forgot-password form and check the recipient inbox.

`app/services/email.py` contains the integration. `send_password_reset_email()` creates a `SendSmtpEmail` object and calls Brevo's `TransactionalEmailsApi`. The route never displays the reset URL or logs the token.

## Important details

The application deliberately shows the same message whether or not an email exists. This prevents account enumeration. The email link expires after `PASSWORD_RESET_MAX_AGE` seconds, which defaults to one hour.

Do not put the Brevo API key in Python code, HTML, JavaScript, or Git. Use environment variables or your deployment platform's secret manager. In production, configure a verified domain and monitor delivery failures.
