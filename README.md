# DataEdge — Installment Data Plans
### A product of Vortexedge Limited

DataEdge is a Nigerian fintech web app that lets users subscribe to mobile data plans and pay in small daily installments, fully automated. Powered by Supabase, Paystack, and Termii.

---

## 🚀 Deploy to GitHub in 5 Steps

### Step 1 — Push this repo to GitHub

```bash
git init
git add .
git commit -m "Initial DataEdge deployment"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/dataedge.git
git push -u origin main
```

> Create the repo first at https://github.com/new (set to Public, no README).

---

### Step 2 — Enable GitHub Pages

1. Go to your repo → **Settings** → **Pages**
2. Under **Source**, select **GitHub Actions**
3. Done — frontend auto-deploys on every push to `main`

Your live URL: `https://YOUR_USERNAME.github.io/dataedge/`

---

### Step 3 — Get your Supabase tokens

| What | Where |
|---|---|
| `SUPABASE_ACCESS_TOKEN` | https://supabase.com/dashboard/account/tokens → Generate new token |
| `SUPABASE_PROJECT_REF` | Your project URL — the ID after `/project/` e.g. `jhwsdurdkpciwezhlgzt` |

---

### Step 4 — Add GitHub Secrets

Repo → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**:

| Secret Name | Value |
|---|---|
| `SUPABASE_ACCESS_TOKEN` | Token from Step 3 |
| `SUPABASE_PROJECT_REF` | Project ref from Step 3 |

---

### Step 5 — Run the workflows

Go to repo → **Actions** tab, then trigger manually in this order:

1. **🗄️ Deploy Database** → Run workflow
2. **🛠️ Deploy Backend** → Run workflow
3. Frontend (Pages) already deployed from your Step 1 push ✅

---

## ⚙️ Supabase Edge Function Secrets

Supabase Dashboard → **Settings** → **Edge Functions** → **Add new secret**:

| Secret | Value |
|---|---|
| `SUPABASE_URL` | `https://jhwsdurdkpciwezhlgzt.supabase.co` |
| `SUPABASE_SERVICE_ROLE_KEY` | Settings → API → service_role key |
| `PAYSTACK_SECRET_KEY` | Paystack Dashboard → Settings → API Keys |
| `TERMII_KEY` | Termii Dashboard → API tokens |
| `VTU_SECRET` | Your VTU provider API secret |

---

## 🔔 Paystack Webhook

Dashboard → Settings → Webhooks → Set URL to:
```
https://jhwsdurdkpciwezhlgzt.supabase.co/functions/v1/paystackWebhook
```
Enable event: **charge.success**

---

## 🗃️ Workflows at a Glance

| Workflow | Auto-triggers on | What it does |
|---|---|---|
| `deploy-pages.yml` | Changes to `index.html`, `mobile.html` | Deploys frontend to GitHub Pages |
| `deploy-functions.yml` | Changes to `supabase/functions/**` | Deploys all 8 Edge Functions |
| `deploy-migrations.yml` | Changes to `supabase/migrations/**` | Runs `supabase db push` |

All have a **Run workflow** button in Actions for manual runs.

---

## 📁 Project Structure

```
dataedge/
├── index.html                         # Web app
├── mobile.html                        # Mobile PWA
├── manifest.json
├── .github/workflows/
│   ├── deploy-pages.yml
│   ├── deploy-functions.yml
│   └── deploy-migrations.yml
└── supabase/
    ├── migrations/
    │   ├── 001_initial_schema.sql
    │   ├── 002_rpc_functions.sql
    │   ├── 003_rls_policies.sql
    │   └── 004_indexes_cron_fixes.sql
    └── functions/
        ├── paystackWebhook/
        ├── installmentBilling/
        ├── CreateSubscription/
        ├── createVirtualAccount/
        ├── vtuProcessor/
        ├── retryWorker/
        ├── adminDashboard/
        └── activatePlan/
```

---

**Vortexedge Limited** — All rights reserved © 2025
