1. Project Overview
  # CampusOS

CampusOS is an intelligent university campus management platform that combines a live data dashboard with an AI-powered campus assistant. The platform manages five core campus systems: **Schedules, Rooms, Events, Announcements, and Assignments**. Users can view, add, edit, and delete records through the dashboard, while room bookings and event registrations can also be managed. All changes are stored persistently in a SQLite database, so updates remain available after reloading the application. The integrated AI agent uses **Groq and `openai/gpt-oss-120b` with native tool/function calling** to read and act on the same live database used by the dashboard. This allows users to ask questions about campus information, search for available rooms, check assignments or announcements, book rooms, and register for events without relying on stale or hardcoded information.

2. Tech Stack
   ## Tech Stack

* **Frontend:** HTML, CSS, Vanilla JavaScript
* **Backend:** Node.js + Express.js
* **Database:** SQLite
* **Database Driver:** better-sqlite3
* **AI/LLM:** Groq API
* **Default LLM:** `openai/gpt-oss-120b`
* **AI Integration:** OpenAI-compatible chat completions API with native tool/function calling
* **API:** REST API
* **Environment Management:** dotenv
* **Additional Libraries:** CORS, UUID
* **Runtime Requirement:** Node.js 18+

### AI Agent Tools

The CampusOS agent can use real backend tools including:

* `get_current_datetime`
* `list_schedules`
* `list_rooms`
* `search_available_rooms`
* `book_room`
* `cancel_room_booking`
* `list_events`
* `register_for_event`
* `cancel_event_registration`
* `list_announcements`
* `list_assignments`

The agent uses these tools to access the same live SQLite database as the dashboard.

3. Setup Instructions
   ## Setup Instructions

### Requirements

Make sure the following are installed:

* Node.js 18 or higher
* npm
* A Groq API key for the AI assistant

### 1. Clone the repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
cd campusos
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Create a `.env` file from the provided example:

```bash
cp .env.example .env
```

On Windows, you can also simply copy `.env.example` and rename the copy to `.env`.

Then open `.env` and add your Groq API key:

```env
GROQ_API_KEY=your_groq_api_key_here
```

You can optionally configure:

```env
GROQ_MODEL=openai/gpt-oss-120b
PORT=3000
```

### 4. Start the application

```bash
npm start
```

The server will start at:

```text
http://localhost:3000
```

Open that address in your browser.

### 5. Database initialization

On the first startup, CampusOS automatically creates the SQLite database and seeds it using the JSON files inside the `data/` directory.

After the database has been initialized, SQLite becomes the source of truth and changes persist across application restarts.

If you want to reset the database and reseed the original data, delete:

```text
campusos.db
```

and start the application again.

### Important

Do **not** commit your `.env` file or real API keys to GitHub.

The repository should contain:

```text
.env.example
```

but not:

```text
.env
```

4. Environment Variables
   ## Environment Variables

Create a `.env` file in the project root.

| Variable       | Required         | Default               | Description                             |
| -------------- | ---------------- | --------------------- | --------------------------------------- |
| `GROQ_API_KEY` | Yes for AI agent | —                     | API key used to access the Groq LLM API |
| `GROQ_MODEL`   | No               | `openai/gpt-oss-120b` | LLM model used by the CampusOS agent    |
| `PORT`         | No               | `3000`                | Port used by the Express server         |

### `.env.example`

```env
GROQ_API_KEY=your_groq_api_key_here
GROQ_MODEL=openai/gpt-oss-120b
PORT=3000
```

**Security:** Never commit real API keys to the repository. Only commit `.env.example`.

5. How to Use the Agent
   ## How to Use the AI Agent

The **Campus Assistant** appears on the right side of the CampusOS dashboard.

Users can ask natural-language questions about the five campus systems.

### Schedule Questions

Examples:

```text
When is my next class?

What classes do I have on Wednesday?

Show me today's schedule.

Which room is CSE 4113 in?
```

### Room Questions

Examples:

```text
Which rooms are available?

Which labs have a projector?

Find a room for 30 people tomorrow.

Is there a free room tomorrow from 3 PM to 5 PM?
```

### Room Actions

The agent can also perform room actions:

```text
Book room 7A02 tomorrow from 3 PM to 5 PM.
```

If required information is missing, the agent asks for clarification rather than guessing.

For example, if the user says:

```text
Book me any room tomorrow afternoon.
```

the agent will ask for the specific room and time information required for the booking.

### Event Questions

Examples:

```text
What events are coming up?

What events are happening this week?

How many people are registered for the Guest Lecture?
```

### Event Registration

Users can ask:

```text
Register me for the Guest Lecture on Deep Learning.
```

The agent requests the student's required information when necessary and checks event availability and registration rules.

### Announcement Questions

Examples:

```text
Show me the latest announcements.

Are there any high priority announcements?

What announcements are currently available?
```

### Assignment Questions

Examples:

```text
What assignments are due this week?

Show me my pending assignments.

Which assignments have been graded?
```

### Live Data

The AI agent does not rely on a static copy of the dashboard data.

It calls backend tools that access the same live SQLite database used by the dashboard.

Therefore:

1. Make a change in the dashboard.
2. Reload or navigate as needed.
3. Ask the AI agent about that information.
4. The agent reads the updated database state.

This keeps the dashboard and AI assistant synchronized.

6. Your Submission Checklist
   | Requirement                       | CampusOS                         |
| --------------------------------- | -------------------------------- |
| Public GitHub repository          | **You need to make/verify this** |
| README with setup instructions    | ✅                                |
| Project overview                  | ✅                                |
| Tech stack                        | ✅                                |
| LLM identified                    | ✅ Groq / `openai/gpt-oss-120b`   |
| Database identified               | ✅ SQLite                         |
| `.env.example`                    | ✅                                |
| No real API key in `.env.example` | ✅                                |
| Schedules visible                 | ✅                                |
| Rooms visible                     | ✅                                |
| Events visible                    | ✅                                |
| Announcements visible             | ✅                                |
| Assignments visible               | ✅                                |
| Add                               | ✅                                |
| Edit                              | ✅                                |
| Delete                            | ✅                                |
| Persistent SQLite storage         | ✅                                |
| Room booking                      | ✅                                |
| Room booking conflict checking    | ✅                                |
| Event registration                | ✅                                |
| AI tool calling                   | ✅                                |
| AI reads live database            | ✅                                |
