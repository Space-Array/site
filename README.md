# Space Array website

The public website of the Space Array Initiative: https://spacearray.org

The site is plain HTML and CSS. GitHub Pages publishes the `main` branch. Every merge to `main` goes live within a few minutes.

## Files

| File | Page |
| --- | --- |
| `index.html` | Home |
| `science.html` | Science |
| `sharp.html` | SHARP |
| `technology.html` | Technology |
| `team.html` | Team (the list comes from `team.json`) |
| `news.html` | News |
| `contact.html` | Contact |
| `styles.css` | Colors, fonts and layout for all pages |

## How to add a news item

1. Open `news.html` on GitHub and click the pencil icon.
2. Copy one `<article>` block and paste it above the newest item.
3. Change the date, the title and the text.
4. Click **Commit changes**, choose **Create a new branch**, then **Propose changes**.
5. Open the pull request and merge it (see below).

```html
<article class="card" style="margin-bottom:2rem;">
  <div class="kicker">10 June 2026</div>
  <h2>Title of the news item</h2>

  <p>
    Two or three sentences about the news.
  </p>
</article>
```

## How to update the team page

The Team page reads `team.json`. The script `tools/csv_to_json.py` builds that file from the sign-up form responses.

1. Export the form responses as a CSV file.
2. Save it in the `data/` folder, with the same file name as the CSV that is there now.
3. Run `python3 tools/csv_to_json.py`. It rewrites `team.json`, sorted by last name.
4. Commit the new `team.json`.

Do not edit `team.json` by hand. The script overwrites it the next time it runs.

## How to review and merge a pull request

A pull request (PR) is a proposed change. Nothing goes live until someone merges it.

1. Open the PR from the **Pull requests** tab.
2. Read the description and look at the before and after screenshots.
3. Click **Files changed** to see the exact lines that change.
4. To ask for a change, write a comment on the PR.
5. When you are happy, click **Merge pull request**, then **Confirm merge**.

To undo a merged PR, open it and click **Revert**. GitHub creates a new PR that undoes the change.
