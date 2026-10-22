# Puremetrix Operations Hub – setup & user guide

## 1. Try it first (no setup)
Open `PuremetrixHub.html`. It starts in **Demo mode**. Tap any name on the sign-in page (or type a Login ID) and use password **0000**. Demo Login IDs: admin, director, manager, supervisor, procurement, assistant, accounts, sales, tendai, farai. Demo data lives on that one device only.

## 2. Go live for the whole company (free, ~15 minutes)
1. https://console.firebase.google.com → **Add project**.
2. **Authentication → Get started → Email/Password → Enable.**
3. **Realtime Database → Create database** (locked mode).
4. Realtime Database → **Rules** → paste the contents of `firebase-rules.json` → **Publish**. (If you set up earlier, paste the new rules again – they now let workers add jobs, declare change and confirm receipts.)
5. Project settings → **Your apps → Web (</>)** → copy `apiKey` and the Realtime Database URL.
6. In `PuremetrixHub.html` change `window.PM_CONFIG={};` to
   `window.PM_CONFIG={apiKey:"YOUR_API_KEY",databaseURL:"YOUR_DATABASE_URL"};`
7. Host the file (any web host / Firebase Hosting) and open it.
8. **Straight away** press **"First time here? Set up the Admin account"** and create your Admin (Login ID + password). Do this before sharing the link: the first account created becomes Admin.
9. Admin → **People → + Add worker**.

## Signing in
Everyone signs in with a **Login ID** and **password**. New accounts start with password **0000**; the app shows a yellow banner until the person changes it (Profile → Change password; 0000 is not accepted as the new password).

## Adding workers
People → **+ Add worker**: name, department, job title, phone, Login ID (suggested from the name), starting password (0000), and a role template. Tick or untick the see/do permissions if needed. When saved, a **login card** appears – copy or send it to the worker. Workers are grouped by department on the People page. Untick "Account active" to block someone.

## Access (set per person by the Admin)
People → **Access** next to a name. The Admin has overall power: every tick can be changed at any time.
**See:** all jobs · all requests · staff money · reports/CSV · activity log.
**Do:** create jobs and workshop items · edit any job · approve requests · handle equipment · **cash desk** (see cash requests and receipts, approve cash) · issue funds / verify receipts · announcements · manage staff.

## New people create their own account
On the sign-in page anyone can press **New here? Create an account**. The account stays switched off until the Admin approves it (People → **Waiting for your approval** → Approve, where the Admin picks the role and access). Pending people cannot see anything.

## Jobs and progress
Only **Admin, Director, Manager and Supervisor** can add jobs and workshop items (the Admin can tick **Create jobs and Workshop items** for anyone else in People → Access). When they add one they **tag** the people working on it. Tagged people get a notification in their Inbox (plus a sound and a bell alert while the app is open), and can then post progress, percentage and photos. Only managers can edit or delete the job itself.

## Job categories and the Workshop
Job categories: Anti-band door, Safes (with a size such as 40L, 60L, 100L or a custom size), Strongroom door, Archive doors, Vaults, Man trap doors, Safe relocation, Alarms, CCTV, Biometric access control, Key cabinets, Gun cabinets, Security screens, Automated sliding gates, Intelligent electronic security locks, Electronic boom gates.

**Workshop** (menu, under Jobs & map) shows who is making what right now, grouped by worker. Anyone can add an item (what it is, size, who is making it), set its stage (Queued, Cutting & welding, Assembly, Finishing & paint, Ready for delivery, Delivered to site, Installed), a percentage, and upload photos of the current state. Link an item to a job and the job screen shows "What is being made for this job" with the maker and stage, so site staff can see whose safe or door is being fitted. Managers are notified of production updates.

## Documents: quotations, invoices, receipts and statements
Menu → **Documents** (Admin, Director, Manager, Accounts by default; the Admin can tick **Documents** for anyone in People → Access).
- **Make quotation / invoice / receipt:** a window asks for the customer name, address, RE:, the items and who approves (Ziviso Mhere or Owen Mugari). The document number (000001, 000002… each type counts on its own), today's date, BP NO, TIN NO and bank details are added for you, and "Prepared by" is the signed-in person and their phone number.
- Press **Create** and the **sheet** opens (same layout as your Excel files). Every white cell is editable. **Save** keeps it; open it again any day from the list to change it. **PDF** and **Excel** buttons download it.
- **Admin → Numbering** lets you set the next number for each type (e.g. to carry on from your old books).
- **Paid or not:** the moment an invoice is created, Accounts, Directors and Managers get a notification with a **☐ Paid** button (also on the invoice list and sheet). Paid = credited on the customer statement; not paid = stays as debit. **Part payment** records partial amounts. A receipt made "for invoice no." marks that invoice paid automatically.
- **Statements:** Documents → Statements shows outstanding per company, and a statement per customer built automatically from invoices against payments, with the date of each invoice. Choose the period (From/To), then download PDF or Excel. **PDF (all companies)** gives the outstanding balances for everyone. Each document list also has **PDF list** which asks for the period.

## Money flow (strict and traceable)
1. Anyone presses **Request cash** and must state the **purpose**. Only the **cash desk** (Accounts and Procurement) and the Admin can see it. Procurement can approve; Accounts issues the funds.
2. The worker gets a notification and ticks **I received this money**. At that moment it is **booked in the Cash book** (Money → 📒 Cash book).
3. The worker adds each expense with a receipt; Accounts and Procurement see the receipts and Accounts verifies them. Verified spending is booked.
4. If money is left, the worker presses **Return my change** and enters the amount. Accounts gets a "tick when received" notification; ticking it books the change into the Cash book, and the advance balances and closes.
5. Every advance has an **Audit trail** (requested → approved → issued → received → each receipt → change → balanced), with names and times.
Items work as before: Procurement ticks **Bought / given**, then the requester ticks **I received it**.

## Monthly PDF reports
Reports → **Download monthly PDFs** (also buttons on Requests and Money). Pick a month:
- **Items requested:** who asked, who approved, who bought/gave it and when, and when it was received.
- **Cash and receipts:** a balance sheet of money given vs money used, a summary by staff member, and for every advance who requested it, who gave it, whether it was received, what it was used for, receipts checked, change returned and whether it balances.

## How requests reach the right person
A worker picks **Send to** (the whole Procurement or Accounts team, or one named person). That person gets a card on Home, a red badge, a sound and a bell entry. They can pass it on, comment, mark ordered, or tick **Bought / given**, which clears the alert for everyone and tells the worker. For cash, **Issue funds** puts the money in the worker's Money tab, where receipts are uploaded and change remaining is shown.

## Limits to know
- **Passwords in live mode:** Firebase needs 6+ characters, so the app adds a hidden prefix to what you type (0000 works). A forgotten password can only be e-mailed if the worker has a real e-mail saved; otherwise Admin must delete and re-add the worker with a new Login ID. (Demo mode: Admin can reset to 0000.)
- Live-mode sign-in was tested against a simulated Firebase, **not a real project** – do a quick trial with 2 accounts after setup.
- Cash requests and money records ARE locked in the database: only the cash desk/Admin (and the requester for their own) can read them. Receipt photos are stored by an unguessable ID, so they are hidden in the app but are not a hard lock.
- Hiding jobs/equipment requests inside the app is not a hard lock: any active signed-in staff member could read them technically. Money records, inboxes and the activity log are locked by the rules.
- Alerts appear while the app is open (banner, sound, bell). Phone push alerts when closed need a later upgrade.
- Photos are compressed; PDFs/files max 1.5 MB. Move to Firebase Storage if you collect thousands of photos.
