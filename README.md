# Media Mister Panel

Static web page for the Media Mister panel. There is no build step and no dependencies.

## Project structure

```
media-mister-panel/
├── index.html         # Main page
├── design-system.md   # Design system reference
└── assets/
    ├── logo.svg
    ├── stack-bg.svg
    └── text-logo.svg
```

## Run locally

Open `index.html` in a browser, or serve the folder:

```bash
# Python
python -m http.server 8000

# or Node
npx serve .
```

Then visit http://localhost:8000.

## Push to Git

1. Create an empty repository on GitHub, GitLab or Bitbucket.
2. In the project folder, run:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

Later changes:

```bash
git add .
git commit -m "Describe your change"
git push
```

## Deploy

Because the site is static, any of these work. All deploy automatically on every push to `main`.

### GitHub Pages
1. Go to **Settings → Pages** in the repository.
2. Under **Build and deployment**, set **Source** to *Deploy from a branch*.
3. Choose branch `main` and folder `/ (root)`, then click **Save**.
4. The site goes live at `https://<your-username>.github.io/<your-repo>/` in a minute or two.

### Netlify
1. Click **Add new site → Import an existing project** and connect the repository.
2. Leave **Build command** empty and set **Publish directory** to `.`
3. Click **Deploy**.

### Vercel
1. Click **Add New → Project** and import the repository.
2. Set **Framework Preset** to *Other*. Leave the build command empty and the output directory as `.`
3. Click **Deploy**.

### Cloudflare Pages
1. Go to **Workers & Pages → Create → Pages → Connect to Git**.
2. Leave the build command empty and set the output directory to `/`.
3. Click **Save and Deploy**.

### Your own server (Nginx)
Copy the files to the web root:

```bash
scp -r index.html assets user@your-server:/var/www/media-mister-panel/
```

Example Nginx config:

```nginx
server {
    listen 80;
    server_name example.com;
    root /var/www/media-mister-panel;
    index index.html;
}
```

## Custom domain

Add the domain in your host's settings (for example **Settings → Pages → Custom domain** on GitHub Pages). Then create a `CNAME` record at your DNS provider pointing to the host's address.

## Troubleshooting

- **Images or logos missing:** asset paths are relative (`assets/...`). Keep the folder structure unchanged.
- **404 on GitHub Pages:** confirm the file is named `index.html` (lowercase) and sits at the repository root.
- **Changes not showing:** wait for the deploy to finish, then hard-refresh with `Ctrl+Shift+R`.
