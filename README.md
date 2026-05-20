# 🕌 Namaz Tracker — Elite Prayer Tracker

A mobile-first Progressive Web App (PWA) for tracking daily Islamic prayers, viewing accurate prayer timetables, reading Quran Surahs, and syncing data to the cloud via Firebase.

Built by **Type01warrior**.

---

## ✨ Features

### 🕐 Today Tab (Live)
- Real-time **countdown timer** to the next prayer
- **Precision timer** showing time since the current prayer began
- Toggle checkboxes to **mark each prayer as done** (Tahajjud, Sehri, Fajr, Zohr, Asr, Maghrib, Isha)
- Highlights the **currently active prayer row**
- Optional **Keep Screen Awake** toggle (Wake Lock API)

### 📅 Namaz Times Tab
- Full monthly **prayer timetable** displayed in a scrollable table
- Shows accurate times for all prayers across the month
- Highlights today's row for quick reference

### 📊 Dashboard Tab
- Monthly **prayer record table** with ✓/✗ marks per prayer per day
- **Score percentage** calculated per day (out of 6 prayers)
- **Performance dashboard** with 4 pie charts:
  - Daily score
  - Weekly average
  - Monthly average
  - Yearly average
- Month selector dropdown to browse historical records
- **Export to HTML report** — generates a printable prayer record for any date range (downloads via browser or Android bridge)

### 📖 Surah Tab
- Browse and read all **114 Surahs** of the Quran
- Each verse displayed with:
  - Arabic text (Noto Naskh Arabic font)
  - Transliteration
  - English translation
- **Font size controls** (A- / A+) for comfortable reading
- Keep Screen Awake toggle for uninterrupted reading

### ☁️ Cloud Sync (Firebase)
- **Real-time sync** across multiple devices via Firestore
- Manual sync button with animated indicator
- Auto-sync on prayer marking
- Supports sign-in / sign-out from the settings panel

### 🎨 Themes & Appearance
- **19 color themes**: Royal, Robotic, Material, Glass, Luxury, Void, Steel, Nebula, Ocean, Sunset, Monochrome, Amethyst, Matrix, Obsidian, Goldite, Midnight, Volcano, Abyss, Sahara
- **Light / Dark mode** toggle
- Theme and mode preferences persisted in `localStorage`

### 📱 Mobile UX
- Swipe left/right to navigate between tabs
- Safe-area insets for notched phones
- No white flash on load (dark background set at `html` level)
- Tap feedback on all interactive elements

---

## 📁 File Structure

```
├── index.html       # Main app (prayer tracker, dashboard, Surah reader)
├── login.html       # Authentication screen (Sign In / Sign Up)
├── icon.png         # Login screen logo
├── 55340.png        # App brand icon (shown in top bar)
├── manifest.json    # PWA manifest for installability
```

---

## 🔐 Authentication (`login.html`)

- Email/password **Sign In** and **Sign Up** with Firebase Auth
- **Forgot Password** sends a reset email
- Password visibility toggle (eye icon)
- Auto-redirects to `index.html` if already logged in (no double screen)
- **Skip for now** option to use the app without an account
- Android WebView bridge support (`AndroidBridge.goToMain()`)
- Fixed: dark background from first paint, no autofill yellow flash, real `<input>` elements for MIUI/Android compatibility

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML, CSS, JavaScript |
| Auth & Database | Firebase Authentication + Firestore (v8 SDK) |
| Fonts | Google Fonts (Lexend, Noto Naskh Arabic, Bangers, Teko, Press Start 2P) |
| Icons | Font Awesome 6 |
| PWA | Web App Manifest, Wake Lock API |
| Android | WebView with `AndroidBridge` JS interface |

---

## 🚀 Getting Started

### Web (Browser)
1. Clone or download the project files.
2. Open `login.html` in a browser — or set it as the entry point on your server.
3. Sign in or skip to use the app locally (prayer data stored in `localStorage`).
4. Sign in with an account to enable cloud sync across devices.

### Android WebView (Native Wrapper)
The app communicates with the native layer via a JavaScript bridge:
```javascript
window.AndroidBridge.goToMain();       // Navigate to main screen
window.AndroidBridge.downloadFile(html, filename); // Save export to Downloads
```
Expose these methods from your `WebViewClient` implementation in Kotlin/Java.

### Firebase Setup
Replace the `firebaseConfig` object in both `index.html` and `login.html` with your own Firebase project credentials:
```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT.firebasestorage.app",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

---

## 📦 Firestore Data Structure

```
elite_users/
  └── {uid}/
        └── tracking: {
              "2025-01-15": { fajr: true, zohr: true, asr: false, ... },
              "2025-01-16": { ... },
              ...
            }
```

Each day's prayer data is stored under `tracking` as a map keyed by `YYYY-MM-DD`.

---

## 📤 Export

The **Dashboard tab** includes an export feature that generates a self-contained HTML report of your prayer record for any date range. The report includes:
- A row per day with ✓/✗ for each prayer
- Score percentage per day (colour-coded green / amber / red)
- Summary: total days tracked and overall average score

---

## 🤝 Contact

- **WhatsApp:** [+91 96036 11435](https://wa.me/919603611435)
- **Instagram:** [@type01warrior](https://www.instagram.com/type01warrior/)

---

## 📄 License

This project is personal/open use. Please credit **Type01warrior** if you build upon it.
