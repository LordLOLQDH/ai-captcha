# AI CAPTCHA — VERIFY YOU ARE A ROBOT

An experimental reverse-CAPTCHA protocol. It asks a client to solve a server-generated structured challenge before issuing a short-lived, single-use token.

## Live project
- Website: https://lordlolqdh.github.io/ai-captcha/
- Repository: https://github.com/LordLOLQDH/ai-captcha
- Machine protocol: https://lordlolqdh.github.io/ai-captcha/.well-known/ai-captcha.json
- Supabase gateway: https://eopvkwhcgznvubesaszv.supabase.co/functions/v1/ai-captcha-gateway

## Protocol
Send HTTPS POST requests with JSON to the gateway.

1. Request a challenge: `{"action":"challenge"}`
2. Add the three values in `challenge.values` and verify: `{"action":"verify","challenge_id":"<challenge_id>","answer":{"answer":1234}}`. Replace 1234 with the calculated sum.
3. Send `{"action":"site"}` with `Authorization: Bearer <access_token>` to retrieve the archive once.

Challenges expire after 180 seconds and allow at most three incorrect answers. Access tokens expire after 600 seconds and are single-use. Expected answers and token hashes are stored server-side in Supabase.

## Backend
The `ai-captcha-gateway` Supabase Edge Function runs in the existing KDS AI project and uses `ai_captcha_challenges` and `ai_captcha_access_tokens`. Both tables have RLS enabled and no public policies; the function accesses them server-side.

## Security limitation
This is an experiment, not a reliable AI detector. Humans and scripts can solve the same challenge. It demonstrates challenge-gated access, not proof of AI identity. Do not use it as the sole security control for accounts, payments, personal data, or production APIs.

## Local use
Open `index.html` in a browser or enable GitHub Pages for the repository's `main` branch. No frontend build step or client-side secret is required.


## Administrator password access
The landing page includes an administrator password field. Password verification is performed server-side by the Edge Function; the password is never embedded in the public HTML. Before using it, configure the Edge Function secret named `AI_CAPTCHA_ADMIN_PASSWORD` in Supabase with your chosen administrator password. The endpoint returns a short-lived, single-use token only after a successful check. If the secret is missing, login returns `admin_password_not_configured`.
