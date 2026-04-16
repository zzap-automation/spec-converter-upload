# Spec Header Converter — Zwicker Zareski Architecture

Updates header text across Word spec documents and exports PDFs. No logins, no installs — works in any browser.

**Live tool:** `https://zzap-automation.github.io/spec-converter/`

---

## How to use

1. Open the link above
2. Pick the submission status, date, and version
3. Drop in your .docx files (or click to browse)
4. Click Run
5. Download the zip of PDFs

---

## Repository structure

```
spec-converter/
  index.html        ← the front end (GitHub Pages)
  README.md
  backend/
    app.py          ← Python backend (Render.com)
    requirements.txt
    Dockerfile
```

---

## Setup — two parts

### Part 1: GitHub Pages (front end) — already done if you're reading this

The `index.html` file is served automatically by GitHub Pages at the URL above.

### Part 2: Render.com backend (one-time, ~10 minutes, free)

The backend runs Python + LibreOffice to do the actual PDF conversion.

1. Go to **render.com** and sign up free (use the automation@zzap.ca account)
2. Click **New → Web Service**
3. Connect your GitHub account and select the `zzap-automation/spec-converter` repository
4. Fill in:
   - **Name:** `spec-converter`
   - **Root directory:** `backend`
   - **Environment:** `Docker`
   - **Instance type:** Free
5. Click **Create Web Service**
6. Wait ~5 minutes for the first deploy (it installs LibreOffice)
7. Copy the URL Render gives you — it looks like `https://spec-converter-xxxx.onrender.com`
8. Open `index.html`, find this line near the bottom and replace the placeholder:
   ```javascript
   const BACKEND_URL = 'https://YOUR-APP-NAME.onrender.com/convert';
   ```
   Replace with your actual Render URL + `/convert`
9. Save and push `index.html` back to GitHub

The tool is now fully live.

---

## Updating the status options

Open `index.html` and find the pills section. Edit the button labels and values as needed:

```html
<button class="pill" onclick="setStatus(this,'Issued for Construction')">Issued for construction</button>
```

The text inside `setStatus(this,'...')` is what gets written into the document.

---

## Handing over to someone else

1. Add them as a collaborator: GitHub repo → Settings → Collaborators
2. Give them access to the Render.com account (render.com → Account → Team)
3. The tool URL never changes

---

## Free tier limits

- **GitHub Pages:** unlimited — no limits for static files
- **Render.com free tier:** 750 hours/month (enough for daily use), spins down after 15 min of inactivity — first request after idle takes ~30 seconds to wake up. Subsequent requests are instant.
