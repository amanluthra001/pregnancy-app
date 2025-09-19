Pregnancy App (MERN)
AI‑ready maternal health app with a landing page, Patient/Doctor portals, MongoDB backend, and educational resources pages. Simple to run locally and easy to extend with ML later.

Repository
GitHub: https://github.com/amanluthra001/pregnancy-app

Features
Role-based auth with JWT (Patient, Doctor).

Patient questionnaire with provisional risk score.

Doctor can assign patients and view latest submissions.

Static educational pages and utility components (Kick Counter, Health Monitoring, etc.).

Prerequisites
Node.js LTS (includes npm).

MongoDB Community Server installed and running locally.

A terminal (VS Code integrated terminal recommended).

Project structure
server/

src/ index.js, middleware/auth.js, models/, routes/

.env.example (copy to .env)

package.json

public/

minor_project.html, styles.css

patient.html, doctor.html

nutrition.html, exercise.html, fetal-development.html, mental-health.html

kick-counter.html, health-monitoring.html, risk-assessment.html, exercise-guidance.html, emergency-access.html

1) Clone
HTTPS:

git clone https://github.com/amanluthra001/pregnancy-app.git

SSH:

git clone git@github.com:amanluthra001/pregnancy-app.git

cd pregnancy-app

2) Configure environment
cd server

Copy example env:

Windows: copy .env.example .env

macOS/Linux: cp .env.example .env

Open .env and ensure:

MONGO_URI=mongodb://127.0.0.1:27017/pregnancy_app

JWT_SECRET=replace_me

PORT=5000

3) Install dependencies
From pregnancy-app/server:

npm install

4) Start MongoDB
Windows (service):

Start “MongoDB” in Services app, or run in Admin PowerShell: net start MongoDB

macOS (Homebrew):

brew services start mongodb-community@7.0

Linux (systemd):

sudo systemctl start mongod

Verify:

mongosh --eval "db.runCommand({ connectionStatus: 1 })" should show ok: 1

5) Run the backend
From pregnancy-app/server:

npm run dev

Expected:

“Server running on http://localhost:5000”

Health check in browser:

http://localhost:5000/api/health should return {"ok": true}

6) Serve the frontend (choose one)
Option A (recommended): serve public on port 3000

Open a new terminal

cd pregnancy-app/public

npx serve -p 3000

Open http://localhost:3000/minor_project.html

Option B: VS Code Live Server (often http://127.0.0.1:5500)

Open minor_project.html with Live Server

If CORS error appears, see “CORS configuration” below

Option C: open file directly

Double‑click public/minor_project.html

Works, but a static server is more consistent for relative paths.

7) Using the app
Patient portal (public/patient.html)

Register (role patient) or Login.

After auth, “My User ID” is displayed with a Copy button.

Submit questionnaire to get provisional risk label.

Doctor portal (public/doctor.html)

Register (role doctor) or Login.

Paste the patient’s full User ID into “Assign Patient”.

Use “Refresh” to see Patients and Latest Questionnaires.

Educational pages

“Learn More →” links from landing page open Nutrition, Exercise, Fetal Development, Mental Health.

Components

Cards link to Kick Counter, Health Monitoring, Risk Assessment, Exercise Guidance, Emergency Access.

8) CORS configuration (if using Live Server)
The backend allows http://localhost:3000 by default.

If serving the frontend at http://127.0.0.1:5500 or http://localhost:5500, add these origins in server/src/index.js CORS setup and restart the backend:

http://127.0.0.1:5500

http://localhost:5500

Example:

js
app.use(cors({
  origin: [
    "http://localhost:3000",
    "http://127.0.0.1:3000",
    "http://127.0.0.1:5500",
    "http://localhost:5500"
  ],
  credentials: true
}));
9) Common issues
Health endpoint not reachable:

Ensure MongoDB is running; check PORT in .env; restart backend.

CORS error (preflight blocked):

Add the page’s origin to CORS list (see above) and restart backend.

“Email already registered”:

Use Login with that email, or register a different email.

Assign Patient fails:

Paste the full 24‑character “User ID” shown on the Patient page after auth.

10) Scripts
Backend (from server):

npm run dev → dev server with auto-reload

npm start → production server

11) Roadmap
Replace provisional risk with ML microservice (store mlScore/mlLabel/mlVersion).

Migrate static pages to React for routing/state.

Security hardening: validation, rate limiting, HttpOnly cookies.

12) Contributing
Create a feature branch:

git checkout -b feature/your-change

Commit and push:

git add .

git commit -m "Describe your change"

git push -u origin feature/your-change

Open a Pull Request to main.
