# Time Tracker

A multi-user productivity and time management application built with Streamlit and MongoDB. Combines a Pomodoro-style focus timer with goal planning, weekly scheduling, session analytics, journaling, and a dedicated focus mode — all persisted to a MongoDB backend.

## Features

### Timer & Sessions
- Configurable 25-minute work intervals with 5-minute break cycles
- Session logging with user, category, task, start time, duration, and IST timezone metadata
- Sound alerts on session completion (configurable per user)

### Planning & Goals
- Weekly planner for creating and tracking goals across categories
- Backlog queue with `current` / `backlog` priority buckets
- Persistent plan repository with status tracking across sessions

### Analytics
- Aggregate daily and overall time spent per category and task
- Streak tracking: consecutive active days computed from session history
- Bar charts and summary tables via pandas and matplotlib

### Journaling
- Date-indexed daily notes with save and retrieval
- Notes viewer with date-range filtering

### Multi-User Support
- User profiles created and persisted in MongoDB
- All session and note data scoped by `user_id`
- User management utilities for account maintenance and deduplication

## Tech Stack

| Component | Technology |
|---|---|
| App Framework | Streamlit |
| Database | MongoDB (pymongo) |
| Data Processing | pandas, numpy |
| Visualisation | matplotlib |
| Timezone Handling | pytz (Asia/Kolkata) |
| TLS / Connectivity | certifi |

## Project Structure

```
├── app.py                     # Main Streamlit application entry point
├── core/
│   ├── config.py              # Environment and configuration loading
│   ├── constants.py           # Category definitions and timer defaults
│   ├── db.py                  # MongoDB connection management
│   └── time_utils.py          # IST timezone conversion utilities
├── data_access/
│   ├── sessions_repo.py       # CRUD for timer session records
│   ├── users_repo.py          # User management queries
│   ├── goals_repo.py          # Goals persistence
│   └── plans_repo.py          # Weekly planner data access
├── services/
│   ├── sessions_service.py    # Session business logic
│   └── planner_service.py     # Goal and planning logic
├── ui/
│   ├── tabs/
│   │   ├── timer_tab.py       # Pomodoro timer UI
│   │   ├── analytics_tab.py   # Analytics and chart views
│   │   └── planner_tab.py     # Weekly planner UI
│   └── components/
│       └── sound.py           # Audio alert component
├── analytics.py               # Standalone analytics queries
├── focus.py                   # Focus mode interface
├── journal.py                 # Journal entry management
└── requirements.txt
```

## Prerequisites

- Python 3.9+
- MongoDB instance (local or Atlas)

## Setup

```bash
pip install -r requirements.txt
```

Configure the MongoDB connection in `.streamlit/secrets.toml`:

```toml
[mongo]
uri = "mongodb+srv://<user>:<password>@<cluster>.mongodb.net/"
db  = "time_tracker"
```

## Running the Application

```bash
streamlit run app.py
```

Opens at `http://localhost:8501`.

## Session Categories

Sessions are tagged to one of the following built-in categories:

`Learning`, `Projects`, `Certification`, `Career`, `Health`, `Wellbeing`, `Start-up`, `Other`

Custom categories can be added through the UI and are persisted per user.

## Database Collections

| Collection | Description |
|---|---|
| `users` | User profiles and metadata |
| `sessions` | Completed Pomodoro session records |
| `goals` | Active and completed user goals |
| `plans` | Weekly plan entries |
| `journal` | Daily journal entries |

## License

MIT
