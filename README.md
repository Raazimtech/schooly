# Schooly

Schooly is the user-facing school workspace. Administrative account creation and school management live in the separate `SCHLY-admin` application.

## Architecture

- `schooly`: end-user portal for authenticated school accounts.
- `SCHLY-admin`: restricted administrator console. It is the only place with account creation and bulk CSV import.
- Supabase: shared project `cabdikariimibraahim808@gmail.com's Project`, using isolated `schooly_*` tables and the `schooly-accounts` Edge Function. Existing Safar Link and other application tables are not touched by Schooly.

## Accounts

Users sign in with an account ID and password. The backend maps IDs to internal non-user-facing Auth emails. There is no public signup.

## First run

Open `SCHLY-admin`. When the Schooly database has no administrator yet, the one-time bootstrap form is shown. After the first admin is created, the bootstrap path is permanently closed by the database control row.

## Security

The browser only uses the Supabase publishable key. The service-role key is used only inside the Edge Function for Auth account creation and password administration. Schooly tables use RLS, with authorization derived from trusted Auth `app_metadata` rather than editable user metadata.
