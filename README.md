# CASnival 2026 — Volunteer Desk

A live volunteer check-in site for CASnival at `volunteers.casnival.site`.
Stall owners sign in with their stall's code and mark whether each volunteer
assigned to them turned up. Coordinators see every stall at once.

It uses the **same Google Sheet and the same Apps Script** as the ticket site.
The volunteer data lives in three extra tabs: **Locations**, **Volunteers** and
**Assignments**. Ticket data stays separate, and volunteer codes can't open the
ticket site.

| Who | Signs in with | Can do |
|---|---|---|
| Stall owner / post lead | The 6-letter code for their stall (Locations tab) | See and mark only their own stall's volunteers |
| Coordinator | `COORDINATOR_PIN` in `Volunteers.gs` | See and mark every stall, search, filter no-shows |

Each volunteer can be marked **Arrived**, **Didn't show**, **Left early** or
**Finished shift**, with an optional 1–5 star rating and a short note. Every mark
saves the time and the name of the person who made it, and is also written to the
**Log** tab.

The three rotations are **8:30–10:30**, **10:30–2:00** and **2:00–5:00**. The site
opens on whichever rotation is happening now.

---

## Setup

### Part 1: Add the volunteer script (5 min)

1. Open the **CASnival 2026 Tickets** sheet, then **Extensions → Apps Script**.
2. Click `Code.gs`, select everything, and paste in the new
   `casnival-checkin/apps-script/Code.gs`. It has one new line that sends volunteer
   requests to the new file. Put your two ticket PINs back in.
3. In the **Files** list on the left, click **+ → Script** and name it `Volunteers`.
4. Delete what's in it and paste in all of `casnival-checkin/apps-script/Volunteers.gs`.
5. Near the top, change `CHANGE-ME-COORD` to your own coordinator PIN. Make it different
   from the ticket PINs.
6. Press **Cmd+S** to save.
7. In the function dropdown, choose **setupVolunteers** and click **▶ Run**.
   If Google asks for permission, allow it as before.
8. Go back to the sheet. You should see **Locations**, **Volunteers** and **Assignments** tabs.
9. **Deploy → Manage deployments → ✏️ → Version: New version → Deploy.** The link stays the same.

### Part 2: Fill in the sheet

- **Volunteers tab:** the volunteers are listed as *Volunteer 1* to *Volunteer 88*, in the
  same order as the allocations list. Paste the real names into column **B** in that
  order. Phone numbers in column **C** are optional; stall owners can tap them to call.
- **Locations tab:** column **F** has a random login code for every stall and post.
  Give each stall owner **only their own code**. You can rename stalls in column **B**
  at any time, and the site picks the new name up.
- **Assignments tab:** one row per volunteer per rotation. To move someone, change the
  **Location** code in column D. Don't type in the Status columns; those are filled in
  from the site.

### Part 3: Put the site on GitHub (10 min)

1. On GitHub, click **+ → New repository**, name it `casnival-volunteers`, choose **Public**,
   and click **Create repository**.
2. Click **uploading an existing file** and drag in `index.html`, `config.js` and `README.md`
   from this folder. Click **Commit changes**. `config.js` already has the script link.
3. Go to **Settings → Pages**, set the branch to **main** and **/ (root)**, and click **Save**.

### Part 4: Connect volunteers.casnival.site

1. **Namecheap → Domain List → Manage `casnival.site` → Advanced DNS → Add New Record**:
   - **Type:** CNAME Record
   - **Host:** `volunteers`
   - **Value:** `aatisherra.github.io.`
2. In the new repository, go to **Settings → Pages → Custom domain**, type
   `volunteers.casnival.site` and click **Save**.
3. Once the DNS check is green, wait for the certificate, then tick **Enforce HTTPS**.

### Part 5: Test

1. Open the site and sign in with your name and one stall's code. You should see only
   that stall's volunteers.
2. Tap **✓ Arrived** on one volunteer. The row in the **Assignments** tab turns green.
3. Sign out (tap your name at the top right) and sign in with the **coordinator PIN**.
   You should see every stall, grouped, with arrived/total counts.
4. Set the test volunteer back with **Undo — set back to not marked**.

---

## Stall numbers

Food stalls are **F**, game stalls are **G**, matching the map. The **Map** column is
the code printed on the stall map.

| Code | Area | Map | | Code | Area | Map |
|---|---|---|---|---|---|---|
| F1 | Basketball courts (top) | SS | | G1 | Turf (by stage) | PE |
| F2 | Basketball courts (top) | DS | | G2 | Turf (by stage) | GS |
| F3 | Basketball courts (top) | CS | | G3 | Turf (right side) | AT |
| F4 | Basketball courts (top) | FS | | G4 | Turf (right side) | NR |
| F5 | Basketball courts (bottom) | JM | | G5 | Turf (right side) | CF |
| F6 | Basketball courts (bottom) | SG | | G6 | Turf (right side) | LC |
| F7 | Basketball courts (bottom) | CN | | G7 | Turf (bottom) | FL |
| F8 | Basketball courts (bottom) | MM | | G8 | Turf (bottom) | SH |
| F9 | Palm Court | ST | | G9 | Turf (bottom) | WB |
| F10 | Palm Court | CC | | G10 | Turf (bottom) | DL |
| F11 | Palm Court | PZ | | G11 | Turf (bottom) | SK |
| F12 | Palm Court | IO | | G12 | Turf (top left) | SC |
| F13 | Palm Court | 45 | | G13 | Turf (top left) | TTT |
| F14 | Palm Court | BD | | G14 | Turf (left side) | GR |
| F15 | Palm Court | GA | | G15 | Turf (left side) | AF |
| F16 | Basketball courts (bottom) | CT | | G16 | Next to cricket pitch | ND |
| F17 | Basketball courts (bottom) | FB | | G17 | Teacher's car park | PA |
| F18 | Basketball courts (bottom) | TB | | G18 | Not on map yet | — |
| F19 | Teacher's car park | MR | | | | |
| F20 | Next to cricket pitch | SP | | | | |
| F21 | Not on map yet | FF | | | | |

**Other locations:** Bouncy Castle (BC), Rodeo Bull (RB), Trampoline (TP), Oak Jail,
Ticket check (Gate 2), Ticket counter (Gate 2), Ticket counter (Atrium), Coupon
counters 1 and 2, Water bottles, Student security (Gate 5), NGO stall (to confirm)
and Floaters.

**To check:**
- **F21** (FF) is in the food legend but not drawn on the map.
- **G18** is the "carnival craze" post from the allocations list. It isn't on either map.
- **NGO stall (to confirm)** is the "chitra mam ngo" post from the allocations list.
  If it's one of the NGO stalls on the map (G8, G12, G14, G15 or G16), change those
  volunteers' Location codes in the Assignments tab.
- **TP** (Trampoline) is in the legend but not on the newer map.
- "DIY handicrafts" in the allocations list is assumed to be **G5** (Carnival Crafts).

## Trying it without the sheet

If `API_URL` in `config.js` is empty, the site runs in **demo mode** on that device only.
Use `1234` for the coordinator, or `FOOD01`, `GAME03` or `OAK000` as stall codes.
