# The Cedar Ridge Regulator: setup guide

This is a plain website plus a free editing screen (Decap CMS) at `yourwebsite.com/admin`. Articles are saved as files in a GitHub repository, and Netlify publishes the site from that repository. Everything below is free.

You will need a free GitHub account and a free Netlify account. Setup takes about 30 minutes.

## What is in this folder

- `index.html`: the newspaper itself
- `admin/`: the Editor’s Desk (`config.yml` controls what it can edit)
- `content/articles.json`: all articles. The Editor’s Desk edits this for you.
- `content/site.json`: the newspaper name, tagline, footer and labels
- `images/`: uploaded photos

## Step 1: Put the files on GitHub

1. Sign in at github.com and click **New repository**. Name it (for example `cedar-ridge-regulator`) and create it.
2. Click **uploading an existing file**, then drag in everything from this folder (including the `admin`, `content` and `images` folders). Click **Commit changes**.
3. Open `admin/config.yml` on GitHub, click the pencil icon, and change the `repo:` line to `your-github-username/your-repo-name`. Commit the change.

## Step 2: Publish the site on Netlify

1. Sign in at netlify.com (using your GitHub account is easiest).
2. Click **Add new site**, then **Import an existing project**, and choose GitHub and your repository.
3. Leave the build command empty and the publish directory empty (or `.`), then click **Deploy**.
4. When it finishes you have a link like `something.netlify.app`. You can rename it under **Site configuration**, or add your own domain under **Domain management**.

## Step 3: Let the Editor’s Desk log in with GitHub

1. On GitHub, go to **Settings → Developer settings → OAuth Apps → New OAuth App**.
   - Homepage URL: your Netlify site address
   - Authorization callback URL: `https://api.netlify.com/auth/done`
2. Create the app, copy the **Client ID**, and click **Generate a new client secret**.
3. In Netlify, open your site and go to **Site configuration → Access & security → OAuth** (the menu wording may differ slightly), click **Install provider**, choose GitHub, and paste the Client ID and secret.

## Step 4: Write articles

1. Go to `yourwebsite.com/admin` and click **Login with GitHub**.
2. Open **Articles → All Articles**, click **Add Article**, fill in the form, and click **Publish**.
3. The new article appears on the site in about a minute.

The sample articles are placeholders, so delete them once you have real ones. **Site Text** in the same screen changes the masthead, tagline, footer and labels.

## Who can edit

Only people with a GitHub account who have **write access to your repository** can use the Editor’s Desk. Add them under the repository’s **Settings → Collaborators**. Readers of the site never see the editing screen.

To have student writers submit drafts that an editor approves first, remove the `#` from the `# publish_mode: editorial_workflow` line in `admin/config.yml`. Drafts then appear in a **Workflow** tab.

## Adding a new section

Add the name to the `options:` list for Section in `admin/config.yml`. It then appears in the site’s menu once an article uses it. To control where it appears in the menu, also add it to the `ORDER` list near the top of the script in `index.html`.

## Trying it on your own computer

Opening `index.html` directly will not work because the page needs to read the content files. Run `python3 -m http.server` in this folder and open `http://localhost:8000`.
