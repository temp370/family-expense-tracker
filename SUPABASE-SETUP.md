# Supabase Setup for Family Expense Tracker

This app supports a cloud-authenticated mode using Supabase.

## 1) Create Supabase project

1. Open https://supabase.com
2. Create a new project
3. Wait until the database is ready

## 2) Get project credentials

Go to:

- Project Settings → API

Copy:

- `Project URL`
- `anon public key`

These are safe to use in the frontend.

Do not copy or use the service role key in the frontend.

## 3) Configure Google OAuth

1. In Supabase, open:
   - Authentication → Providers → Google
2. Enable Google
3. Add your Google OAuth client ID and client secret
4. Set redirect URL to your GitHub Pages URL, for example:

```
https://temp370.github.io/family-expense-tracker/
```

You may also need to add the same URL in Google Cloud OAuth redirect settings.

## 4) Create database tables

Open the Supabase SQL editor and run:

```sql
create table if not exists profiles (
  id uuid primary key references auth.users(id),
  full_name text,
  avatar_url text,
  created_at timestamptz default now()
);

create table if not exists expenses (
  id uuid primary key default gen_random_uuid(),
  user_id uuid references profiles(id) not null,
  type text check (type in ('C','D')) not null,
  category text,
  desc text,
  amt bigint not null,
  ts bigint not null,
  pay_method text,
  who text,
  notes text,
  created_at timestamptz default now(),
  updated_at timestamptz default now()
);

alter table expenses enable row level security;

create policy "select_own" on expenses
  for select using (auth.uid() = user_id);

create policy "insert_own" on expenses
  for insert with check (auth.uid() = user_id);

create policy "update_own" on expenses
  for update using (auth.uid() = user_id) with check (auth.uid() = user_id);

create policy "delete_own" on expenses
  for delete using (auth.uid() = user_id);

create or replace function public.handle_new_user()
returns trigger as $$
begin
  insert into profiles (id, full_name, avatar_url)
  values (
    new.id,
    new.raw_user_meta_data->>'full_name',
    new.raw_user_meta_data->>'avatar_url'
  )
  on conflict (id) do nothing;
  return new;
end;
$$ language plpgsql;

create trigger on_auth_user_created
  after insert on auth.users
  for each row execute procedure public.handle_new_user();
```

## 5) Configure the app

Edit `index.html` and replace:

```js
const SUPABASE_URL = 'https://YOUR_PROJECT_REF.supabase.co';
const SUPABASE_ANON_KEY = 'YOUR_ANON_PUBLIC_KEY';
```

with your real values from Supabase.

## 6) Login flow

The app now supports:

- guest/local mode
- Google login with Supabase
- automatic merge from localStorage to Supabase after first login

## 7) Security notes

- Never store the Supabase service role key in the browser
- Never commit real secrets to this repo
- Keep Google OAuth configured with only the required redirect URL
- Keep the app public or private depending on your preference, but do not commit actual user data
