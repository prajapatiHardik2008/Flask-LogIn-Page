# Configuration

`.env` is loaded by `python-dotenv`. `SECRET_KEY` signs sessions and reset tokens. `DATABASE_URL` selects SQLite or PostgreSQL. `SESSION_COOKIE_SECURE` should be true when the app is served over HTTPS.

Configuration classes separate development, testing, and production defaults. Keep credentials out of Git, rotate compromised secrets, and use your deployment platform's secret manager. A secret in a client-side file is not secret.
