# Deploying Racks with AI Scan Feature

This guide will help you deploy your app to Vercel with the AI Scan feature working for all users.

## Prerequisites

- A Gemini API key (get one from https://aistudio.google.com/app/apikey)
- A GitHub account
- A Vercel account (free)

## Step 1: Push Your Code to GitHub

```bash
git add .
git commit -m "Add Gemini proxy endpoint"
git push origin main
```

## Step 2: Deploy to Vercel

1. Go to https://vercel.com and sign in
2. Click "Add New Project"
3. Import your GitHub repository
4. Click "Deploy" (it will fail first time - that's OK!)

## Step 3: Add Environment Variable

1. In your Vercel project dashboard, go to **Settings** → **Environment Variables**
2. Add a new variable:
   - **Name**: `GEMINI_API_KEY`
   - **Value**: Your Gemini API key (AIzaSyCNyyywYrdI16RKhZr3WcHW5FckXF7TP5Q)
   - **Environment**: Check all (Production, Preview, Development)
3. Click "Save"

## Step 4: Redeploy

1. Go to **Deployments** tab
2. Click the "..." menu on the latest deployment
3. Click "Redeploy"
4. Wait for deployment to complete

## Step 5: Test

1. Visit your deployed URL (e.g., `your-app.vercel.app`)
2. Add an item with a photo
3. Click "AI Scan" - it should work! 🎉

## How It Works

- Your API key is stored securely in Vercel's environment variables
- The `/api/gemini-proxy` endpoint acts as a middleman
- Users never see or need your API key
- All AI Scan requests go through your proxy

## Rate Limiting (Optional)

To prevent abuse, you can add rate limiting to the proxy:

```javascript
// Add to api/gemini-proxy.js
const rateLimit = new Map();

// Check rate limit (max 10 requests per minute per IP)
const ip = req.headers['x-forwarded-for'] || req.connection.remoteAddress;
const now = Date.now();
const userRequests = rateLimit.get(ip) || [];
const recentRequests = userRequests.filter(time => now - time < 60000);

if (recentRequests.length >= 10) {
  return res.status(429).json({ error: 'Too many requests' });
}

recentRequests.push(now);
rateLimit.set(ip, recentRequests);
```

## Costs

- Vercel: Free for personal projects (up to 100GB bandwidth/month)
- Gemini API: Free tier includes generous limits
  - 1,500 requests per day
  - 1M tokens per minute

## Troubleshooting

### "API key not configured" error
- Make sure you added the environment variable
- Redeploy after adding the variable

### 403 Forbidden error
- Your API key may be invalid or leaked
- Generate a new key and update the environment variable

### Function timeout
- Increase timeout in `vercel.json` (max 60s on free tier)

