# Image Quality Enhancement — Website Setup

This project has 2 parts:

- `backend/` — a small Python server. It receives an image and sends back an "enhanced" one.
  Right now it fakes the enhancement (simple upscale) so everything works today.
- `frontend/` — one HTML file. This is the actual webpage people will see and use.

You do NOT need to touch the frontend again after today. Later, your team only
edits ONE function inside `backend/main.py` (called `enhance_image`) to plug in
your real trained model.

---

## STEP 1 — Run it on your own computer first (to test)

### 1a. Run the backend

Open a terminal in the `backend/` folder and run:

```
pip install -r requirements.txt
uvicorn main:app --reload
```

If it works, you'll see something like `Uvicorn running on http://127.0.0.1:8000`.
Leave this terminal open — this is your server running.

### 1b. Open the frontend

Just double-click `frontend/index.html` — it opens in your browser.
(No installation needed, it's a plain HTML file.)

Upload an image, click "Enhance Image" — you should see a bigger version appear
on the right. If you see that, the whole pipeline works.

---

## STEP 2 — Put it online (so you have a real URL to share)

You need to host 2 things separately:

### 2a. Host the backend (the Python server)

Use **Render.com** (free tier works fine):
1. Create a free account at render.com
2. Click "New Web Service"
3. Connect your GitHub repo (put the `backend/` folder in a GitHub repo first)
4. Set the start command to: `uvicorn main:app --host 0.0.0.0 --port 10000`
5. Deploy. Render will give you a URL like `https://your-app.onrender.com`

### 2b. Host the frontend (the webpage)

Use **GitHub Pages** or **Vercel** — both free and simple for a single HTML file:
- Easiest: create a GitHub repo with just `index.html` in it, then turn on
  "GitHub Pages" in the repo settings. You'll instantly get a public URL.

### 2c. Connect them

Open `frontend/index.html`, find this line near the top:

```js
const BACKEND_URL = "http://localhost:8000";
```

Change it to your real backend URL from step 2a, for example:

```js
const BACKEND_URL = "https://your-app.onrender.com";
```

Save, re-upload to GitHub Pages. Now your public URL fully works.

---

## STEP 3 — Later, when your model is trained

Open `backend/main.py`. Find the function called `enhance_image`.
Replace the placeholder code inside it with your model's real prediction code.
Nothing else needs to change — not the frontend, not the deployment, nothing.

---

## Quick summary of what each teammate can own

- Whoever finishes the model → edits `enhance_image()` in `backend/main.py`
- Whoever wants to make the page look nicer → edits `frontend/index.html`
- Anyone can redeploy by just pushing updated files to GitHub
