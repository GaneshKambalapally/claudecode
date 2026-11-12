# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

"Spendly" — a Flask expense tracker built as a step-by-step tutorial scaffold. Much of it is intentionally unimplemented; placeholder routes and files name the tutorial step that fills them in.

## Commands

```powershell
python -m venv venv; venv\Scripts\activate   # venv/ is gitignored
pip install -r requirements.txt              # Flask, Werkzeug, pytest, pytest-flask
python app.py                                # dev server, debug mode, http://localhost:5001
pytest                                       # no tests exist yet (no tests/ dir)
pytest path/to/test_file.py::test_name       # run a single test
```

No linter or build step is configured.

## Architecture

- `app.py` is the single Flask module holding all routes. The landing, register, login and terms routes only render templates. The remaining routes (`/logout`, `/profile`, `/expenses/add`, `/expenses/<id>/edit`, `/expenses/<id>/delete`) are stubs returning "coming in Step N" strings. Replace them as the steps are implemented.
- `database/db.py` is comments only. It specifies the intended SQLite layer: `get_db()` (connection with `row_factory` and foreign keys enabled), `init_db()` (`CREATE TABLE IF NOT EXISTS`), and `seed_db()` (dev sample data). Nothing imports it yet. The SQLite file is `expense_tracker.db` (gitignored).
- `templates/` all extend `base.html`, which defines the `title` and `head` blocks and loads Google Fonts plus `static/css/style.css`. Page-specific CSS (e.g. `landing.css`) goes in the `head` block. Templates link with `url_for('<endpoint>')`, so renaming a view function breaks nav links.
- Register and login are static forms with no POST handling, sessions or auth yet.
