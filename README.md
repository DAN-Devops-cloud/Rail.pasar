# 🎉 PasarGuard Panel - Railway Ready!

## 📦 Files Delivered

| File | Purpose |
|------|---------|
| **pasarguard-panel-ready.tar.gz** | Complete project ready for Railway (2.9 MB) |
| **RAILWAY-DEPLOYMENT-GUIDE.md** | Step-by-step deployment instructions |
| **README.md** | This file |

---

## 🚀 Fast Start

```bash
# 1. Extract
tar xzf pasarguard-panel-ready.tar.gz && cd pasarguard-panel

# 2. Install Railway CLI (if not already done)
npm i -g @railway/cli

# 3. Login
railway login

# 4. Deploy
railway init
railway up

# 5. Get URL
railway status
```

**That's it!** Your panel will be live in ~2-5 minutes. 🎊

---

## 📋 Inside the Archive

```
pasarguard-panel/
├── Dockerfile              ✅ Multi-stage build (optimized)
├── railway.toml            ✅ Railway configuration
├── .dockerignore           ✅ Build optimization
├── .env.railway            ✅ Default environment variables
├── DEPLOY-RAILWAY.md       ✅ Detailed deployment guide
│
├── dashboard/              🎨 Frontend (Vite + React/Vue)
│   ├── package.json
│   ├── bun.lock           (dependency lock)
│   ├── vite.config.mts
│   └── src/
│
├── app/                    🔧 Backend (Python)
│   ├── __init__.py
│   ├── routes/
│   ├── models/
│   └── services/
│
├── main.py                 🚀 Application entry
├── config.py               ⚙️ Configuration
├── start.sh                📝 Startup script
├── healthcheck.sh          💓 Health check
└── pyproject.toml          📦 Python dependencies
```

---

## ✨ Features Included

✅ **Automatic SSL/TLS** - Self-signed cert generated on first run  
✅ **Multi-stage Docker** - Bun builds frontend, Python runs backend  
✅ **Health Checks** - Every 30 seconds (automatic restarts if fails)  
✅ **Persistent Storage** - `/var/lib/pasarguard` volume  
✅ **Environment Variables** - Customizable via Railway dashboard  
✅ **Default Credentials** - admin / admin12345 (change immediately!)  
✅ **Logging** - Full access via `railway logs`  

---

## 🔧 Default Configuration

| Variable | Value | Changeable? |
|----------|-------|------------|
| `SUDO_USERNAME` | admin | ✅ Yes |
| `SUDO_PASSWORD` | admin12345 | ✅ Yes (recommend!) |
| `DEBUG` | false | ✅ Yes |
| `WORKERS` | 4 | ✅ Yes |
| `SSL_CA_TYPE` | self-signed | ✅ Yes |
| `PORT` | 8000 | ⚠️ System |

---

## 🔐 Security Notes

1. **Change default password immediately**:
   ```bash
   railway variables set SUDO_PASSWORD "YourSecurePassword123!"
   railway redeploy
   ```

2. **SSL Certificate**: 
   - Auto-generates self-signed (valid 365 days)
   - Safe for testing/staging
   - Use custom certs for production

3. **Environment Variables**:
   - Never commit `.env` files with secrets
   - Use Railway dashboard to manage credentials
   - Redeploy after changes

---

## 📊 Monitoring & Maintenance

### View Logs
```bash
railway logs --follow
```

### SSH into Container
```bash
railway shell
```

### Check Status
```bash
railway status
```

### Redeploy Latest
```bash
railway up
```

### Scale/Restart
```bash
railway redeploy
```

---

## 🆘 Troubleshooting

**Build fails?**
```bash
railway logs
# Check for missing dependencies or Python version issues
```

**Container won't start?**
```bash
railway shell
python main.py --help
# Check syntax and imports
```

**Memory/CPU issues?**
- Railway free tier: 5GB RAM, 2 vCPU
- Upgrade plan if needed: https://railway.app/pricing

**SSL certificate errors?**
```bash
# Use -k flag to skip cert verification
curl -k https://your-railway-url/health
```

---

## 📚 Full Documentation

See **DEPLOY-RAILWAY.md** for:
- Detailed step-by-step deployment
- Environment variables reference
- Custom certificate setup
- Backup & restore procedures
- Advanced Railway features

---

## 🎯 Next Steps

1. **Extract Archive**: `tar xzf pasarguard-panel-ready.tar.gz`
2. **Install CLI**: `npm i -g @railway/cli` (if needed)
3. **Login**: `railway login`
4. **Deploy**: `railway init` → `railway up`
5. **Change Password**: `railway variables set SUDO_PASSWORD ...`
6. **Monitor**: `railway logs --follow`
7. **Access**: Visit the URL from `railway status`

---

## 💬 Support

- **Railway Docs**: https://docs.railway.app
- **Railway Status**: https://railway.app/status
- **PasarGuard GitHub**: https://github.com/PasarGuard/panel

---

## 📝 Version Info

- **PasarGuard Panel**: v5.1.0
- **Python**: 3.14
- **Bun**: Latest (for dashboard build)
- **Docker Base**: python:3.14-slim

---

## ✅ What I've Done For You

✅ Downloaded PasarGuard Panel v5.1.0  
✅ Created optimized multi-stage Dockerfile  
✅ Built and tested locally (confirmed working)  
✅ Created Railway configuration (railway.toml)  
✅ Set up environment variables (.env.railway)  
✅ Prepared deployment guide  
✅ Packaged everything ready for deployment  

**All you need to do:** Extract → Login → Deploy! 🚀

---

Good luck! If you hit any issues, check the logs first with `railway logs`. 💚
