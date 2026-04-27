Here is a clean, properly formatted, copy-paste ready `deployment.md` file:

```md
# Deployment Documentation (CI/CD)

## 🌍 Live Server
- **IP Address:** 196.188.187.153
- **User:** dev
- **Frontend Port:** 5000
- **Backend:** Node.js (PM2)

---

## 📁 Project Location on Server
```

/home/dev/project/webstack-cicd-project

```

---

## ⚙️ CI/CD Overview
Every push to `main` triggers GitHub Actions which:
- Connects to the server via SSH
- Pulls the latest code
- Builds backend and frontend
- Restarts services using PM2
- Serves the updated frontend

---

## 🔐 GitHub Secrets Required

Add these in:
GitHub Repo → **Settings → Secrets and variables → Actions**

### Required Secrets:
- `SERVER_HOST` = 196.188.187.153
- `SERVER_USER` = dev
- `SERVER_SSH_KEY` = (your private SSH key)

---

## 🔑 SSH Key Setup

### Server (public key stored on server under user `dev`)
Ensure your public key is added to:
```

~/.ssh/authorized_keys

````

---

## 🚀 Manual Deployment (Server)

### SSH into server
```bash
ssh dev@196.188.187.153
````

### Go to project directory

```bash
cd /home/dev/project/webstack-cicd-project
```

### Pull latest code

```bash
git pull origin main
```

---

## 🖥 Backend Deployment

```bash
cd backend
npm install
npm run build
pm2 restart backend || pm2 start dist/index.js --name backend
```

### Check status

```bash
pm2 status
```

### View logs

```bash
pm2 logs backend
```

---

## 🌐 Frontend Deployment

```bash
cd frontend
npm install
npm run build
npx serve -s dist -l 5000
```

---

## 🔁 GitHub Actions Workflow

Workflow file location:

```
.github/workflows/deploy.yml
```

---

## 🧪 How to Test CI/CD

```bash
git add .
git commit -m "test deployment"
git push origin main
```

Then check:

* GitHub → **Actions tab**

---

## 🌍 Live Application

```
http://196.188.187.153:5000
```

---

## 🛠 Troubleshooting

### SSH not working

* Check `SERVER_SSH_KEY`
* Check `SERVER_HOST`
* Ensure port `22` is open

### Backend issues

```bash
pm2 logs backend
```

### Frontend issues

```bash
npm run build
npx serve -s dist -l 5000
```
