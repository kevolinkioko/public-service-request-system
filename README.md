# Public Service Request System (Mini eCitizen-style)

Responsive citizen service-request prototype using HTML, CSS, JavaScript and Supabase Auth/Postgres/storage.

## Required features
- Citizen registration and sign-in
- Request form: category, location, description and optional image (5 MB max)
- Citizen sees own requests and status
- Admin dashboard, search, status filter, case counts and status updates
- Workflow: Pending → In Progress → Resolved
- Row-level security policies included

## 1. Create Supabase backend
1. Create a project at https://supabase.com/ and keep the database password private.
2. Open SQL Editor → New query. Paste all of `supabase-schema.sql` and Run.
3. In project settings/API or Connect, copy the Project URL and the publishable/anon public key.
4. Edit `app.js`: replace `PASTE_SUPABASE_PROJECT_URL` and `PASTE_SUPABASE_ANON_PUBLIC_KEY`.
5. Never put a service-role/secret key in browser JavaScript.
6. In Authentication settings, decide whether email confirmation is enabled. For quick testing you can disable confirmation temporarily; for real public use keep it enabled and configure email delivery.

## 2. Set up administrator
1. Open the site and register with your own email. Confirm email if required.
2. In Supabase SQL Editor, run this query after replacing the email:
   `update public.profiles p set role='admin' from auth.users u where p.id=u.id and u.email='YOUR-EMAIL@example.com';`
3. Sign out and sign back in. Admin tab should appear.
4. Never share your password or database credentials.

## 3. Test locally
Use VS Code with Live Server, or run `python -m http.server 8000` in this folder and open http://localhost:8000.
Test account registration, request submission, citizen history, admin status changes, search/filter and second-user privacy.

## 4. Upload to GitHub
Create a public repository named `public-service-request-system`. On the empty repository, Add file → Upload files, then upload the contents of this folder and commit them. The repo URL goes into the assignment's GitHub/GitLab Repository URL field.

## 5. Deploy
1. Create an account at https://www.netlify.com/ and choose Add new project / Import existing project.
2. Connect GitHub and select this repository.
3. Leave build command blank and set publish directory to `.` (repository root), then deploy.
4. Add the resulting HTTPS URL in Supabase Authentication → URL Configuration as Site URL and Redirect URL.
5. Test the deployed app in a private browser window. Use a separate citizen account and admin account to test permissions.
6. Submit the Netlify URL in the Live/Deployed URL field.

## Submission checklist
- Repository URL opens and contains source files.
- Live URL opens over HTTPS.
- Sign-up/login works.
- Citizen can submit and track a request.
- Admin can view all requests and update status.
- Counts change after status updates.
- No secrets or real citizen personal data in public repository.
- Submit before the portal countdown expires.

## Honest limitations
This is an academic prototype, not an official County service. Before production use, it needs approved branding/hosting, privacy notice, stronger operational monitoring, audit logging, rate limiting and backup procedures. Images are stored privately; this starter records image paths but does not yet show image previews in request cards.
