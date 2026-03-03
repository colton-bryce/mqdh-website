# Michigan Quality Deer Habitat — Website

Single-page website with a contact form that sends email via Gmail SMTP.

---

## Setup

### 1. Install dependencies

```bash
npm install
```

### 2. Create your .env file

```bash
cp .env.example .env
```

Open `.env` and fill in your values (see below).

### 3. Generate a Gmail App Password

The server uses Gmail SMTP with an **App Password** — not your regular Gmail
password. This requires 2-Step Verification to be enabled on the sending account.

1. Go to **myaccount.google.com/security** and enable **2-Step Verification**
   if you haven't already.

2. Go to **myaccount.google.com/apppasswords**

3. Click **"Create a new app password"**, give it a name like `MQDH Website`,
   and click **Create**.

4. Copy the 16-character code Google shows you (e.g. `abcd efgh ijkl mnop`).

5. Paste it into `.env` as `EMAIL_PASS` — remove any spaces:
   ```
   EMAIL_PASS=abcdefghijklmnop
   ```

### 4. Fill in .env

```
EMAIL_USER=you@gmail.com        # the Gmail account generating the App Password
EMAIL_PASS=abcdefghijklmnop     # the 16-char App Password (no spaces)
PORT=3000
```

### 5. Start the server

```bash
npm start
```

Then open **http://localhost:3000** in your browser.

For development with auto-restart on file changes (Node 18+):

```bash
npm run dev
```

---

## How it works

- Express serves `index.html` and all static assets from the project folder.
- When the contact form is submitted, the browser sends a `POST /contact`
  request with the form data as JSON.
- The server sends an email to `coltonabryce@gmail.com` via Nodemailer.
- The `Reply-To` header is set to the contact's email address so you can
  reply directly from your inbox.

---

## Project structure

```
index.html      — single-page website
server.js       — Express + Nodemailer backend
package.json    — Node dependencies
.env            — your secrets (never commit this)
.env.example    — template for .env
.gitignore      — excludes .env and node_modules
```
