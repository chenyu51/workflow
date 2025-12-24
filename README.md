# Growth Workflow

This repository hosts a lightweight personal growth workflow built around GitHub Issues and Actions. The intent is simple: connect long-term goals to daily effort and weekly reflection so momentum is visible and sustainable.

## How it works
- **Long-term goals → daily effort → weekly review**: capture small daily moves and consolidate insights weekly to stay aligned with your direction.
- **Time investment**: aim for **3 minutes every day** and **10 minutes every week** to keep the habit easy to sustain.
- **Issue automation**: GitHub Actions creates Daily and Weekly issues automatically so you never skip a reflection slot.

## Usage
1. Ensure repository labels exist before running the workflows (recommended: `daily`, `weekly`, plus optional `skill:*`, `mindset:*`, `habit:*`).
2. Enable workflows with appropriate permissions (Settings → Actions → General → Workflow permissions → **Read and write permissions** if you want issues auto-created).
3. Use the Issue Forms for a guided experience:
   - Daily form focuses on facts, one strengthening win, and one improvement.
   - Weekly form captures real growth, efforts that did not differentiate you, and one focus for next week.

## Suggested labels
- Core cadence: `daily`, `weekly`
- Growth focus (suggested patterns, use as needed): `skill:*`, `mindset:*`, `habit:*`

## Timezone and scheduling
- Workflows assume the **America/Toronto** timezone. Cron expressions use UTC; see comments inside workflow files for the corresponding Toronto times and how to adjust.

## Files
- `.github/ISSUE_TEMPLATE/daily.yml` – Daily Issue Form
- `.github/ISSUE_TEMPLATE/weekly.yml` – Weekly Issue Form
- `.github/workflows/daily_issue.yml` – Automated Daily issue creation (weekdays)
- `.github/workflows/weekly_issue.yml` – Automated Weekly issue creation (Fridays)
