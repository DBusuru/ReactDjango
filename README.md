# React-Django App

This project is a **full-stack web application** using **React** as the frontend and **Django** as the backend.<br><br><br><br> The app fetches data from Django APIs and displays it in a modern UI built with Material-UI (MUI).


## Features

* React frontend with MUI components.
* Django REST API backend.
* Fetches and displays dynamic data from backend APIs.
* Responsive navigation bar and search UI.
* Ready for cross-origin requests (CORS enabled).

---

## Tech Stack

**Frontend:**

* React (Vite)
* Material-UI
* Axios / Fetch API

**Backend:**

* Python 3.11+
* Django 4.x
* Django REST Framework
* Django CORS Headers

---

## Getting Started

### Prerequisites

Make sure you have installed:

* Node.js (v18+)
* npm or yarn
* Python 3.11+
* pip
* virtualenv

---

### Backend Setup

1. Create and activate a virtual environment:

```bash
python -m venv venv
# Windows
venv\Scripts\activate
# macOS/Linux
source venv/bin/activate
```

2. Install dependencies:

```bash
pip install django djangorestframework django-cors-headers
```

3. Start a Django project:

```bash
django-admin startproject backend
cd backend
python manage.py startapp api
```

4. Configure `settings.py`:

```python
INSTALLED_APPS = [
    ...
    'rest_framework',
    'corsheaders',
    'api',
]

MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',
    ...
]

CORS_ALLOW_ALL_ORIGINS = True  # for development
```

5. Create a simple API endpoint in `api/views.py`:

```python
from django.http import JsonResponse

def hello(request):
    return JsonResponse({"message": "Hello from Django!"})
```

6. Add URL in `api/urls.py`:

```python
from django.urls import path
from .views import hello

urlpatterns = [
    path('hello/', hello),
]
```

Include it in `backend/urls.py`:

```python
from django.urls import path, include

urlpatterns = [
    path('api/', include('api.urls')),
]
```

7. Run the backend:

```bash
python manage.py runserver
```

---

### Frontend Setup

1. Create a React project with Vite:

```bash
npm create vite@latest frontend
cd frontend
npm install
```

2. Install dependencies:

```bash
npm install @mui/material @emotion/react @emotion/styled
```

3. Connect to backend API using Axios or Fetch:

```javascript
import { useEffect, useState } from 'react';

function App() {
  const [msg, setMsg] = useState("Loading...");

  useEffect(() => {
    fetch("http://127.0.0.1:8000/api/hello/")
      .then(res => res.json())
      .then(data => setMsg(data.message));
  }, []);

  return <h1>{msg}</h1>;
}

export default App;
```

4. Start the frontend:

```bash
npm run dev
```

---

## Folder Structure

```
ReactDjango/
├─ backend/        # Django project
│  ├─ backend/
│  └─ api/
├─ frontend/       # React project
│  ├─ src/
│  └─ public/
└─ README.md
```

---

## API Integration

* Ensure **CORS** is enabled in Django.
* Use absolute URLs (`http://127.0.0.1:8000/api/...`) for development.
* In production, you can serve React build with Django or use a proxy.

---

## License

MIT License © 2025
