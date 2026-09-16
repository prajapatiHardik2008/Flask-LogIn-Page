# Flask AuthKit

Flask AuthKit is a reusable, production-oriented authentication foundation for Flask applications. It demonstrates account registration, secure password hashing, sessions, CSRF-protected forms, Brevo password-recovery email, and protected views without hiding the important decisions behind unnecessary abstractions.

## Features

- Email/username login, registration, logout, remember-me sessions
- Flask-Bcrypt password hashing and Flask-Login current-user handling
- Flask-WTF CSRF protection and WTForms validation
- SQLite default with a PostgreSQL-compatible SQLAlchemy URL
- Signed, expiring password-reset tokens delivered through Brevo
- Responsive accessible UI, password visibility control, and strength feedback
- Beginner-focused documentation and pytest coverage

## Stack

Python 3.10+, Flask, Flask-SQLAlchemy, Flask-Login, Flask-Bcrypt, Flask-WTF, WTForms, Brevo transactional email, Jinja2, SQLite/PostgreSQL, pytest.

## Quick start

```bash
git clone https://github.com/prajapatiHardik2008/Flask-LogIn-Page.git
cd Flask-LogIn-Page
python -m venv .venv
# macOS/Linux: source .venv/bin/activate
# Windows: .venv\\Scripts\\activate
pip install -r requirements.txt
cp .env.example .env
python run.py
```

Open http://127.0.0.1:5000. Set a strong `SECRET_KEY` and Brevo settings in `.env`; `DATABASE_URL` defaults to SQLite. Run `pytest` for tests.

## Email configuration

Create a Brevo API key, verify your sender, and set `BREVO_API_KEY`, `MAIL_FROM_EMAIL`, and `MAIL_FROM_NAME`. The forgot-password route sends reset instructions through Brevo. See [docs/email-delivery.md](docs/email-delivery.md).

## Architecture

`app/__init__.py` owns the application factory and extensions. `models.py` owns persistence. Blueprints separate authentication from application pages. Forms own input validation; `services/email.py` owns Brevo delivery; templates own presentation; static assets contain the small UI layer. See [docs/index.md](docs/index.md) for the learning path.

## Routes

| Route | Purpose | Access |
|---|---|---|
| `/` | Landing page | Public |
| `/register` | Create an account | Public |
| `/login` | Start a session | Public |
| `/logout` | End a session | Authenticated |
| `/profile` | Example protected page | Authenticated |
| `/forgot-password` | Request a Brevo reset email | Public |
| `/reset-password/<token>` | Set a new password | Token |

## Security highlights

Secrets come from environment variables, passwords are salted and hashed, CSRF is enabled, cookies use HTTP-only/SameSite settings, reset tokens expire, and login/recovery responses avoid identifying accounts. This starter does not claim to solve rate limiting, email verification, MFA, or every deployment concern. Read [SECURITY.md](SECURITY.md) before production use.

## Screenshots

Add deployment screenshots here when branding this starter for your application.

## Customization and contribution

Change templates and CSS without changing the auth flow; add fields through the model and forms; replace or extend the Brevo service for verification emails. Pull requests should include tests and keep security-sensitive changes documented.

## License

MIT. See [LICENSE](LICENSE).
