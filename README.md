# StudyHub — AI-only Classes 9 & 10

A Flask-based study materials website for Class 9 and Class 10 **Artificial Intelligence**.

## What's new in this version

- Responsive mobile + desktop student interface.
- Mobile navigation menu.
- Responsive admin dashboard.
- Supabase Storage integration for cloud file uploads.
- Private Supabase bucket support using short-lived signed download URLs.
- Existing local uploads continue to work when cloud storage is not configured.
- Database automatically adds storage metadata columns to an existing `studyhub.db`.

## Run locally

1. Create/activate a virtual environment.
2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Copy `.env.example` to `.env` and set values. The application automatically loads `.env` at startup using `python-dotenv`.

4. Start:

```bash
python app.py
```

Open `http://localhost:5000`.

## Supabase Storage setup

Create a Supabase project and create a **private** Storage bucket named `study-materials` (or choose another name and set `SUPABASE_BUCKET`).

Set these environment variables before starting the app:

```text
SUPABASE_URL=https://YOUR_PROJECT_REF.supabase.co
SUPABASE_SERVICE_ROLE_KEY=YOUR_SERVICE_ROLE_KEY
SUPABASE_BUCKET=study-materials
SUPABASE_SIGNED_URL_SECONDS=300
```

The service-role key is a **server secret**. Never put it in frontend JavaScript, HTML, GitHub, or client-side code.

When these variables are present, new uploads are sent directly from the Flask server to Supabase Storage. Student downloads use short-lived signed URLs. Deleting a material also removes its cloud object.

## Admin credentials

Use environment variables in production:

```text
ADMIN_USERNAME=your-admin-name
ADMIN_PASSWORD=your-strong-password
SECRET_KEY=your-long-random-secret
```

Do not deploy with the default `admin/admin123` credentials.

## Current content model

- Class 9 → Artificial Intelligence
- Class 10 → Artificial Intelligence
- Notes
- Sample Papers
- Worksheets
- Assignments
- Important Questions
- Announcements

Students do not need accounts. Only the owner/admin can upload or delete content.

## Important production note

The current release keeps SQLite for local metadata. Before public deployment, move metadata to a managed PostgreSQL database and configure production environment variables. Cloud file storage is already separated behind the storage backend fields so this migration can be done without changing the student-facing flow.
