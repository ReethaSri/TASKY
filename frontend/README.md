# Tasky

A task assigner website: assign tasks by name, submit them, track deadlines on a calendar, and get reminders.
Python backend (standard library only) + plain HTML/CSS/JavaScript frontend.

## Features
- Sign up with name, email, phone and age; sign in with email, phone or name; optional password
- "Remember me" with saved accounts; signing up again with the same email signs you in
- Profile: edit login details, profile picture, password
- Linked devices: list, unlink, and add a device with a 10-minute code
- Home dashboard, assign task, pending, completed (by month), deadlines, calendar
- Task submission with a note; reminders as pop-ups, a bell and browser notifications

## Project structure
```
tasky/
├── app.py              backend: REST API + static file server
├── requirements.txt    dependencies (none)
├── static/
│   ├── index.html      page layout
│   ├── style.css       theme and styling
│   └── app.js          pages, calendar, reminders, API calls
├── tests/test_api.py   API smoke tests
├── demo/tasky-demo.html  standalone demo (data kept in the browser, no server)
├── .gitignore
└── README.md
```

## Run
Requires Python 3.8+.
```
python app.py
```
Open http://localhost:8080. Data is stored in `tasky.db` (SQLite), created on first run.

| Setting | Default | Purpose |
|---|---|---|
| `PORT` | 8080 | Server port |
| `TASKY_DB` | `./tasky.db` | Database file path |

## Test
```
python -m unittest discover tests
```

## API
All endpoints except `/api/login` need the `X-User` and `X-Device` headers (set by the frontend).

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/api/login` | `mode`: `in`, `up`, `code`, `resume` |
| PUT | `/api/me` | Update profile and picture |
| PUT | `/api/password` | Set, change or remove password |
| GET | `/api/devices` | List linked devices |
| POST | `/api/devices/code` | Create a 6-digit link code |
| DELETE | `/api/devices/<id>` | Unlink a device |
| GET | `/api/users` | Known names |
| GET / POST | `/api/tasks` | List / assign tasks |
| POST | `/api/tasks/<id>/submit` | Submit a task |
| DELETE | `/api/tasks/<id>` | Delete a task you assigned |

## Notes
- Accounts without a password can be signed in to by anyone who knows the email, phone or name. Set a password for any account that matters.
- Reminders only appear while a Tasky tab is open.
