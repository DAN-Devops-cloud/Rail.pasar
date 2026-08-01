# 🚀 PasarGuard Panel - Railway Deployment Guide

## ✅ What's Ready

I've prepared your PasarGuard Panel for Railway deployment with:

- ✅ **Optimized Dockerfile** - Multi-stage build with Bun + Python
- ✅ **Railway Configuration** - railway.toml with all settings
- ✅ **Environment Setup** - .env.railway with defaults
- ✅ **Self-signed SSL** - Auto-generates cert on first run
- ✅ **Health Checks** - Container monitoring included
- ✅ **Persistent Volume** - Data storage at /var/lib/pasarguard

---

## 📋 Quick Deployment (3 Steps)

### Step 1: Install Railway CLI

```bash
# Option A: via npm
npm i -g @railway/cli

# Option B: via curl
curl -fsSL https://railway.app/install.sh | bash

# Verify
railway --version
```

### Step 2: Login to Railway

```bash
railway login
```

(Opens browser for authentication)

### Step 3: Deploy

```bash
# Extract the archive
tar xzf pasarguard-panel-ready.tar.gz
cd pasarguard-panel

# Initialize Railway project
railway init
# Follow prompts:
# - Project name: "pasarguard-panel"
# - Environment: "production"

# Deploy
railway up

# Monitor
railway logs --follow
```

That's it! 🎉

---

## 🔗 After Deployment

Once deployed, Railway will give you:

```
✓ Logs: railway logs
✓ URL: railway status
✓ Shell: railway shell
✓ Variables: railway variables
✓ Dashboard: https://railway.app
```

Your panel will be accessible at: `https://your-railway-url.up.railway.app`

---

## ⚙️ Default Credentials

| Field | Value |
|-------|-------|
| **Username** | `admin` |
| **Password** | `admin12345` |
| **Port** | `8000` (Railway maps externally) |

**⚠️ Change the password!** Set via Railway dashboard:
```bash
railway variables set SUDO_PASSWORD your-secure-password
```

---

## 📦 What's Included

```
pasarguard-panel-ready.tar.gz contains:
├── Dockerfile                 (Multi-stage build)
├── railway.toml              (Railway config)
├── .dockerignore             (Build optimization)
├── .env.railway              (Env variables)
├── DEPLOY-RAILWAY.md         (Full guide)
├── dashboard/                (Vite frontend)
├── app/                       (Python backend)
├── pyproject.toml            (Dependencies)
└── [other original files]
```

---

## 🛠️ Customization

### Change Admin Password
```bash
railway variables set SUDO_PASSWORD "YourNewPassword123!"
```

### Enable Debug Mode
```bash
railway variables set DEBUG true
railway redeploy
```

### Scale Workers
```bash
railway variables set WORKERS 8
railway redeploy
```

### Custom SSL Certificates
1. Upload cert files to Railway volumes
2. Set paths:
   ```bash
   railway variables set SSL_CERT_FILE /path/to/cert.pem
   railway variables set SSL_KEY_FILE /path/to/key.pem
   railway variables set SSL_CA_TYPE custom
   railway redeploy
   ```

---

## 📊 Monitoring

### View Logs
```bash
railway logs --follow
```

### Health Check Status
```bash
railway shell
curl https://localhost:8000/health
```

### Check Disk Usage
```bash
railway shell
df -h /var/lib/pasarguard
```

---

## 💾 Backup & Restore

### Backup Data
```bash
railway shell
tar czf backup.tar.gz /var/lib/pasarguard
# Download via Railway dashboard
```

### Restore Data
```bash
railway shell
tar xzf backup.tar.gz -C /
```

---

## 🆘 Troubleshooting

| Issue | Solution |
|-------|----------|
| Build fails | `railway logs` - check for syntax errors |
| Memory error | Railway free tier = 5GB; upgrade plan if needed |
| Connection refused | Wait 30s after deploy, check health: `curl -k https://url:8000/health` |
| Cert issues | Self-signed by default; use `-k` for curl or ignore warnings |

---

## 🔗 Useful Links

- **Railway Dashboard**: https://railway.app
- **Railway Docs**: https://docs.railway.app
- **PasarGuard GitHub**: https://github.com/PasarGuard/panel
- **Deploy Docs**: See `DEPLOY-RAILWAY.md` in the archive

---

## ✨ Notes

- Container restarts automatically on crash (Railway policy)
- Logs persist for 7 days in Railway
- Environment variables can be updated without rebuilding
- Health check runs every 30 seconds (automatic)
- SSL cert auto-generates if missing (self-signed, valid for 365 days)

---

## 🎯 Next Steps

1. ✅ Extract the archive
2. ✅ Install Railway CLI
3. ✅ Login to Railway
4. ✅ Run `railway init` and `railway up`
5. ✅ Get your public URL from Railway dashboard
6. ✅ Access panel and change admin password
7. ✅ Monitor logs: `railway logs --follow`

**You're ready to go! 🚀**

Any questions? Check the logs first: `railway logs`
