# CYFSA Document Analyzer — Vercel Deploy

## Project Structure

```
cyfsa-vercel/
├── api/
│   └── analyze.js       ← Serverless proxy (holds your API key)
├── public/
│   └── index.html       ← Full frontend
├── vercel.json          ← Routing config
└── README.md
```

---

## Deploy in 5 Steps

### 1. Install Vercel CLI (one time)
```bash
npm install -g vercel
```

### 2. Login to Vercel
```bash
vercel login
```

### 3. Deploy from this folder
```bash
cd cyfsa-vercel
vercel
```
- Framework preset: **Other**
- Root directory: `.` (current)
- Say **yes** to defaults

### 4. Add your API key (CRITICAL)
Go to: **vercel.com → your project → Settings → Environment Variables**

Add:
| Name | Value |
|------|-------|
| `ANTHROPIC_API_KEY` | `sk-ant-...your key...` |

Set it for **Production**, **Preview**, and **Development**.

Then redeploy so it picks up the key:
```bash
vercel --prod
```

### 5. Done
Your analyzer is live at `https://your-project.vercel.app`

---

## Embed on Existing Site

If you want to embed the analyzer in an existing site, add an iframe:
```html
<iframe src="https://your-project.vercel.app" width="100%" height="900px" frameborder="0"></iframe>
```

Or link to it directly as a tool page.

---

## Security Notes

- Your `ANTHROPIC_API_KEY` is stored as a Vercel environment variable — it **never** appears in browser source code
- The `/api/analyze` proxy is the only thing that touches Anthropic's API
- To restrict access to your own domain only, update the CORS header in `api/analyze.js`:
  ```js
  res.setHeader('Access-Control-Allow-Origin', 'https://yourdomain.com');
  ```

---

## Local Testing

```bash
vercel dev
```
Then open `http://localhost:3000`

You'll need a `.env.local` file for local dev:
```
ANTHROPIC_API_KEY=sk-ant-...your key...
```
