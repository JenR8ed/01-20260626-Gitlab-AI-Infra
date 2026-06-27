# AI Infrastructure Meetup — GitLab Self-Hosted Demo

Complete package for presenting self-hosted CI/CD for AI/ML applications.

## 🚀 Quick Start

**[View Interactive Demo](https://htmlpreview.github.io/?https://github.com/JenR8ed/01-20260626-Gitlab-AI-Infra/blob/main/gitlab-demo.html)** ← Click to run the pipeline walkthrough

## What's Included

- **gitlab-demo.html** — Interactive pipeline demo (test → build → deploy)
- **AI_Meetup_SkyPilot_Deployment_Guide.md** — Setup instructions
- **GitLab-AI-Infra-Setup.md** — Infrastructure configuration
- **Config-Reference.md** — CI/CD pipeline reference
- **Implementation-Steps.md** — Step-by-step deployment

## The Setup

- **Hardware:** 16GB RAM, 8 cores, 100GB NVMe (Proxmox VM)
- **Stack:** GitLab CE + Runner + Docker Registry
- **App:** ai-list-assist (FastAPI + Gemini AI)
- **Cost:** $0/month (vs $42 cloud) — ROI ~10 months

## Pipeline Stages
commit → lint → test → security scan → build docker image → staging deploy

Features:
- Automated testing (85% coverage) + security scanning
- Docker build & private registry push
- Webhook-triggered deployments
- All secrets stored encrypted in GitLab variables

## Key Benefit

**Self-hosted = no recurring SaaS costs + full control over AI/ML infrastructure**

---
*Note: Demo prepared for March 2026 AI Infrastructure Meetup (not presented due to transportation unavailable)*
