# Telegram Mini App - Deployment Guide

## What is this?

This is a Telegram Web App (Mini App) that provides a visual interface for users to set their apartment search filters.

## Features

- 🎨 Modern dark-mode UI with Tailwind CSS
- 💰 Price range slider (₪3K - ₪25K)
- 🛏 Room count selector (1-4+)
- 🚫 Private owners only toggle
- 📱 Full Telegram integration

## How to Deploy on GitHub Pages

### Step 1: Create a GitHub Repository

1. Go to [GitHub](https://github.com/new)
2. Create a new repository (e.g., `yad2-bot-webapp`)
3. Make it **Public** (required for GitHub Pages)

### Step 2: Upload the File

1. Upload `index.html` to your repository
2. Go to **Settings** → **Pages**
3. Under "Source", select **Deploy from a branch**
4. Select branch: **main** and folder: **/ (root)**
5. Click **Save**

### Step 3: Get Your URL

After a few minutes, your app will be available at:
```
https://YOUR_USERNAME.github.io/yad2-bot-webapp/index.html
```

Example:
```
https://johndoe.github.io/yad2-bot-webapp/index.html
```

### Step 4: Configure in BotFather

1. Open [@BotFather](https://t.me/BotFather) in Telegram
2. Send `/mybots`
3. Select your bot
4. Click **Bot Settings** → **Menu Button**
5. Choose **Edit Menu Button URL**
6. Paste your GitHub Pages URL
7. Set button text: "🔧 Set Filters"

## Alternative: Host Anywhere

You can host this HTML file anywhere that supports HTTPS:
- GitHub Pages ✅ (Free, easiest)
- Vercel
- Netlify
- Your own server

The only requirement is **HTTPS** - Telegram Web Apps don't work over HTTP.

## Testing Locally

You cannot test Telegram Web Apps locally (localhost) because Telegram requires HTTPS.

To test:
1. Deploy to GitHub Pages first
2. Open your bot in Telegram
3. Click the menu button
4. The Web App should open

## How It Works

1. User opens the Web App from Telegram bot menu
2. User adjusts filters (price, rooms, private only)
3. User clicks "Save Filters 🔔"
4. Data is sent back to the bot via `Telegram.WebApp.sendData()`
5. Bot receives the data in `handlers_webapp.py`
6. Filters are saved to the database
7. User starts receiving notifications!

## Customization

### Change Price Range
Edit `index.html` line 68-72:
```html
<input
    type="range"
    id="maxPrice"
    min="3000"   <!-- Minimum price -->
    max="25000"  <!-- Maximum price -->
    step="500"   <!-- Price increment -->
    value="10000" <!-- Default value -->
/>
```

### Change Room Options
Edit `index.html` lines 80-92 to add/remove room options.

### Change Colors
The app uses Tailwind CSS. Key classes:
- `bg-gray-900` - Dark background
- `bg-gray-800` - Card background
- `bg-blue-600` - Accent color
- `text-white` - Text color

## Troubleshooting

### Web App doesn't open
- Make sure URL is HTTPS
- Check that the file is named `index.html`
- Verify GitHub Pages is enabled in repository settings

### Data not saving
- Check bot logs for errors
- Verify `handlers_webapp.py` is imported in `main_final.py`
- Make sure bot is running

### UI looks broken
- Clear browser cache
- Check that Tailwind CSS CDN is loading
- Open browser console (F12) to check for errors

## Support

If you have issues, check:
1. GitHub Pages is enabled and deployed
2. URL in BotFather is correct (with `https://`)
3. Bot is running and handlers are registered
4. Database has `users` table with `filters` column
