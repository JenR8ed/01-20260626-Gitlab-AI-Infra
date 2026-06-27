# AI Infrastructure Meetup - GitLab Self-Hosted Demo

Complete package for presenting self-hosted CI/CD for AI/ML applications.

## 📦 Package Contents

1. **GitLab-AI-Infrastructure-Setup.md** - 30-minute deployment guide
2. **Demo-SOP-Guide.md** - Presentation script with Q&A prep  
3. **docker-compose.yml** - GitLab CE + Runner deployment
4. **gitlab-ci.yml** - Production AI pipeline example
5. **Dockerfile** - Multi-stage FastAPI container
6. **setup.sh** - Automated setup script
7. **DEMO-QUICK-REFERENCE.md** - Print-ready cheat sheet
8. **README.md** - This file

## 🚀 Quick Start

```bash
# Run automated setup
chmod +x setup.sh
./setup.sh

# Access GitLab at http://localhost
# Username: root
# Password: (displayed by script)
```

## 📊 Demo Focus (12 minutes)

1. **Live Pipeline Demo** - Commit → Test → Build → Deploy (4-6 min)
2. **Container Registry** - Versioned ML model artifacts (2 min)  
3. **Cost Comparison** - $0/month vs $500+/year cloud (1 min)

## 🎯 Key Messages

- "API keys never leave your infrastructure"
- "4-minute deploy time: commit → staging"  
- "16GB VM replaces GitHub Actions + GCP Registry"
- "Docker-in-Docker for ML workload isolation"

## 🔧 Prerequisites

- Ubuntu 22.04 LTS on Proxmox VM
- 16GB RAM, 8 cores, 100GB NVMe
- Docker + Docker Compose installed

## 📋 Pre-Demo Checklist

- [ ] Run setup.sh 24 hours before
- [ ] Test pipeline 3+ times
- [ ] Record backup video
- [ ] Verify runner online
- [ ] Organize browser bookmarks
- [ ] Mobile hotspot as backup

## 🐛 If Demo Fails

- **Plan A:** Switch to phone hotspot
- **Plan B:** Play backup video at 2x
- **Plan C:** Walk through architecture

## 📚 See Full Documentation

- Read **Demo-SOP-Guide.md** for complete script
- Read **GitLab-AI-Infrastructure-Setup.md** for technical details
- Print **DEMO-QUICK-REFERENCE.md** for laptop reference

---

**Good luck! 🚀**
