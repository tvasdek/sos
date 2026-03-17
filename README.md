# 🔴 SOS Panic Button

A free, open-source emergency panic button installable as a mobile app through Chrome — no app store needed. One press sends an automatic distress message with GPS location to a Telegram group of your choice.

Built for elderly and vulnerable people. Requires zero technical knowledge to use.

**[▶ Live Demo — open on mobile](https://tvasdek.github.io/sos/)**

---

## Why This Exists

My 74-year-old mother was targeted by two individuals as part of a con. They shocked her, threatened her, and convinced her that her life was in danger — even had someone pretend to be a police officer there to "help" her. Frightened and confused, she handed over a large amount of money and personal jewellery.

I built this so it never happens again. To her, or to anyone like her.

---

## How It Works

1. Press the big red **SOS** button
2. A **5-second countdown** begins — tap Cancel if it was a mistake
3. If not cancelled, a **pre-written distress message fires automatically** to your Telegram group
4. If GPS is available, the message includes a **Google Maps link** with the exact location
5. A **one-tap call button** appears — to 112 or any number you set

The person pressing the button does not need Telegram installed. They just need Chrome and internet.

---

## Features

- ✅ One-button operation — designed for elderly users
- ✅ 5-second cancellable countdown (prevents accidental triggers)
- ✅ Automatic Telegram group alert — no tapping through menus
- ✅ GPS location included in the message as a Google Maps link
- ✅ Falls back gracefully if GPS is unavailable
- ✅ Quick-call button if no internet is available
- ✅ Fully configurable via in-app settings — no code editing needed
- ✅ All data stored locally on the device — no servers, no accounts, no subscriptions
- ✅ Installable as a home screen app via Chrome (PWA)
- ✅ Works on any Android phone with Chrome
- ✅ Free forever — open source

---

## Installation (for the user's phone)

### Step 1 — Open the app in Chrome
On the phone that will use the panic button, open Chrome and go to:
```
https://tvasdek.github.io/sos/
```

### Step 2 — Install to Home Screen
- Tap the **three dots menu** (⋮) in Chrome
- Tap **"Add to Home Screen"** (or "Install App")
- Tap **Install**

The red SOS icon will appear on the home screen like a regular app.

> **Note:** The "Add to Home Screen" option only appears when opening via a web URL — not from a local file. This is why the app needs to be hosted online.

---

## Setup — Telegram Bot & Group

The app uses a Telegram bot to send alerts. You set this up once. The person using the panic button does **not** need Telegram.

### Step 1 — Create a Telegram Bot

1. Open Telegram and search for **@BotFather**
2. Tap **Start**
3. Send: `/newbot`
4. Choose a name (e.g. `Mama SOS Alert`)
5. Choose a username ending in `bot` (e.g. `mama_sos_alert_bot`)
6. BotFather will reply with a **Token** — copy it. It looks like:
   ```
   YOUR_BOT_TOKEN_HERE
   ```

### Step 2 — Create a Telegram Group

1. Create a new Telegram group
2. Name it something clear (e.g. `🆘 SOS Alerts`)
3. Add all family members or people who should receive alerts
4. Add your bot to the group
5. Make the bot an **Admin** of the group (required so it can post messages)

### Step 3 — Get the Group Chat ID

1. Send any message in the group (e.g. "test")
2. Open a browser and go to:
   ```
   https://api.telegram.org/bot<YOUR_TOKEN>/getUpdates
   ```
   Replace `<YOUR_TOKEN>` with the token from Step 1
3. Look for `"chat":{"id":` in the response — the number after it is your Chat ID
4. It will look like: `-1001234567890` (always starts with `-100` for groups)

### Step 4 — Enter Settings in the App

1. Open the app and tap the **⚙️ gear icon** (bottom right)
2. Enter your **Bot Token** (Step 1)
3. Enter your **Chat ID** (Step 3)
4. Write your **distress message** (e.g. "🆘 I need help immediately!")
5. Enter a **quick-call number** (e.g. a family member's number or `112`)
6. Tap **📡 Test Connection** — a test message should appear in your Telegram group
7. Tap **✓ Save**

---

## What the Telegram Message Looks Like

```
🆘 I need help immediately!

📍 https://maps.google.com/?q=37.984123,23.727821
🕐 14:32
```

If GPS is not available:
```
🆘 I need help immediately!

📍 Θέση άγνωστη (χωρίς GPS)
🕐 14:32
```

---

## Hosting Your Own Version

You can fork this repo and host your own version for free.

### Option A — GitHub Pages
1. Fork this repo
2. Go to **Settings → Pages**
3. Set source to **main branch / root**
4. Your app will be live at `https://yourusername.github.io/sos/`

> **Important:** GitHub Pages requires a **public** repo on free accounts. If you want the repo private, use Netlify.

### Option B — Netlify (free, supports private repos)
1. Go to [netlify.com](https://netlify.com)
2. Drag and drop the `index.html` file onto the Netlify dashboard
3. You get an instant permanent URL

---

## Security

**Bot Token exposure:** The bot token is stored in the device's local storage (entered via settings). It is never sent anywhere except to Telegram's official API. The token can only be used to send messages to your specific group — it cannot access your Telegram account or any other data.

**GPS data:** Location is only accessed when the SOS button is triggered and is only sent to your Telegram group via Telegram's API. It is never stored or sent anywhere else.

**No backend:** This app has no server. There is no database, no user accounts, no analytics, and no data collection of any kind. Everything runs entirely in the browser.

---

## FAQ

**Does the person using the app need Telegram?**
No. They only need Chrome and an internet connection. Telegram is only needed by the people receiving the alerts.

**Does it work without internet?**
The Telegram message requires internet. Without internet, the app shows a quick-call button to dial a pre-set number (like 112 or a family member) directly.

**What if GPS is turned off or unavailable?**
The message is still sent — it just includes "location unknown" instead of a map link. The app does not block on GPS.

**Can I use it for someone who speaks a different language?**
Yes — just write the distress message in any language via the settings panel.

**Can multiple people have the app set up to send to the same group?**
Yes. Each person sets up the app with the same bot token and chat ID, and all alerts go to the same group.

**What Android version is required?**
Any Android phone with Chrome installed. Tested on Android 10+. Should work on Android 8+.

**Does it work on iPhone?**
The app works in Safari on iOS. However, iOS has stricter PWA support and the "Add to Home Screen" experience may differ slightly. Core functionality (sending Telegram alert + GPS) works the same.

**Can I change the countdown from 5 seconds?**
Not via the settings panel currently — but it's a one-line change in the source code (`countdownValue = 5`).

**What happens if the Telegram message fails to send?**
An error screen appears with a Retry button and a direct call button, so the user is never left without options.

**Is this really free?**
Yes. Telegram bots are free. GitHub Pages is free. The app itself is free. No subscriptions, ever.

---

## Contributing

Pull requests are welcome. Some ideas for expansion:

- [ ] SMS fallback via Twilio or similar (for areas with no data but SMS coverage)
- [ ] Multiple alert contacts without Telegram (email via EmailJS)
- [ ] Periodic "I'm OK" check-in with auto-alert if missed
- [ ] iOS-optimized PWA manifest
- [ ] Multi-language UI

---

## License

MIT — free to use, modify, and distribute. If you build something useful on top of this, please share it back.

---

*Built with Claude by [Theo Vasdekis](https://github.com/tvasdek) — because our people deserve to feel safe.*
