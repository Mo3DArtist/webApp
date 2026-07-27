# Personal Expense Tracker — Setup Guide

Three free pieces, no server needed:
1. A Google Sheet (your database)
2. A Google Apps Script (the bridge between the web page and the Sheet)
3. GitHub Pages (free static hosting for the web page)

## Step 1 — Create the Google Sheet

1. Go to Google Sheets and create a new blank spreadsheet.
2. Name it whatever you like, e.g. "Expenses".

## Step 2 — Add the Apps Script

1. In the Sheet, go to **Extensions > Apps Script**.
2. Delete the placeholder code and paste in the full contents of `Code.gs` (included in this folder).
3. In the toolbar, select the function `setup` from the dropdown next to the Run button, then click **Run**.
   - The first time, Google will ask for permissions. Click through and allow it (it's your own script acting on your own sheet).
   - This creates an "Expenses" tab with the right headers.
4. Click **Deploy > New deployment**.
   - Click the gear icon next to "Select type" and choose **Web app**.
   - Execute as: **Me**
   - Who has access: **Anyone**
   - Click **Deploy**.
5. Copy the **Web app URL** it gives you (looks like `https://script.google.com/macros/s/XXXXX/exec`). You'll need this in Step 4.

Whenever you edit `Code.gs` later, go to **Deploy > Manage deployments > Edit (pencil icon) > New version > Deploy**, otherwise your changes won't take effect.

## Step 3 — Put the site on GitHub Pages

1. Create a new **public** GitHub repo, e.g. `my-expenses`.
2. Upload `index.html` and `manifest.json` from this folder to the repo (drag and drop works fine on github.com).
3. Go to the repo's **Settings > Pages**.
4. Under "Source", choose the `main` branch and `/ (root)` folder, then Save.
5. GitHub will give you a URL like `https://yourusername.github.io/my-expenses/`. That's your app.

## Step 4 — Connect the page to your Sheet

1. Open your GitHub Pages URL on your phone (or desktop).
2. Tap the gear icon (top-left).
3. Paste the **Web app URL** from Step 2 into "رابط الـ Web App".
4. (Optional) Paste your Google Sheet's normal URL too, so you get a quick link to open it.
5. Save.

## Step 5 — Add it to your iPhone home screen

1. Open the GitHub Pages URL in Safari.
2. Tap the Share icon > **Add to Home Screen**.
3. Now it opens full-screen like a real app, no browser bar.

## How the auto-categorization works

- The page ships with a starter list of Arabic keywords mapped to categories (e.g. "لحمة" → "لحوم", "لبن" → "بقالة").
- If it doesn't recognize a word, you just pick the category yourself once — it saves that correction in the phone's local storage, so next time it recognizes it automatically. This is per-device, not synced, so if you use it from two phones you'll teach each one separately.
- To edit the built-in keyword list, open `index.html` and edit the `DEFAULT_KEYWORDS` object near the top of the `<script>` section.

## Viewing your monthly analysis

The app only handles fast data entry. All analysis happens in the Sheet itself:
- Use a **Pivot Table** (Insert > Pivot table) with rows = Category, values = Sum of Amount, to see spend per category.
- Add a second pivot filtered by "Type" (Fixed vs Variable) to separate rent/bills from day-to-day spending.
- Insert a simple pie or bar chart from either pivot table for a visual monthly breakdown.

## Notes / limitations

- This is intentionally simple: no login, no multi-user support. Anyone with your Apps Script URL could technically POST data to your sheet, so don't publish that URL anywhere public — it only lives in your phone's local storage.
- If Apps Script ever feels slow (it can have a short delay on first request after being idle), that's normal for the free tier.
