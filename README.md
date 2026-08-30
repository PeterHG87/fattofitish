[README.md](https://github.com/user-attachments/files/31619542/README.md)
# Recomp Tracker — accounts for Peter and Ilina

Real login now, not just picking a name. Each of you creates your own account
with an email and password, and from then on you only ever see your own
weight, food, targets, and training — completely private from each other.

## One-time setup (only one of you needs to do this part)

1. Go to https://supabase.com, sign up free, create a new project.
2. In the dashboard, go to **Authentication → Providers**, and make sure
   **Email** is enabled (it is by default). Optionally, under
   **Authentication → Settings**, you can turn off "Confirm email" if you'd
   rather skip the email-confirmation step for a private two-person app —
   otherwise each new signup gets a confirmation email first.
3. Go to **SQL Editor → New query**, paste in the contents of `schema.sql`
   (included here), and run it. This creates the `profiles` and `kv_store`
   tables with security rules so each person can only read/write their own
   rows.
4. Go to **Project Settings → API**, copy the **Project URL** and the
   **anon public** key.
5. Host `index.html` somewhere (see below), open it, and paste in that URL
   and key when asked. This is saved per-device, not per-account.

## Hosting it (free)

Easiest: drag this folder onto **https://app.netlify.com/drop** — you get a
free URL instantly. Share that URL with Ilina.

## Using it

- First time on a device: paste in the Supabase URL/key once (step 5 above).
- Then **Create account** with an email and password.
- You'll be asked for your starting weight, height, age, goal weight, and
  how fast you want to lose (kg/week) — this sets your calorie and macro
  targets automatically. You can adjust height, age, goal, and rate anytime
  via "Edit goals", and override any individual target (calories, protein,
  carbs, fat) directly if you'd rather set your own numbers.
- Ilina does the same "Create account" step on her phone, with her own
  email/password and her own goals — her data never overlaps with yours.

## Notes

- Passwords are handled entirely by Supabase's auth system — this app never
  sees or stores them itself.
- Forgot password / password reset isn't wired up in this version; if that
  comes up, it's a small addition — just ask.
- **Food database is shared**: when anyone (you, Ilina, or any future account)
  searches and saves a new food, it's added to a shared list everyone can see
  and search — not private to that person. Personal logs (what you actually
  ate, your weight, your targets) stay completely private per account.
- If you re-run `schema.sql` on an existing project, it's safe — the new
  `shared_foods` table is added alongside what's already there without
  touching your existing data.
- **`food-data.sql`**: a large batch of pre-researched Swedish restaurant and
  coffee shop items (McDonald's, MAX, Burger King, KFC, Sibylla, Espresso
  House, Wayne's Coffee, Starbucks) with real macros. Run this once in
  Supabase's SQL Editor after `schema.sql` to pre-populate the shared food
  list — it's independent of the website code, so it doesn't require a
  redeploy, and it's safe to re-run later if updated.
