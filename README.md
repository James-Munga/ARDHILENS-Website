# ArdhiLens Website

ArdhiLens is a multi-page website introducing the organisation's geospatial services, team, contact information, and mapping projects. It is built with plain HTML, CSS, and JavaScript and can be previewed locally without a build step.

## Contents

- `home.html` â€” home page and shared site interactions.
- `services.html` â€” geospatial services.
- `projects.html` â€” project map and project statistics.
- `about.html` â€” organisation, team, and partners.
- `contacts.html` â€” contact information and enquiry form.
- `home.css`, `services.css`, `projects.css`, `about.css`, `contacts.css` â€” page styles. The secondary pages also load `home.css` for shared styling.
- `home.js` â€” shared navigation, page effects, and newsletter interactions. The contact form integration is loaded by `contacts.html`.
- `projects.js` â€” project map and GeoJSON loading.
- `Images/` and `Video/` â€” local page media.
- `Data/` â€” GeoJSON used by the project map and supporting geospatial data.

## Requirements

- A modern web browser.
- Git, if you plan to publish changes to GitHub.
- A local static web server to preview the map and other features that load local data files. For example, if Python is installed, run `python -m http.server 8000` from the project folder and open `http://localhost:8000/home.html`. You can also use the Live Server extension in Visual Studio Code.

Opening the HTML files directly with a `file://` URL may prevent the browser from loading GeoJSON or other local resources. Use a local server for a representative preview.

## Preview the site

1. Open this project folder in Visual Studio Code or another editor.
2. Start a static local server from the project root.
3. Visit `http://localhost:8000/home.html` to open the home page.
4. Use the navigation to visit `services.html`, `projects.html`, `about.html`, and `contacts.html`.

The projects page loads `Data/ARDHILENS_Projects_Geocoded.geojson` and `Data/KenyaCounties.geojson`. It uses Leaflet from a public CDN. Fonts, Font Awesome icons, and the EmailJS browser library are also loaded from external CDNs, so those features need an internet connection.

## Push changes to GitHub

The configured remote for this checkout is `origin`. These instructions assume your GitHub account has permission to push to that repository. Run the commands below in a terminal opened at the project root.

### 1. Check the repository and pending changes

```bash
git status
git remote -v
git branch --show-current
```

Confirm that `origin` points to the intended GitHub repository and that you are working on the branch you intend to publish. If this is a new local project without a Git repository, initialize it and add the remote first:

```bash
git init
git branch -M main
git remote add origin https://github.com/ACCOUNT/REPOSITORY.git
```

Replace `ACCOUNT` and `REPOSITORY` with the correct GitHub owner and repository name. Do not run `git init` or add a second `origin` when working in the existing checkout.

### 2. Review and stage the intended files

Review the changes before staging. Stage all intended project changes with:

```bash
git add README.md home.html home.css home.js services.html services.css projects.html projects.css projects.js about.html about.css contacts.html contacts.css Images Data Video
```

Or stage only selected files by listing their paths instead. Check exactly what is staged:

```bash
git status
git diff --cached --stat
git diff --cached
```

The media and county GeoJSON files can make a push large. Keep the assets required by the site, and avoid staging unrelated exports, credentials, or temporary files.

### 3. Commit the changes

```bash
git commit -m "Describe the website update"
```

Use a short message that describes the change, such as `Document GitHub publishing steps`.

### 4. Push the branch to GitHub

For the `main` branch:

```bash
git push -u origin main
```

For a different branch, replace `main` with the branch shown by `git branch --show-current`. The `-u` option records the upstream the first time you push that branch. Later pushes from the same branch can use:

```bash
git push
```

If GitHub requests authentication, use Git Credential Manager, GitHub CLI authentication, or an SSH remote configured for your account. GitHub no longer accepts account passwords for HTTPS Git operations. If Git reports that the remote contains work you do not have locally, fetch and review those commits before integrating them; do not force-push over remote history you need.

## Publish with GitHub Pages

GitHub Pages can host this static site. The repository currently uses `home.html` as the home page filename; a Pages site expects an `index.html` file at its published root. Before publishing, add an `index.html` entry page (for example, a copy of `home.html`) so the site root opens correctly. Keep it in sync when the home page changes. The existing `home.html` URL will also remain available.

1. Push the site files to GitHub using the steps above.
2. Open the repository on GitHub and go to **Settings â†’ Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select the branch you pushed (usually `main`) and the `/ (root)` folder, then save.
5. Wait for the Pages deployment to finish. GitHub will show the published address on the Pages settings screen.
6. Open the published site and check the navigation, images, videos, project map, and contact form.

Pages serves the site over HTTPS. If a map or media item fails after deployment, check that the referenced file is committed and that the file name and letter case in each HTML/JavaScript path exactly match the repository. GitHub Pages paths are case-sensitive.

## External services and configuration

- **Leaflet:** The project map loads Leaflet CSS and JavaScript from `unpkg.com`.
- **Fonts and icons:** Google Fonts and Font Awesome load from their public CDNs.
- **Contact form:** `contacts.html` loads EmailJS from jsDelivr. Review the EmailJS configuration in the contact page before using the form on a live site. Keep private service credentials out of a public repository; only publish browser-safe public identifiers intended for client-side use.
- **Newsletter:** The newsletter form is a front-end interaction. Connect it to a mailing-list provider before relying on it to collect subscriptions.

## Troubleshooting

- **A page or image is missing:** Check the path spelling and capitalization, and confirm the asset is committed.
- **The project map is blank:** Run the site from a local server or check the deployed browser console for a failed GeoJSON request. Confirm both files in `Data/` are present.
- **The site root returns a not-found page:** Add and push the root `index.html` entry page described in the GitHub Pages section.
- **`git push` is rejected:** Check your authentication and permissions, then fetch and inspect remote changes before integrating them.

## License and data

No software license is currently included. Add a `LICENSE` file if you want to grant others explicit reuse rights. Confirm that you have permission to publish the included photography, video, logos, project data, and county boundary data before distributing the repository or deploying it publicly.
