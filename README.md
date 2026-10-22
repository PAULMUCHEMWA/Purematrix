# Puremetrix Operations Hub

Company communication and management site: jobs map with progress photos, requests to procurement and accounts, cash advances and receipts, messages, monthly PDF reports.

Files: `index.html` (the app), `config.js` (your Firebase details), `firebase-rules.json` (database rules), `netlify.toml`.

## Deploy: GitHub, then Netlify
1. GitHub: create a **private** repository and upload everything from this folder (Add file, Upload files).
2. Netlify: Add new site, Import an existing project, GitHub, pick the repository. Leave build command empty; publish directory `.`. Deploy.
3. The site works straight away in **Demo mode** (one device only). To go live for the whole company follow the steps below.

## Go live (shared data, free)
1. https://console.firebase.google.com: Add project. Authentication, Get started, **Email/Password**, Enable.
2. Realtime Database: Create database (locked mode). Open **Rules**, paste `firebase-rules.json`, Publish.
3. Project settings, Your apps, Web (`</>`): copy `apiKey` and the Realtime Database URL.
4. Edit `config.js` in GitHub (pencil icon), uncomment the two lines and paste your values. Commit. Netlify redeploys in about a minute.
5. **Immediately** open your Netlify site and press "First time here? Set up the Admin account" (the first account created is Admin). Then People, + Add worker.
6. Optional: in Netlify, Domain management to use your own address. Firebase, Authentication, Settings, Authorized domains: add your Netlify domain if sign-in complains.

The apiKey in `config.js` is not a secret; protection comes from the database rules.

---



## User guide
## Job categories and the Workshop
Job categories: Anti-band door, Safes (with a size such as 40L, 60L, 100L or a custom size), Strongroom door, Archive doors, Vaults, Man trap doors, Safe relocation, Alarms, CCTV, Biometric access control, Key cabinets, Gun cabinets, Security screens, Automated sliding gates, Intelligent electronic security locks, Electronic boom gates.

**Workshop** (menu, under Jobs & map) shows who is making what right now, grouped by worker. Anyone can add an item (what it is, size, who is making it), set its stage (Queued, Cutting & welding, Assembly, Finishing & paint, Ready for delivery, Delivered to site, Installed), a percentage, and upload photos of the current state. Link an item to a job and the job screen shows "What is being made for this job" with the maker and stage, so site staff can see whose safe or door is being fitted. Managers are notified of production updates.

## Signing in
Everyone signs in with a **Login ID** and **password**. New accounts start with password **0000**; the app shows a yellow banner until the person changes it (Profile → Change password; 0000 is not accepted as the new password).

## Adding workers
People → **+ Add worker**: name, department, job title, phone, Login ID (suggested from the name), starting password (0000), and a role template. Tick or untick the see/do permissions if needed. When saved, a **login card** appears – copy or send it to the worker. Workers are grouped by department on the People page. Untick "Account active" to block someone.

## Access (set per person by the Admin)
People → **Access** next to a name.
**See:** all jobs · all requests · staff money · reports/CSV · activity log.
**Do:** create/edit jobs · approve requests · handle equipment requests (tick bought) · issue funds / verify receipts · announcements · manage staff.
Everyone can always post progress and photos on their assigned jobs, request equipment or cash, message colleagues, and upload receipts for money given to them.

## Jobs and progress (everyone)
Anyone can press **+ New job** (or "Add a job" on Home). They are put on the job automatically and can **edit it**, set its status, and **post progress with photos and a percentage** (shown as the pie chart). Anyone who can see a job but isn't on it can press **Join this job**. Only people with the "create/edit jobs" tick can edit or delete *other people's* jobs. Managers and the Director are notified when someone adds a job or posts progress.

## Money flow
1. A worker uses **Request cash**. Accounts gets a notification and presses **Issue funds**.
2. The worker is asked to tick **I received this money** (Accounts sees "waiting for confirmation" until then).
3. The worker adds each expense with a receipt photo/PDF and amount; **change remaining** updates. Accounts is notified of every receipt and ticks **Verify** (or **Query** with a reason).
4. If money is left, the worker presses **Return my change**, enters how much, and Accounts is notified.
5. Accounts ticks **Change received** (or **Not received**, with a note). When money given = money used + change received and every receipt is verified, the advance shows **Balanced ✔** and closes automatically; the worker is told.
Items work the same way: Procurement ticks **Bought / given**, then the requester ticks **I received it**.

## Monthly PDF reports
Reports → **Download monthly PDFs** (also buttons on Requests and Money). Pick a month:
- **Items requested:** who asked, who approved, who bought/gave it and when, and when it was received.
- **Cash and receipts:** a balance sheet of money given vs money used, a summary by staff member, and for every advance who requested it, who gave it, whether it was received, what it was used for, receipts checked, change returned and whether it balances.

## How requests reach the right person
A worker picks **Send to** (the whole Procurement or Accounts team, or one named person). That person gets a card on Home, a red badge, a sound and a bell entry. They can pass it on, comment, mark ordered, or tick **Bought / given**, which clears the alert for everyone and tells the worker. For cash, **Issue funds** puts the money in the worker's Money tab, where receipts are uploaded and change remaining is shown.

## Limits to know
- **Passwords in live mode:** Firebase needs 6+ characters, so the app adds a hidden prefix to what you type (0000 works). A forgotten password can only be e-mailed if the worker has a real e-mail saved; otherwise Admin must delete and re-add the worker with a new Login ID. (Demo mode: Admin can reset to 0000.)
- Live-mode sign-in was tested against a simulated Firebase, **not a real project** – do a quick trial with 2 accounts after setup.
- Hiding jobs/requests inside the app is not a hard lock: any active signed-in staff member could read them technically. Money records, inboxes and the activity log are locked by the rules.
- Alerts appear while the app is open (banner, sound, bell). Phone push alerts when closed need a later upgrade.
- Photos are compressed; PDFs/files max 1.5 MB. Move to Firebase Storage if you collect thousands of photos.
