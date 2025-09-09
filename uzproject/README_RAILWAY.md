# Railway Deploy Guide

## 1) Create a project
- Go to https://railway.app and create/sign in to your account.
- Click **New Project** → **Deploy from GitHub** (recommended) or **New Service** → **Deploy from Repository**.
- If you do not use GitHub, you can **Upload** this prepared ZIP directly.

## 2) Add this code
- If using GitHub: push the project and connect the repo.
- If uploading: upload the ZIP after unzipping it locally.

## 3) Configure variables (Telegram bot & DB)
Set environment variables in Railway → **Variables**. Typical keys:
- `BOT_TOKEN` (Telegram)
- `WEBHOOK_URL` (your Railway domain + Telegram endpoint)
- `DATABASE_URL` (if using Postgres/Redis; create a Railway DB plugin then copy the URL)
- Any other variables your app requires

## 4) Deploy
- Railway will detect the `Dockerfile` and build the image.
- Start command is set in `Procfile`:  
  `node index.js`

If your stack is a web server, bind to `0.0.0.0:$PORT`.
If it is a bot without HTTP, consider adding a small health web server or use a **Background Worker** service instead of **Web**.

## 5) Telegram webhook (if applicable)
- After the service is running and has a domain like `https://your-service.up.railway.app`, call Telegram's `setWebhook` with your token and route:
  `https://api.telegram.org/bot<token>/setWebhook?url=https://your-service.up.railway.app/<your-webhook-path>`

## Notes
- This package includes: `Dockerfile`, `Procfile`, `railway.toml`.
- Adjust `node index.js` if your entry point differs.
