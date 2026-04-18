# KSP Feedback App 🍱

> **Khane Se Pyaar** — Monthly Menu Feedback  
> Built by [DigiFX Solutions](https://digifx.in) for premium tiffin client management.

---

## 🌟 Overview

A **zero-dependency**, single-file mobile web app for collecting monthly menu feedback from KSP's premium clients. Designed to be fast, beautiful, and functional — with Apple-style minimalism and an absolute dark mode.

---

## ✨ Features

- **Client Identity** — Name + Flat/Block number captured with every submission
- **28 Menu Items** across 3 categories: Gravy, Dry, and Special
- **3-Tier Rating System** — Loved it / Fine / Needs work per dish
- **Skip Button** — For dishes not tried this month
- **5-Star Overall Rating** — Holistic monthly experience score
- **Sticky Progress Header** — Live tracking (e.g. 14/28 rated)
- **Suggestions Box** — Free-text client feedback
- **Premium Success Screen** — Personalized "Thank You, [Name]!" overlay
- **Google Sheets Integration** — One-click data pipeline via Apps Script
- **Zero Dependencies** — Pure HTML5 + Tailwind CDN + Vanilla JS

---

## 🚀 Usage

Simply open `index.html` on any mobile device or host it on any static server.

```bash
# Local preview (macOS)
open index.html
```

---

## 📊 Google Sheets Setup (5 Steps)

1. Open your **Google Sheet**
2. Go to **Extensions → Apps Script**
3. Paste the script below:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheets()[0];
  var data = JSON.parse(e.postData.contents);
  sheet.appendRow([
    new Date(),           // Timestamp
    data.name,            // Client Name
    data.phone,           // Flat / Block Number
    data.totalRated,      // Items Rated count
    data.overallRating,   // 1–5 star overall score
    data.suggestions,     // Free-text feedback
    JSON.stringify(data.ratings) // All dish ratings as JSON
  ]);
  return ContentService.createTextOutput("Success")
    .setMimeType(ContentService.MimeType.TEXT);
}
```

4. **Deploy → New Deployment → Web App**  
   - Execute as: **Me**  
   - Who has access: **Anyone**  
5. Copy the **Web App URL** and paste it into `SCRIPT_URL` in `index.html`

---

## 🎨 Design System

| Token | Value |
|:---|:---|
| Background | `#000000` (Absolute Black) |
| Primary Accent | `#f97316` (KSP Orange) |
| Typography | Plus Jakarta Sans |
| Border Radius | 24–32px (Apple-style) |
| Glassmorphism | `rgba(255,255,255,0.03)` + `backdrop-filter: blur(20px)` |

---

## 📁 File Structure

```
ksp feedback/
└── index.html    ← Complete self-contained app (logo embedded as base64)
```

---

© 2026 Khane Se Pyaar · Built with ❤️ by DigiFX Solutions
