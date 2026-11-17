# Space Array website

The public website of the Space Array Initiative: https://spacearray.org

The site is built with [Astro](https://astro.build). GitHub builds the site and publishes it after every merge to `main`, so nobody needs to run anything on their own computer. A merge goes live within a few minutes.

## Files

Each page is one file in `src/pages/`. The menu, the page head and the footer are in one shared file, `src/layouts/Layout.astro`. Change the menu there, and it changes on every page.

| File | Page |
| --- | --- |
| `src/pages/index.astro` | Home |
| `src/pages/science.astro` | Science |
| `src/pages/sharp.astro` | SHARP |
| `src/pages/technology.astro` | Technology |
| `src/pages/team.astro` | Team (the list comes from `public/team.json`) |
| `src/pages/news.astro` | News |
| `src/pages/contact.astro` | Contact |
| `src/layouts/Layout.astro` | Head, menu and footer for all pages |
| `public/styles.css` | Colors, fonts and layout for all pages |
| `public/images/` | Images |

Files in `public/` go online as they are. For example, `public/images/photo.jpg` is at `https://spacearray.org/images/photo.jpg`.

The page addresses did not change. `src/pages/news.astro` is still at `https://spacearray.org/news.html`.

## How to change the text on a page

1. Open the page's file in `src/pages/` on GitHub (see the table above) and click the pencil icon.
2. Change the text between `<main>` and `</main>`. It is normal HTML.
3. Click **Commit changes**, choose **Create a new branch**, then **Propose changes**.
4. Open the pull request and merge it (see below).

Each page file starts like this. Leave these lines as they are:

```astro
---
import Layout from "../layouts/Layout.astro";
---
<Layout title="Science · Space Array" active="science.html">
```

The last line of the file is `</Layout>`. Leave it as well.

**Curly brackets:** do not type `{` or `}` in the text. Astro reads them as code, and the build fails. Write `&#123;` for `{` and `&#125;` for `}`.

## How to add a page

A new page needs a file and a menu link.

1. Open a page in `src/pages/` on GitHub, for example `science.astro`, and copy all of its text.
2. Go to the `src/pages/` folder. Click **Add file**, then **Create new file**. Give it a short name, for example `events.astro`, and paste the text. Its address is then `https://spacearray.org/events.html`.
3. In the `<Layout ...>` line of the new file, change the title and set `active` to the new address:

   ```astro
   <Layout title="Events · Space Array" active="events.html">
   ```

4. Replace the text between `<main>` and `</main>`.
5. Click **Commit changes**, choose **Create a new branch**, then **Propose changes**.
6. Add the menu link in the same branch. On the repository page, switch the branch menu from `main` to your new branch. Open `src/layouts/Layout.astro` and click the pencil icon.
7. In the menu (`<nav>`), copy one link line and change it to the new page:

   ```astro
   <a class={active === "events.html" ? "active" : undefined} href={`${base}events.html`}>Events</a>
   ```

8. Click **Commit changes** and choose **Commit directly to** your branch. Then open the pull request and merge it.

The menu on every page now shows the link. The link is highlighted on the new page.

## How to add a news item

1. Open `src/pages/news.astro` on GitHub and click the pencil icon.
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

### Give a news item its own page

A news item with its own page shows a proper preview (title, summary and photo) when someone shares its link on LinkedIn, X, Slack or email. See `src/pages/news/simulation-working-group-sweden.astro` for an example.

1. Put the photo in `public/images/`. Also add a copy cropped to 1200 x 630 pixels for the preview.
2. Copy the example page in `src/pages/news/` and give the copy a short name, for example `my-news-item.astro`.
3. Change the title, the summary (`description`, under 160 characters), `path`, `image`, `imageAlt` and the text.
4. On the News page, link the item's title to `news/my-news-item.html`.
5. After the merge, share `https://spacearray.org/news/my-news-item.html`, not the News page.

## How to update the team page

The Team page reads `public/team.json`. The script `tools/csv_to_json.py` builds that file from the sign-up form responses.

1. Export the form responses as a CSV file.
2. Save it in the `data/` folder, with the same file name as the CSV that is there now.
3. Run `python3 tools/csv_to_json.py`. It rewrites `public/team.json`, sorted by last name.
4. Commit the new `public/team.json`.

Do not edit `public/team.json` by hand. The script overwrites it the next time it runs.

## How to review and merge a pull request

A pull request (PR) is a proposed change. Nothing goes live until someone merges it.

1. Open the PR from the **Pull requests** tab.
2. Read the description and look at the before and after screenshots.
3. Click **Files changed** to see the exact lines that change.
4. To ask for a change, write a comment on the PR.
5. When you are happy, click **Merge pull request**, then **Confirm merge**.

To undo a merged PR, open it and click **Revert**. GitHub creates a new PR that undoes the change.

## If the site does not update after a merge

After each merge, GitHub builds the site. Open the **Actions** tab to see the build.

- A green check means the build worked and the live site has the change.
- A red X means the build failed. The live site does not change. It keeps the last version that built.

To find the problem:

1. Click the failed run, then click **build**.
2. Look for `ERROR`. The lines near it name the page, for example `science.astro:19` (the file and line number) or `rendering /science`.
3. Fix it in a new PR. Or open the PR that caused it and click **Revert**.

Two common causes: a `{` or `}` in the text (see "How to change the text on a page"), or a deleted `</Layout>` line.

## Preview the site on your own computer

This is optional. You only need it to see a change before you open a PR.

1. Install [Node.js](https://nodejs.org) version 22.23.4 or later.
2. In the repository folder, run `npm ci` once. It installs Astro.
3. Run `npm run dev` and open http://localhost:4321 in a browser. When you save a file, the page updates.
4. Press **Ctrl+C** to stop it. If it started in the background, run `npx astro dev stop`.

To check that GitHub can build your change, run `npm run build`. It must end with `Complete!`. The built site is in `dist/`.

## License

- **Code** (HTML structure, CSS, scripts): MIT License. See [LICENSE](LICENSE).
- **Content** (text and images): Creative Commons Attribution 4.0 International (CC BY 4.0). See [LICENSE-CONTENT](LICENSE-CONTENT).

Images from other sources keep their own license. Their credit lines say where they come from.
