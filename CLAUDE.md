# Spendly — Expense Tracker

## Project Overview

**Spendly** is a personal expense tracking web app where users register, log expenses by category, and review spending breakdowns. Currency is Indian Rupees (₹). The project is structured as a student learning exercise with incremental implementation steps — placeholder routes exist for features not yet built.

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python 3, Flask 3.1 |
| Database | SQLite (via `database/db.py`) |
| Templates | Jinja2 (server-rendered HTML) |
| Auth | Werkzeug (password hashing) |
| Frontend | Vanilla CSS + JS, no framework |
| Fonts | DM Sans (body), DM Serif Display (headings) |
| Testing | pytest + pytest-flask |

## Project Structure

```
expense-tracker/
├── app.py                  # Flask app — all routes defined here
├── database/
│   ├── __init__.py
│   └── db.py               # get_db(), init_db(), seed_db() — to be implemented
├── templates/
│   ├── base.html           # Shared layout: navbar, footer, font/CSS links
│   ├── landing.html        # Public marketing homepage
│   ├── login.html          # Auth form
│   └── register.html       # Auth form
├── static/
│   ├── css/style.css       # All styles — CSS custom properties, no framework
│   └── js/main.js          # Client-side JS (currently empty)
└── requirements.txt
```

## How to Run

```bash
# Create and activate virtual environment
python3 -m venv venv
source venv/bin/activate      # macOS/Linux
# venv\Scripts\activate       # Windows

# Install dependencies
pip install -r requirements.txt

# Run the app
python app.py
# → http://localhost:5001
```

## Implemented vs Placeholder Routes

| Route | Status |
|---|---|
| `GET /` | Done — landing page |
| `GET /register` | Done — renders form |
| `GET /login` | Done — renders form |
| `GET /logout` | Placeholder (Step 3) |
| `GET /profile` | Placeholder (Step 4) |
| `GET /expenses/add` | Placeholder (Step 7) |
| `GET /expenses/<id>/edit` | Placeholder (Step 8) |
| `GET /expenses/<id>/delete` | Placeholder (Step 9) |

`POST` handlers for register, login, and expense forms are not yet wired up.

## Coding Conventions

### Python / Flask
- One file for all routes (`app.py`) — keep it that way until there's a reason to split
- Routes use `render_template()` for pages; return plain strings for stubs
- Route functions named with underscores: `add_expense`, `edit_expense`, etc.
- Run with `debug=True` on port `5001`
- Database helpers live in `database/db.py`: `get_db()`, `init_db()`, `seed_db()`

### Templates (Jinja2)
- All templates extend `base.html` via `{% extends "base.html" %}`
- Use `{% block title %}`, `{% block content %}`, `{% block head %}`, `{% block scripts %}`
- Use `url_for()` for all internal links — never hardcode paths (exception: form `action` attributes currently use hardcoded paths)
- Error messages passed via `{{ error }}` context variable, rendered in `.auth-error` div

### CSS
- All styles in a single `style.css` — no framework, no preprocessor
- CSS custom properties defined in `:root` — always use variables, never raw hex/px values
- Section blocks separated by `/* --- */` banners with consistent formatting
- BEM-lite naming: block (`auth-card`), element (`auth-title`), modifier (`mock-bar-2`)
- Responsive breakpoints: 900px (tablet), 600px (mobile)
- Design tokens: `--accent` (#1a472a dark green), `--accent-2` (#c17f24 amber), `--ink` (#0f0f0f)

### JavaScript
- Lives in `static/js/main.js` — add feature JS there as routes are built
- No frameworks — plain vanilla JS

### Testing
- Use pytest with pytest-flask
- Test files go alongside or in a `tests/` directory
