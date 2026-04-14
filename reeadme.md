# Booking System

&#x20;

A fully custom, branded appointment booking system for a psychology practice. Built with vanilla HTML/CSS/JS on the frontend and Google Sheets + Apps Script as the backend. Hosted for free on GitHub Pages.

***

## 🌐 Live Demo

[janademboski-jpg.github.io/janaina-agenda](https://janademboski-jpg.github.io/janaina-agenda/)

***

## ✨ Features

* Weekly calendar view with available slots
* Booking form with validation (name, WhatsApp, email, tipo de atendimento, message)
* Tipo de atendimento: Online / Presencial — Águas Claras / Presencial — Plano Piloto
* Booking confirmation email to patient with cancel link
* Notification email to practitioner
* Cancel booking flow via unique token link
* Admin panel with password protection (tabs: Horários + Agendamentos)
* Add / Edit / Delete / Block / Liberar slots
* Skeleton loading with shimmer animation
* Warm + Dark theme toggle (☀️ / 🌙)
* Fully responsive (mobile + desktop)
* SEO optimised with Open Graph, Twitter Card, JSON-LD structured data
* Google Analytics GA4 with custom events
* Accessibility compliant (ARIA labels, roles, landmarks)
* Local fonts (Great Vibes, Playfair Display, Inter)
* Performance: 95 mobile / 92 desktop (PageSpeed)

***

## 📁 File Structure

```
/
├── index.html          # Main page — all UI structure
├── style.css           # All styles — tokens, components, responsive
├── app.js              # All logic — calendar, booking, admin, themes
├── Code.gs             # Google Apps Script — API backend
├── og-image.jpg        # Open Graph image for social previews
├── fonts/              # Local woff2 font files
│   ├── great-vibes-v21-latin-regular.woff2
│   ├── playfair-display-v40-latin-regular.woff2
│   ├── playfair-display-v40-latin-500.woff2
│   ├── playfair-display-v40-latin-italic.woff2
│   ├── playfair-display-v40-latin-500italic.woff2
│   ├── inter-v20-latin-300.woff2
│   ├── inter-v20-latin-regular.woff2
│   └── inter-v20-latin-500.woff2
└── README.md

```

***

## 🛠️ Setup Guide

### Prerequisites

* GitHub account
* Google account
* No server, no database, no paid services needed

***

### Step 1 — Create the Google Sheet

1. Go to [sheets.google.com](https://sheets.google.com/) and create a new spreadsheet
2. Name it `Janaina Agenda` (or anything you prefer)
3. Create two tabs at the bottom: **Slots** and **Bookings**

**Slots tab — add these headers in row 1:**

| A  | B   | C    | D      | E    |
| :- | :-- | :--- | :----- | :--- |
| ID | Day | Time | Status | Date |

**Bookings tab — add these headers in row 1:**

| A      | B    | C        | D     | E        | F    | G         | H     |
| :----- | :--- | :------- | :---- | :------- | :--- | :-------- | :---- |
| SlotID | Name | Whatsapp | Email | Mensagem | Tipo | Timestamp | Token |

***

### Step 2 — Set up Google Apps Script

1. In your Google Sheet, go to **Extensions → Apps Script**
2. Delete all existing code in the editor
3. Copy the entire contents of `Code.gs` and paste it
4. Update the following constants at the top:

```
const ADMIN_PASSWORD = "your_password_here";
const SITE_URL       = "https://yourusername.github.io/your-repo/";
// JANA_EMAIL is hardcoded in the email functions — find and replace
// 'janademboskipsi@gmail.com' with the practitioner's email

```

1. Click **💾 Save**
2. Click **Deploy → New deployment**
3. Type: **Web app**
4. Execute as: **Me**
5. Who has access: **Anyone**
6. Click **Deploy** → Copy the deployment URL

> ⚠️ Every time you change `Code.gs` you must create a **New deployment** — editing an existing deployment does NOT update the live API.

***

### Step 3 — Set up the Frontend

1. Fork or clone this repository to your GitHub account
2. Open `app.js` and update line 2:

```
const API_URL = 'YOUR_APPS_SCRIPT_DEPLOYMENT_URL_HERE';

```

1. Open `index.html` and update:

   * Practitioner name (search for `Janaína Demboski`)
   * CRP number (search for `CRP 01/31035`)
   * Locations (search for `Águas Claras` and `Plano Piloto`)
   * WhatsApp number (search for `5561992849023`)
   * Instagram handle (search for `psi.janainspira`)
   * Canonical URL and OG URLs (search for `janademboski-jpg.github.io`)
   * Google Analytics ID (search for `G-PSYB15ZH4S`)
2. Replace `og-image.jpg` with your own branded image (recommended: 1200x630px)

***

### Step 4 — Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings → Pages**
3. Source: **Deploy from a branch**
4. Branch: **main** → **/ (root)**
5. Click **Save**
6. Wait \~2 minutes, then visit `https://yourusername.github.io/your-repo/`

***

### Step 5 — Test the Setup

1. Open the site and check the calendar loads (no error message)
2. Click a slot → fill the form → submit booking
3. Check the Bookings tab in Google Sheet — a new row should appear
4. Check your email — you should receive the notification
5. Open admin panel → enter password → check both tabs work

***

## ⚙️ Configuration Reference

### `Code.gs` Constants

| Constant              | Description                                  |
| :-------------------- | :------------------------------------------- |
| `SHEET_NAME_SLOTS`    | Name of the slots tab in Google Sheet        |
| `SHEET_NAME_BOOKINGS` | Name of the bookings tab                     |
| `ADMIN_PASSWORD`      | Password for the admin panel                 |
| `SITE_URL`            | Your GitHub Pages URL (used in cancel links) |

### `app.js` Constants

| Constant  | Description                     |
| :-------- | :------------------------------ |
| `API_URL` | Your Apps Script deployment URL |

### Admin Panel Password

Change `ADMIN_PASSWORD` in `Code.gs`, save, and deploy a new version.

***

## 📧 Email Flow

| Event        | Emails sent                                            |
| :----------- | :----------------------------------------------------- |
| New booking  | Notification to practitioner + Confirmation to patient |
| Cancellation | Notification to practitioner + Confirmation to patient |

All emails include formatted date, time, tipo de atendimento, and contact details.

***

## 🔒 Security Notes

* The Apps Script URL is public — this is intentional and safe for this use case
* Admin actions (edit, delete, block) are protected by the admin password
* Cancel tokens are unique per booking and single-use
* Patient data is stored only in your private Google Sheet

***

## 📊 Google Analytics Events

| Event               | Triggered when                |
| :------------------ | :---------------------------- |
| `slot_selected`     | Patient clicks a slot         |
| `booking_completed` | Patient completes a booking   |
| `booking_cancelled` | Patient confirms cancellation |

***

## 🗂️ Google Sheet Schema

### Slots tab

| Column | Field  | Format                  | Example          |
| :----- | :----- | :---------------------- | :--------------- |
| A      | ID     | `YYYY-MM-DD-HHh`        | `2026-04-01-20h` |
| B      | Day    | Portuguese short        | `Terca`          |
| C      | Time   | `HHh` or `HHhMM`        | `20h` or `20h30` |
| D      | Status | `available` or `booked` | `available`      |
| E      | Date   | `YYYY-MM-DD`            | `2026-04-01`     |

### Bookings tab

| Column | Field     |
| :----- | :-------- |
| A      | SlotID    |
| B      | Name      |
| C      | Whatsapp  |
| D      | Email     |
| E      | Mensagem  |
| F      | Tipo      |
| G      | Timestamp |
| H      | Token     |

***

## 🚧 Roadmap (Version 2.0)

* \[ ] Monthly calendar view with prev/next navigation
* \[ ] Recurring slots (add every Tuesday 20h for N weeks)
* \[ ] Zoom auto-link for online appointments
* \[ ] SMS reminders (24h before appointment)
* \[ ] Intake forms (pre-session questions)
* \[ ] Google Calendar sync
* \[ ] Multi-language support (PT/EN)
* \[ ] Appointment summary card with timezone

***

## 🛠️ Built With

* Vanilla HTML, CSS, JavaScript — no frameworks
* Google Sheets — data storage
* Google Apps Script — serverless API
* GitHub Pages — free hosting
* Great Vibes + Playfair Display + Inter — Google Fonts (self-hosted)

***

## 👨‍💻 Developer

Built by [Saurabh Shah](https://saurabhshah.me/)
