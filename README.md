# Racks Resale Management System

🎥 [Demo Video](https://www.youtube.com/shorts/rw_uApxBhhw)

A comprehensive inventory management system for resale businesses with AI-powered price detection using Google's Gemini API.

## Features

- 📸 Photo management (up to 5 photos per item)
- 🤖 **AI Scan** - Automatically detect prices and item types from photos
- 💰 Sales tracking and profit calculation
- 📊 Analytics dashboard
- 🎯 Auto-pricing with configurable markup
- 📦 Bulk import from CSV
- 🔍 Advanced filtering and search
- 📱 Mobile-friendly camera capture
- 💾 Local storage (no server required)

## AI Scan Feature

The AI Scan feature uses Google's Gemini 2.5 Flash model to:
- Extract prices from photo tags
- Identify clothing/item types
- Auto-fill item details

## Deployment

See [DEPLOYMENT.md](DEPLOYMENT.md) for detailed deployment instructions.

### Quick Start (Vercel)

1. Push code to GitHub
2. Import to Vercel
3. Add `GEMINI_API_KEY` environment variable
4. Deploy!

Your users can now use AI Scan without needing their own API keys.

## Local Development

1. Get a Gemini API key from https://aistudio.google.com/app/apikey
2. Set it as environment variable:
   ```bash
   export GEMINI_API_KEY=your_key_here
   ```
3. Install Vercel CLI:
   ```bash
   npm install -g vercel
   ```
4. Run local dev server:
   ```bash
   vercel dev
   ```
5. Open http://localhost:3000

## Tech Stack

- **Frontend**: Vanilla JavaScript, Alpine.js
- **Storage**: Browser localStorage
- **AI**: Google Gemini 2.5 Flash
- **Deployment**: Vercel Serverless Functions
- **Styling**: Custom CSS with responsive design

## Security

- API key is never exposed to clients
- Requests are proxied through serverless function
- No database - all data stays in user's browser

## License

MIT
