# Compass Rose Leisure — Website Concept
### Design by Chris Bohn

A luxury travel agency website with an AI-powered lead generation chatbot ("Rose"), built for Compass Rose Leisure.

---

## What's included

- Full single-page website (hero, specialties, destinations, process, testimonials, CTA, footer)
- Floating "Rose" AI chat widget — powered by Claude (Anthropic API)
- Serverless API backend (`/api/chat`) that keeps the API key secure server-side
- Lead capture: when Rose collects a visitor's name + email, a toast notification fires (this is where you'd hook in email/CRM notifications)
- Mobile responsive

---

## Deploy to Vercel in 5 minutes

### Prerequisites
- A [Vercel account](https://vercel.com) (free)
- An [Anthropic API key](https://console.anthropic.com) (get one at console.anthropic.com)
- [Node.js](https://nodejs.org) installed locally
- [Vercel CLI](https://vercel.com/docs/cli) — install with: `npm i -g vercel`

---

### Step 1 — Install dependencies
```bash
cd compass-rose
npm install
```

### Step 2 — Deploy to Vercel
```bash
vercel
```
Follow the prompts:
- Set up and deploy? → **Y**
- Which scope? → select your account
- Link to existing project? → **N**
- Project name → `compass-rose-leisure` (or whatever you like)
- In which directory is your code located? → **./  (just hit Enter)**
- Want to modify these settings? → **N**

Vercel will give you a preview URL. Copy it.

### Step 3 — Add your Anthropic API key
```bash
vercel env add ANTHROPIC_API_KEY
```
- Select **Production**, **Preview**, and **Development**
- Paste your API key when prompted

### Step 4 — Redeploy with the env variable live
```bash
vercel --prod
```

Your live URL will look like: `https://compass-rose-leisure.vercel.app`

---

## How Rose works

1. Visitor clicks the gold chat bubble (bottom-right corner)
2. Rose asks about their trip — honeymoon, family vacation, Europe, Caribbean, etc.
3. Rose naturally collects: destination, travel dates, number of travelers, budget range, name, email
4. When name + email are captured, a `LEAD_CAPTURED` payload is returned from the API
5. A toast notification fires on-screen (in production, this is where you'd fire a webhook to email/HubSpot/Google Sheets)

### Adding email notifications for leads (optional next step)
In `/api/chat.js`, after `let leadData = JSON.parse(...)`, add:
```js
// Example: send to a webhook (Zapier, Make, etc.)
await fetch('https://hooks.zapier.com/your-webhook-url', {
  method: 'POST',
  body: JSON.stringify(leadData)
});
```
Or use Nodemailer / SendGrid to email the lead directly to the advisors.

---

## Project structure

```
compass-rose/
├── api/
│   └── chat.js          # Serverless function — Anthropic API proxy
├── public/
│   └── index.html       # Full website + chat widget
├── package.json
├── vercel.json          # Routing config
└── README.md
```

---

## Customization notes

- **Rose's personality & goals** — edit the `SYSTEM_PROMPT` constant in `/api/chat.js`
- **Website content** — all copy is in `/public/index.html`, clearly sectioned
- **Colors** — CSS variables at the top of the `<style>` block: `--navy`, `--gold`, `--sand`
- **Agency stats** (500+ trips, etc.) — update in the hero section of `index.html`

---

*Built with Claude (Anthropic) · Deployed on Vercel · Design concept by Chris Bohn*
