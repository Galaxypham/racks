# GitHub Pages + Vercel Proxy Setup

This guide shows you how to keep your app on **GitHub Pages** (free static hosting) while using **Vercel** only for the AI Scan proxy (also free).

## Benefits of This Setup

✅ **GitHub Pages**: Hosts your entire app for free  
✅ **Vercel**: Only hosts the tiny proxy function  
✅ **Your URL stays the same**: `https://galaxypham.github.io/racks/`  
✅ **AI Scan works for all users**: No API key needed!  

## Architecture

```
GitHub Pages (Your App)
    ↓ User clicks "AI Scan"
    ↓
Vercel Proxy (Your Serverless Function)
    ↓ Forwards request with hidden API key
    ↓
Google Gemini API
    ↓ Returns price detection
    ↓
Back to User
```

## Setup Steps

### Step 1: Deploy Proxy to Vercel

1. Go to https://vercel.com and sign in
2. Click **"Add New Project"**
3. Import your `racks` repository
4. Click **"Deploy"**
5. Note your Vercel URL (e.g., `racks-abc123.vercel.app`)

### Step 2: Add API Key to Vercel

1. In Vercel project → **Settings** → **Environment Variables**
2. Add:
   - **Name**: `GEMINI_API_KEY`
   - **Value**: `AIzaSyCNyyywYrdI16RKhZr3WcHW5FckXF7TP5Q`
   - Check **all environments**
3. Click **"Save"**
4. Go to **Deployments** → Redeploy

### Step 3: Update Your GitHub Pages App

1. Open `index.html` in your code
2. Find line ~14818 that says:
   ```javascript
   ? 'https://your-vercel-app.vercel.app/api/gemini-proxy'
   ```
3. Replace `your-vercel-app` with your actual Vercel URL
4. Example:
   ```javascript
   ? 'https://racks-abc123.vercel.app/api/gemini-proxy'
   ```

### Step 4: Push to GitHub

```bash
git add index.html api/gemini-proxy.js
git commit -m "Update proxy URL for GitHub Pages deployment"
git push origin main
```

### Step 5: Test It!

1. Visit: https://galaxypham.github.io/racks/
2. Add an item with a photo
3. Click **"AI Scan"**
4. It should work! 🎉

## Troubleshooting

### CORS Error
If you see "CORS policy" error:
- Make sure you deployed the updated `api/gemini-proxy.js` to Vercel
- The proxy includes your GitHub Pages URL in allowed origins

### 404 Error on Proxy
- Double-check your Vercel URL in `index.html`
- Make sure it ends with `/api/gemini-proxy`
- Verify the function deployed correctly in Vercel dashboard

### API Key Not Working
- Generate a new API key (the shared one might be flagged)
- Update it in Vercel environment variables
- Redeploy on Vercel

## Costs

- **GitHub Pages**: FREE ✨
- **Vercel Functions**: FREE (100GB bandwidth/month) ✨
- **Gemini API**: FREE (1,500 requests/day) ✨

**Total Cost: $0 per month!** 🎊

## How It Works

1. User visits your GitHub Pages site
2. User clicks "AI Scan"
3. JavaScript detects it's on GitHub Pages
4. Sends request to your Vercel proxy URL
5. Vercel proxy adds your API key (hidden)
6. Forwards to Gemini API
7. Gets response and sends back to user
8. User sees the results!

Your API key never leaves the Vercel server. Users never see it. Perfect! 🔒

