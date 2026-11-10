# 🤖 Streamly — TikTok Downloader Bot

A premium Telegram bot for downloading TikTok videos (MP4) and audio (MP3) with a colorful, multi-language (Bangla/English) interface.

## ✨ Features

- 🎬 HD TikTok video download (no watermark)
- 🎵 MP3 audio extraction
- 🌐 Bangla + English
- 👑 Contact Owner (opens URL)
- 🛠 Admin panel: users, ban, stats, broadcast, owner-link
- 💾 Persistent storage (JSON file)
- 🔁 Dual API (TikWM → SnapTik fallback)

## 🚀 Deploy on Render

### 1. Create the bot

1. Open [@BotFather](https://t.me/BotFather) on Telegram
2. `/newbot` → set name & username
3. Copy the **token** (looks like `123456:ABC...`)
4. Set a **profile picture** via `/setuserpic`

### 2. Get your admin user ID

- Message [@userinfobot](https://t.me/userinfobot) → copy your numeric ID

### 3. Push to GitHub

Create a new repo and upload these 4 files:

```
bot.py
requirements.txt
render.yaml
README.md
```

### 4. Deploy on Render

1. Go to [render.com](https://render.com) → **New → Blueprint**
2. Connect your GitHub repo
3. Render reads `render.yaml` automatically
4. Fill in the **environment variables**:

   | Key | Value |
   |-----|-------|
   | `TOKEN` | `123456:ABC...` (from BotFather) |
   | `ADMIN_ID` | `123456789` (your ID, comma-separated for many) |
   | `BOT_USERNAME` | `my_streamly_bot` (without `@`) |

5. Click **Apply** — done! 🎉

### 5. First-time setup

1. Message your bot: `/start`
2. Send `/admin` (only works for `ADMIN_ID`)
3. Tap **🔗 OWNER LINK** → send your contact URL (e.g. `https://t.me/yourusername`)
4. Done! Users tapping **👑 CONTACT OWNER** will now see a clickable URL button.

## ⚠️ Important Notes

- **Bot profile picture:** Set one via BotFather (`/setuserpic`) so `/start` shows it above the welcome text.
- **Button colors:** Telegram Bot API does **not officially support colors** on ReplyKeyboard buttons. This bot sends a `style` field (primary/success/danger) — some Telegram clients display colors, others show them normal. Buttons always work regardless.
- **Free tier sleep:** The bot pings itself via `/healthz` every 10–13 minutes to stay awake on Render's free plan. Set `KEEP_ALIVE_URL` only if you deploy on a non-Render host.
- **Data persistence:** `streamly_data.json` is created next to `bot.py`. On Render's free tier, it **resets on restart**. For true persistence, upgrade or use a database.
- **50 MB limit:** Telegram's Bot API caps uploads at 50 MB. Larger files are rejected with a friendly message.

## 🧩 File map

```
bot.py           → Full bot source (~1000 lines)
requirements.txt → Empty (stdlib only)
render.yaml      → Render deployment config
README.md        → This file
```

## 🛠 Changing language default

In `bot.py`, change:

```python
def get_lang(chat_id): return LANG.get(chat_id, "en")
#                                       ^^^
#                                       "en" → "bn" for Bangla default
```