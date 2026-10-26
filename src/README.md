# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- View current activity participants
- Teacher-only student registration and unregistration

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Configure teacher credentials in the environment (do not commit credentials):

   ```
   export TEACHER_USERNAME=teacher
   export TEACHER_PASSWORD='use-a-strong-password'
   ```

3. Run the application:

   ```
   uvicorn src.app:app --reload
   ```

4. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

Use HTTPS when exposing the application beyond local development. Teacher credentials
are sent using HTTP Basic authentication and are held only in browser memory while
logged in. If the teacher credentials are not configured, login and all registration
changes are unavailable; activity and participant viewing remains public.

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/auth/login`                                                      | Validate teacher credentials (HTTP Basic)                           |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Register a student (teacher authentication required)                |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Unregister a student (teacher authentication required)            |

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

All activity data is stored in memory, which means it will be reset when the server
restarts. Teacher credentials are configured through `TEACHER_USERNAME` and
`TEACHER_PASSWORD`; they are not stored in the repository.
