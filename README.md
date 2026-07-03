# stackmap

## Local Setup

### Prerequisites

- Python 3.11+
- pip

### 1. Create and activate the virtual environment

```bash

- Use Python 3 to create a local isolated Python environment in a folder called .venv
python -m venv .venv

- turns that virtual environment on for your current terminal session.
source .venv/bin/activate
```

### 2. Install dependencies

```bash
pip install -r backend/requirements.txt
```

### 3. Run the Django development server

```bash
cd backend
python manage.py migrate
python manage.py runserver
```

The API will be available at `http://127.0.0.1:8000/`.
