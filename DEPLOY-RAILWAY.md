# PasarGuard Panel - Railway Deployment

## Quick Start

### Prerequisites
- Railway account: https://railway.app
- Railway CLI installed: https://docs.railway.app/develop/cli

### Deployment Steps

#### 1. Install Railway CLI
```bash
npm i -g @railway/cli
# or
curl -fsSL https://railway.app/install.sh | bash
```

#### 2. Login to Railway
```bash
railway login
```

#### 3. Clone / Prepare Repository
```bash
cd pasarguard-panel
git init
git add .
git commit -m "Initial commit"
```

#### 4. Create Railway Project
```bash
railway init
# Follow prompts:
# - Project name: "pasarguard-panel" (or your choice)
# - Environment: "production"
```

#### 5. Set Environment Variables (Optional)
If you want to customize before deploy:
```bash
railway variables set SUDO_USERNAME admin
railway variables set SUDO_PASSWORD your-secure-password
railway variables set DEBUG false
railway variables set WORKERS 4
```

#### 6. Deploy
```bash
railway up
```

Railway will:
1. Detect `Dockerfile` and build the image
2. Create a volume for `/var/lib/pasarguard`
3. Expose the service on a public URL
4. Start the container

#### 7. Monitor Logs
```bash
railway logs
```

#### 8. Get Public URL
```bash
railway status
# or check the Railway dashboard at https://railway.app
```

---

## Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `PYTHONUNBUFFERED` | `1` | Unbuffered Python output |
| `DEBUG` | `false` | Enable debug mode |
| `SUDO_USERNAME` | `admin` | Default admin username |
| `SUDO_PASSWORD` | `admin12345` | Default admin password (change this!) |
| `WORKERS` | `4` | Number of worker processes |
| `SSL_CA_TYPE` | `self-signed` | Certificate type (self-signed / custom) |
| `PORT` | `8000` | Internal port (Railway maps to external) |

### Custom Certificates (Optional)
If you want to use your own SSL certificates:

1. Upload cert files to Railway
2. Set in Railway dashboard:
   ```
   SSL_CERT_FILE=/path/to/cert.pem
   SSL_KEY_FILE=/path/to/key.pem
   SSL_CA_TYPE=custom
   ```

---

## Docker Build Details

The `Dockerfile` uses multi-stage builds:
1. **Stage 1**: Builds the Vite dashboard using Bun
2. **Stage 2**: Creates Python runtime and combines both

Total size: ~650MB (optimized with slim base image)

---

## Volumes & Persistence

Railway creates a volume at `/var/lib/pasarguard` for persistent storage.

To access:
```bash
railway shell
ls -la /var/lib/pasarguard
```

---

## Health Check

The container includes a health check endpoint:
- **HTTP**: `http://your-railway-url:8000/health`
- **Interval**: 30 seconds
- **Timeout**: 5 seconds
- **Retries**: 3

---

## Troubleshooting

### Build Fails
```bash
railway logs --follow
# Check for missing dependencies or syntax errors
```

### Container Crashes
```bash
railway shell
cat /var/log/pasarguard.log
```

### Memory Issues
If you see OOM errors, Railway offers paid plans with more memory:
https://railway.app/pricing

---

## Cleanup

To delete the Railway project:
```bash
railway down
```

---

## Support & Documentation
- Railway Docs: https://docs.railway.app
- PasarGuard: https://github.com/PasarGuard/panel
