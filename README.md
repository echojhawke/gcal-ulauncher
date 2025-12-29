# Quick Google Calendar Event Creator for Ulauncher

<img width="656" height="238" alt="image" src="https://github.com/user-attachments/assets/35b8d4bd-1c43-4c73-8911-2526ec64bd7e" />


Create Google Calendar events fast from [Ulauncher](https://ulauncher.io/) using natural language.

This extension **opens a pre-filled Google Calendar event page** in your browser (it does not auto-submit/save the event).

---

## Features

- **3 calendar profiles** with separate keywords:
  - `event` → Personal
  - `wevent` → Work
  - `oevent` → Other
<img width="696" height="508" alt="image" src="https://github.com/user-attachments/assets/fb3c70f3-2580-44c2-819d-7889b30052f9" />

- Natural language date/time parsing:
  - Dates: `tomorrow`, `today`, `this friday`, `next friday`, `dec 25`, `12.25`, `25th`
  - Times: `at 4`, `at 4:30p`, `at 1630`
  - Ranges: `from 3 to 10`, `at 11 to 1`, `from 4:30p-6p`
  - Duration: `for 90m`, `for 2h`, `for 1h30m`
<img width="638" height="237" alt="image" src="https://github.com/user-attachments/assets/4c60cbb4-900e-476f-a33e-5ec8c5f42f4b" />

- Guests:
  - Raw emails: `with someone@gmail.com`
  - Aliases: `with Mom, Dad` (mapped to emails)
  - Mix and match: `with Mom, dad@x.com and John`
- Location & notes:
  - Location: `in Backyard`
  - Notes: `note Bring drinks` (also `desc` / `details`)
- Live “what got parsed” feedback in the result description.

---

## Install (direct)

Open ULauncher Settings
Switch to the Extensions Tab,
Click "Add extension"
Paste the following URL:

```bash
https://github.com/echojhawke/gcal-ulauncher
```
<img width="511" height="221" alt="image" src="https://github.com/user-attachments/assets/5e3359ae-460a-48a7-b4b4-6c62a93487b1" />

Restart Ulauncher:

```bash
pkill ulauncher
ulauncher &
```

Then open: **Ulauncher → Preferences → Extensions** and configure the extension.


## Install (manual)

1. Create the extension folder:

```bash
mkdir -p ~/.local/share/ulauncher/extensions/com.ejh.gcal_event
```

2. Copy these files into the folder:

* `manifest.json`
* `versions.json`
* `main.py`
* `images/icon.png` (optional icon)

3. Restart Ulauncher:

```bash
pkill ulauncher
ulauncher &
```

---

## Configuration

In Ulauncher Preferences → Extensions → Quick Google Calendar Event:

### Keywords

* **Personal keyword** (default: `event`)
* **Work keyword** (default: `wevent`)
* **Other keyword** (default: `oevent`)

### Time zone

* **Time zone (IANA)** (default: `America/Denver`)

### Duration

* **Default duration (minutes)** (default: `60`)

### Calendar URLs

Each profile has a base URL and optional `src`:

* **Base URL** (defaults):

  * Personal: `https://calendar.google.com/calendar/u/0/r/eventedit`
  * Work: `https://calendar.google.com/calendar/u/1/r/eventedit`
  * Other: `https://calendar.google.com/calendar/u/2/r/eventedit`

> Tip: `/u/0`, `/u/1`, `/u/2` correspond to which Google account you’re signed into in your browser session.

#### Using a specific calendar inside an account (`src`)

If “Other” is a shared calendar (not a third Google account), keep the base URL as `/u/0` and set:

* **Other src (optional)** = the calendar ID (often an email address)

Example:

* Other base URL: `https://calendar.google.com/calendar/u/0/r/eventedit`
* Other src: `yourcalendarid@group.calendar.google.com`

---

## Guest Aliases

Configure **Guest aliases** as a single comma-separated line:

```
Mom=mom@example.com, Dad=dad@example.com, John=john@work.com
```

Then use them like:

```
event Family party tomorrow at 1 to 3 with Mom, Dad
```

Unmatched names will be shown as warnings in the result description.

---

## How to use

Type one of the keywords, followed by your event text. The extension will show a single **Create** result. Hit Enter to open a **pre-filled** Google Calendar event page, then click **Save**.

### Full examples (copy/paste)

**1) Appointment + address + emails**

```
event Dentist appointment tomorrow at 2:30p for 1h in 123 Main St, New York City, NY 12345 with dentist@example.com, partner@example.com note Ask about retainers
```

**2) Party using aliases**

```
event Family party this saturday at 4 to 8 with Sarah, Dad, John note Bring chips in 55 W 100 N, Chicago, IL
```

**3) Work meeting + mixed guests**

```
wevent Sprint planning next monday at 10 to 11:30a with pm@company.com, dev1@company.com and John in Zoom note Review backlog and assign tickets
```

**4) “No on” date phrases**

```
event Costco run tomorrow at 6p
event Date night this friday at 7:15p for 2h in PF Changs note Reservation under Echo
```

**5) Time range via `from`**

```
event Road trip from 3 to 10 next friday with friend@gmail.com note Snacks + playlists
```

### Supported keywords / operators

* **Date**

  * `on <date>` (optional)
  * or put date words inside the title: `tomorrow`, `this friday`, `next friday`, `12.15`, `dec 25`
* **Time**

  * `at <time>`
  * `from <start> to <end>`
  * `at <start> to <end>`
* **Duration**

  * `for <duration>` (used when no end time is provided)
* **Guests**

  * `with <emails and/or alias names>`
* **Location**

  * `in <location/address>`
* **Notes**

  * `note <text>` (also accepts `desc` / `details`)

---

## Output formatting

The Ulauncher result shows:

* **Name**: `Create (Personal): Dinner`
* **Description**: `1️⃣ Personal | Dinner | 🗓️: Mar 4 2025 | 🕓: 4p-8p | ⏱: 4h | 👥 2 Mom, Dad`

Badges:

* `1️⃣` Personal
* `2️⃣` Work
* `3️⃣` Other

---


## Limitations

* This extension **does not automatically “Save”** events.

  * It opens a prefilled Google Calendar page where you confirm and click **Save**.
* Creating events without user interaction requires Google Calendar API OAuth (not included).

---

## License

https://github.com/echojhawke/gcal-ulauncher/blob/main/LICENSE
