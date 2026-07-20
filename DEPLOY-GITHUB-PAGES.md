# Publishing DM Imprints on GitHub Pages

No command line needed — this is all done through the GitHub website.
About 15 minutes start to finish.

Do `SETUP-GOOGLE-SHEET.md` **first** if you haven't. It's easier to connect the
form before the site is public than after.

---

## Step 1 — Make a GitHub account

Go to <https://github.com> and sign up. Free plan is all you need.

**Pick your username carefully** — it becomes part of your web address.
Something like `dmimprints` gives you `dmimprints.github.io`, which reads well
on a business card. Avoid numbers and dashes if you can.

Write your username down. You'll need it in Step 5.

## Step 2 — Create the repository

A "repository" (repo) is just a folder that lives on GitHub.

1. Click the **+** in the top-right → **New repository**.
2. **Repository name:** type your username followed by `.github.io`

   So if your username is `dmimprints`, the repo name is exactly:

   ```
   dmimprints.github.io
   ```

   This exact naming is what makes your site live at the clean root address
   instead of a longer one with a folder on the end. It has to match your
   username precisely.

3. Set it to **Public**. (Private repos don't get free Pages hosting.)
4. Leave every checkbox unticked — no README, no .gitignore.
5. Click **Create repository**.

## Step 3 — Upload your site files

On the empty repo page, click the **uploading an existing file** link.

Now drag these in from the `site` folder:

- `index.html`
- `favicon.svg`
- `robots.txt`
- `sitemap.xml`
- the whole **`images`** folder

**Do not upload** `SETUP-GOOGLE-SHEET.md`, `DEPLOY-GITHUB-PAGES.md`, or
`apps-script-code.gs.txt`. Those are your notes, not part of the website.
Nothing breaks if you do upload them — they'd just be publicly visible.

Wait for all the files to finish, scroll down, click **Commit changes**.

> If dragging the `images` folder doesn't work in your browser, open the folder
> and drag the 11 image files in directly, then use the "Add file → Create new
> file" trick. Easier fix: use Chrome or Edge, which handle folder drops fine.

## Step 4 — Turn on Pages

1. In your repo, click **Settings** (top of the page).
2. In the left sidebar, click **Pages**.
3. Under **Source**, choose **Deploy from a branch**.
4. Under **Branch**, choose **main**, folder **/ (root)**, click **Save**.

Wait 1–3 minutes. Refresh the page. A green banner appears with your live URL:

```
https://YOUR-USERNAME.github.io/
```

Click it. Your site is live.

## Step 5 — Fix the placeholder URLs

Three files have `YOUR-USERNAME.github.io` written in them as a placeholder.
Until you replace it, link previews on Instagram and iMessage will be broken.

For each file below: open the repo, click the file, click the **pencil icon**,
use Ctrl+F (Cmd+F on Mac) to find `YOUR-USERNAME`, replace with your actual
username, then **Commit changes**.

| File | How many to replace |
|------|--------------------|
| `index.html` | 5 |
| `robots.txt` | 1 |
| `sitemap.xml` | 1 |

Changes go live about a minute after committing.

---

## Making changes later

Everything is editable through the website — no software to install.

- **Edit text:** click the file → pencil icon → edit → **Commit changes**.
- **Add photos:** **Add file → Upload files**, drop them into `images`.
- **Replace a photo:** upload the new one with the *exact same filename*.

Changes take about a minute to appear. If you don't see them, hard-refresh
your browser (Ctrl+Shift+R, or Cmd+Shift+R on Mac).

## Getting a real domain later

You don't need one to launch, and `yourname.github.io` is perfectly respectable.
But when you're ready, a domain like `dmimprints.com` runs $10–15/year from any
registrar (Namecheap, Cloudflare, Porkbun).

GitHub Pages supports custom domains for free. The setup is Settings → Pages →
Custom domain, plus a few DNS records at your registrar. Ask me when you get
there and I'll walk you through it — and update the meta tags to match.

---

## Two things to know

**Your source code is public.** That's the tradeoff for free hosting. It means
your Google Apps Script URL is visible to anyone who views the page source.

Practically this is low-risk: the URL only lets someone *add rows*, never read
your bookings, and the form has a honeypot that stops ordinary bots. If you
ever do get flooded with junk entries, the fix is to make a new deployment in
Apps Script (which generates a fresh URL) and update `index.html`. Tell me if
that happens.

**Your photos are downloadable.** True of every website — anything displayed in
a browser has already been downloaded to view it. If you want visible
watermarks on the gallery images, I can add those.

---

## If something goes wrong

**404 page not found.** Usually the file is named something other than
`index.html`, or it got uploaded inside a subfolder instead of at the top level.
Check that clicking your repo name shows `index.html` in the list immediately.

**Site loads but photos are missing.** The `images` folder didn't upload, or
uploaded with a different name. It must be lowercase `images`.

**Form says "not connected yet".** You skipped Step 5 of the Google Sheet
setup — the Apps Script URL is still a placeholder in `index.html`.

**Changes aren't showing.** Give it 2 minutes, then hard-refresh. GitHub Pages
caches aggressively.
