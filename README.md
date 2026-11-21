# Secret Santa: setup (about 10 minutes, free)

Two files:
- `schema.sql` sets up the database. It makes the assignments and keeps them hidden.
- `index.html` is the whole app: one page that you host anywhere.

## 1. Create the database (Supabase, free tier)
1. Go to https://supabase.com and create a new project.
2. Open **SQL Editor**, paste in all of `schema.sql`, and click **Run**.
3. Open **Project Settings → API** (or **API Keys**) and copy:
   - the **Project URL** (`https://xxxx.supabase.co`)
   - the **public key** (`anon`, or `sb_publishable_…`). Don't use the `service_role` or secret key.

## 2. Connect the page
Open `index.html`, find `SS_CONFIG` near the top, and paste in those two values.

## 3. Put it online
Pick whichever of these is easiest:
- **Netlify Drop:** drag the folder onto https://app.netlify.com/drop and you get a link right away.
- **GitHub Pages**, **Vercel** or **Cloudflare Pages:** any static host works.

## 4. Run your exchange
1. Open your link, enter the exchange name and your name, and click **Create game**.
2. Send the invite link to the group. People show up in your list as they join.
3. When everyone's in, click **Everyone's in. Make assignments**. This closes sign-ups.
4. Everyone (you included) opens the page and taps **Draw a name**.

## How it stays secret
- The database shuffles everyone into **one loop** (A→B→C→…→A). It never sends that list to any browser.
- The page can only call a few functions. `reveal` returns the caller's own person and nothing else. All tables are locked to the public key.
- Each person gets a private token, saved in their browser. The **personal link** on their screen lets them draw from another device.
- Even as host, you only see *who has drawn*. You never see who got whom.
- One caveat: as the owner of the Supabase project, you *could* open the `ss_assignments` table in the dashboard and work it out. Just don't look. 🎅

## Handy to know
- At least 3 people are needed.
- If someone joins late, the host can **Reset the draw**. Sign-ups reopen and everyone draws again.
- Before the draw, the host can remove someone by tapping × twice.
