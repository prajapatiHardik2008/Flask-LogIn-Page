# Security notes

AuthKit is a teaching and reuse-oriented foundation, not a guarantee of complete security. Review it against your threat model before deploying.

## Included protections

- Passwords are processed with Flask-Bcrypt and only the resulting hash is stored.
- Flask-WTF adds a CSRF token to state-changing forms.
- Flask-Login manages the authenticated user and `@login_required` protects private views.
- Session and remember cookies are HTTP-only and SameSite=Lax by default. Enable Secure cookies over HTTPS in production.
- Reset tokens are signed, time-limited, sent through Brevo, and never shown in the HTTP response.

## Production checklist

- Set a long random `SECRET_KEY` and `BREVO_API_KEY` outside source control and use a managed PostgreSQL database.
- Set `SESSION_COOKIE_SECURE=true`, terminate TLS correctly, and configure trusted proxy behavior.
- Verify the Brevo sender/domain and monitor delivery. Never log reset URLs, tokens, passwords, API keys, or secrets.
- Add rate limiting, login lockout/alerting, email verification, MFA, security headers, backups, and monitoring appropriate to your application.
- Use a production WSGI server; do not use Flask's development server publicly.
- Keep dependencies patched and run tests in CI.

## Reporting vulnerabilities

Do not disclose a suspected vulnerability in a public issue. Contact the repository owner privately with reproduction steps, impact, and a safe contact method. Allow reasonable time for a fix before public disclosure.
