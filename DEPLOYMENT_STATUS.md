# Atomic CRM – Deployment-Status

Stand: 2026-06-04

## Live-URLs

| Dienst | URL |
|--------|-----|
| **Produktion (Vercel)** | https://zp-atomic-crm.vercel.app |
| **Supabase API** | https://yqbatimykicunlhhqjof.supabase.co |
| **Lokal (Prod-Build)** | http://127.0.0.1:3000 |

## Erledigt

- [x] Code von `pscadvisory/zp-atomic-crm` geklont
- [x] `npm ci` (empfohlen auf lokalem Pfad `C:\Users\phdsc\zp-atomic-crm` wegen OneDrive)
- [x] Supabase-Projekt **zp-atomic-crm** (`yqbatimykicunlhhqjof`) – 23 Migrationen angewendet
- [x] 6 Edge Functions deployed (users, update_password, postmark, merge_contacts, mcp, delete_note_attachments)
- [x] `.env.production.local` mit `VITE_*` Variablen
- [x] Vercel-Projekt verknüpft, Env-Variablen gesetzt, Production-Deploy
- [x] `vercel.json` mit SPA-Rewrites

## Noch manuell (ca. 5 Min.)

### 1. Supabase Auth-URLs

Dashboard: https://supabase.com/dashboard/project/yqbatimykicunlhhqjof/auth/url-configuration

| Feld | Wert |
|------|------|
| **Site URL** | `https://zp-atomic-crm.vercel.app` |
| **Redirect URLs** | `https://zp-atomic-crm.vercel.app/**` |

### 2. Edge-Function-Secret

Nach `npx supabase login`:

```powershell
$env:NODE_TLS_REJECT_UNAUTHORIZED='0'
npx supabase secrets set SB_PUBLISHABLE_KEY=sb_publishable_CKk3ca24gfQxXKBOPHyELA_pSyL4Kep --project-ref yqbatimykicunlhhqjof
```

Alternativ: Supabase Dashboard → Project Settings → Edge Functions → Secrets.

### 3. Ersten Admin anlegen

https://zp-atomic-crm.vercel.app im Browser öffnen und den Setup-Assistenten durchlaufen.

### 4. Optional später

- Custom SMTP (Postmark, Resend, …) – siehe `setup.md` Schritt 10
- Custom Domain `crm.psc-advisory.de` in Vercel + Supabase Site URL anpassen

## Lokale Entwicklung (Windows)

```powershell
cd C:\Users\phdsc\zp-atomic-crm
npm run build
npx serve -l 3000 dist
```

OneDrive-Pfad `I:\Meine Ablage\ClaudeCode\zp-atomic-crm`: `node_modules` per Junction mit `C:\Users\phdsc\zp-atomic-crm\node_modules` verknüpft.
