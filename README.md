# MANPA Care

Mobile-first monitoring application for scheduled Tuesday and Friday recordings. Student health data is private: deploy only with an approved Supabase project and restrict administrator access.

## Run locally

1. Create a Supabase project, then copy `.env.example` to `.env.local` and add the public URL and anon key.
2. Link the project with the Supabase CLI and run `supabase db push` to create the schema, 26 empty classes, RLS policies, constraints, and realtime publication.
3. Set Edge Function secrets: a long random `BOOTSTRAP_SECRET`, and `BOOTSTRAP_ADMIN_PASSWORD` (set this to the approved initial password). Supabase automatically provides `SUPABASE_SERVICE_ROLE_KEY` to deployed functions; never add it to frontend variables or create it as a custom secret. Deploy `bootstrap-admin`.
4. Set `BOOTSTRAP_ADMIN_USERNAME` and `BOOTSTRAP_ADMIN_PASSWORD`, then call the function once from a protected terminal with header `x-bootstrap-secret`. It creates the sole first administrator and forces password replacement at first login. Delete or rotate bootstrap secrets after this operation.
5. Run `npm.cmd install`, then `npm.cmd run dev`. For production, deploy to Vercel and add the same two `VITE_` variables.

The client never contains a service-role key. A temporary password must be communicated privately; it is intentionally absent from the application UI.
