# Connecting your booking form to a Google Sheet

Every booking request will land as a row in a spreadsheet you own, and email
you a copy at the same time. No new accounts — this uses the Google account
you already have.

Takes about 10 minutes, once.

---

## Step 1 — Make the spreadsheet

1. Go to <https://sheets.google.com> and create a **Blank spreadsheet**.
2. Name it something like `DM Imprints — Bookings`.
3. Leave it empty. The script builds the column headers for you on the first
   submission.

## Step 2 — Open the script editor

In that spreadsheet, go to **Extensions → Apps Script**.

A code editor opens in a new tab with a mostly empty `Code.gs` file.

## Step 3 — Paste in the code

1. Select everything already in `Code.gs` and delete it.
2. Open `apps-script-code.gs.txt` (in this same folder), copy all of it, paste it in.
3. Click the **save icon** (💾).

## Step 4 — Publish it

1. Click **Deploy → New deployment**.
2. Click the **gear icon** next to "Select type" and choose **Web app**.
3. Fill in:
   - **Description:** `Booking form`
   - **Execute as:** `Me`
   - **Who has access:** `Anyone` ← this matters, see the note below
4. Click **Deploy**.
5. Google will ask you to **Authorize access**. Approve it with your Google
   account.
   - You will hit a scary screen saying **"Google hasn't verified this app."**
     This is expected — *you* are the developer of *your own* script, and
     Google shows this for every personal script. Click **Advanced**, then
     **Go to [your project name] (unsafe)**, then **Allow**.
6. Copy the **Web app URL** it gives you. It looks like:

   ```
   https://script.google.com/macros/s/AKfycbx...long-string.../exec
   ```

> **On "Who has access: Anyone"** — this means anyone can *send data to* your
> script. It does **not** make your spreadsheet public and nobody can read your
> bookings. It has to be set this way, because visitors to your site aren't
> logged into your Google account. The honeypot field in the form filters out
> most bots.

## Step 5 — Paste the URL into your site

1. Open `index.html` in any text editor.
2. Find this line (it's near the bottom, around line 310):

   ```js
   const SHEET_ENDPOINT = "PASTE_YOUR_APPS_SCRIPT_URL_HERE";
   ```

3. Replace `PASTE_YOUR_APPS_SCRIPT_URL_HERE` with the URL you copied. Keep the
   quotes:

   ```js
   const SHEET_ENDPOINT = "https://script.google.com/macros/s/AKfycbx.../exec";
   ```

4. Save.

## Step 6 — Test it

Open `index.html` in your browser, fill out the booking form with fake details,
and submit.

Within a few seconds you should see:

- a new row in your spreadsheet (a **Bookings** tab appears automatically), and
- an email in `dmprojectz24@gmail.com`.

If both happened, you're connected. Delete the test row.

---

## Troubleshooting

**Nothing appears in the sheet.**
Open the Apps Script tab → **Executions** in the left sidebar. If you see a
failed run, the error message is there. Most common cause is skipping the
authorization step in Step 4.

**Form says "not connected yet".**
The URL in `index.html` wasn't replaced, or it's missing the `/exec` on the end.

**You edit the script later.**
Changes don't go live automatically. You have to **Deploy → Manage deployments
→ edit (pencil) → Version: New version → Deploy**. Otherwise the site keeps
using the old code.

**You want notifications at a different address.**
Change `NOTIFY_EMAIL` at the top of the script, then redeploy as above.

---

## A note on how the form reports success

The site shows "Request sent" as soon as it hands the data off to Google.
Because of the way browsers restrict cross-site requests, the page can't read
Google's reply, so it can't detect a failure on Google's end.

Practically this means: if you ever change the script, **submit one test
booking afterward** to confirm rows are still landing. The email copy is your
safety net — if bookings stop arriving in your inbox, something upstream broke.
