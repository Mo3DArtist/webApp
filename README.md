# Personal Expense & Income Tracker — Update Guide

This update adds:
- **Income tracking** (salary + freelance, both variable) alongside expenses
- **Monthly dashboard** in the app: total spent, total income, net, top spending category
- **Budget limits** per category with a warning when you go over
- **Monthly Summary sheet** with auto-calculated formulas (mirrors the layout of your old manual sheet)

## What changed

- `Code.gs` — replace the whole content of your Apps Script project with this new version.
- `index.html` — replace the file on GitHub with this new version.
- `manifest.json` — unchanged, no need to re-upload unless you don't have it yet.

## Step 1 — Update the Apps Script

1. Open your Google Sheet, go to **Extensions > Apps Script**.
2. Select all the existing code (Ctrl+A) and delete it.
3. Paste in the new `Code.gs`.
4. Run the `setup` function again (dropdown next to Run > select `setup` > Run).
   - This is safe to re-run — it recreates the Expenses/Income/Budgets/Monthly Summary tabs with headers. It does **not** delete your existing rows in Expenses since the code only clears headers on the sheets it manages fresh, but to be safe: **if you already have expense data you care about, check the Expenses tab after running setup to confirm your rows are still there.**
5. Go to **Deploy > Manage deployments > click the pencil icon (Edit) > Version: New version > Deploy**.
   - You do NOT need a new URL — the existing Web app URL keeps working.

## Step 2 — Update the web page

1. Go to your GitHub repo.
2. Open `index.html`, click the pencil icon (Edit this file).
3. Select all (Ctrl+A), delete, and paste in the new `index.html` content.
4. Scroll down, click **Commit changes**.
5. Give GitHub Pages a minute, then refresh your app.

## Step 3 — Set your budget limits (optional)

1. Open your Google Sheet, go to the new **Budgets** tab.
2. Next to each category, type a monthly limit in جنيه (e.g. لحوم → 1500).
3. Leave it blank for any category you don't want to track a limit for.
4. The app will show a warning banner on the dashboard if you go over any limit you set, for the current month.

## How income works now

- In the app, there's a toggle at the top of the form: **مصروف** / **دخل**.
- Switch to **دخل**, type the source (e.g. "مرتب" or "فريلانس - مشروع كذا"), and the amount.
- Every income entry goes to a separate **Income** tab in the Sheet. You can add as many entries as you want in a month (salary + freelance + anything else) — the dashboard sums them all up.

## The dashboard (top of the app)

Shows, for the current calendar month:
- Total expenses
- Total income
- Net (income − expenses)
- Your top spending category
- Any budget warnings

Tap "تحديث" to refresh it manually, or it refreshes automatically after you add anything.

## Monthly Summary sheet

A new tab called **Monthly Summary** was created with one row for the current month, using formulas that auto-total each category from the Expenses tab, plus total income and net. This mirrors the format of your old manual sheet.

- Columns match the app's categories (لحوم, بقالة, خضار وفاكهة, مواصلات, فواتير, إيجار, ترفيه, صحة, تعليم, أخرى) rather than your old bucket names (كهرباء, اتحاد ملاك...), since the app tracks purchases at that level of detail.
- The last column, **"التحويش (يدوي)"**, is left blank on purpose — how much you actually choose to set aside as savings each month is a personal decision, not something derivable from spend/income automatically, so type it in yourself each month.
- **To add next month's row**: copy row 2 (A2:N2) and paste it into row 3, then change the date in A3 to the 1st of the next month. The formulas will recalculate for that month automatically.

## Notes

- First request after the app has been idle can take a few seconds (Apps Script "waking up"). This is normal and only happens occasionally.
- Auto-categorization corrections are stored per-device (phone's local storage), not synced across devices.
- Don't share your Apps Script Web App URL publicly.
