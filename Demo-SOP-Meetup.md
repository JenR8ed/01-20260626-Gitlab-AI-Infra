# AI Infrastructure Meetup - Demo SOP
## 20-Minute Presentation Script

**Duration:** 12 min demo + 8 min Q&A  
**Focus:** Self-hosted CI/CD for AI applications

---

## PRE-EVENT CHECKLIST (24 hours before)

### Technical
- [ ] GitLab running: `docker ps | grep gitlab`
- [ ] Runner online: `docker exec -it gitlab-runner gitlab-runner verify`
- [ ] Test pipeline: Push dummy commit, verify completes
- [ ] Container registry: Check 10+ images exist
- [ ] **Record backup video** of full pipeline run

### Setup
- [ ] Laptop charged + adapter
- [ ] HDMI adapter tested
- [ ] Browser bookmarks: GitLab UI, Pipelines, Registry
- [ ] Terminal tabs: (1) GitLab logs, (2) Runner logs, (3) Working dir
- [ ] VS Code open to .gitlab-ci.yml
- [ ] Mobile hotspot as backup internet

---

## DEMO SCRIPT (12 minutes)

### Part 1: Hook (2 min)

**Opening:**
> "Show of hands: Using GitHub Actions for AI projects? Anyone been surprised by CI bills or had API keys leak? Today I'm showing $0/month ML infrastructure on my own hardware."

**Transition:**
- Screen share GitLab UI
- "This is running on a Proxmox VM in my home lab - 16GB RAM, 8 cores"

### Part 2: Architecture (2 min)

**Show docker-compose.yml in VS Code:**
> "Three services: GitLab CE, Runner, Container Registry. Total setup: 30 minutes. Let me show you production..."

**Navigate to GitLab UI:**
- Projects → AI-List-Assist
- "Multimodal AI app - takes product photos, generates eBay listings using Gemini"

### Part 3: Live Pipeline (5 min)

**Step 1:** Navigate to CI/CD → Pipelines (show recent success)

**Step 2:** Make code change in VS Code
```python
# app/main.py - add comment
# Demo: AI Infrastructure Meetup - March 2026
```

**Step 3:** Commit & push
```bash
git add app/main.py
git commit -m "feat: improve image processing"
git push gitlab main
```

**Step 4:** Watch pipeline (narrate as it runs)
```
Stage 1 - TEST (1 min):
  ✓ Lint: Ruff checks - 15s
  ✓ Tests: Pytest 85% coverage - 30s
  ✓ Security: Bandit scan - 20s

Stage 2 - BUILD (2 min):
  ✓ Docker build: FastAPI container - 2m
  ✓ Push: Registry with commit SHA - 30s

Stage 3 - DEPLOY (1 min):
  ✓ Staging: Webhook triggered - 1m
  ⏸ Production: Manual approval required
```

**Emphasize:**
- "API keys in GitLab variables - never touch cloud"
- "Private registry - no DockerHub limits"
- "4 minutes: commit → staging"

### Part 4: Container Registry (2 min)

**Navigate:** Packages & Registries → Container Registry

**Show:**
- "15+ versions, each tagged with commit SHA"
- Click latest → Show layers
- "Multi-stage build under 500MB"
- Pull command: `docker pull registry.local:5050/ai-list-assist:abc1234`

### Part 5: Cost Comparison (1 min)

```
GitHub Actions (1000 min/mo):  $8
GCP Registry (50GB):           $5
Managed GitLab:                $29
---
Self-Hosted:                   $0
Hardware (one-time):           $400
ROI:                           10 months
```

---

## BACKUP PLANS

### Plan A: Network Fails
- Switch to phone hotspot
- Continue with recorded video

### Plan B: GitLab Unresponsive
- Play backup video at 2x speed
- Narrate over it
- Skip to Q&A

### Plan C: Total Failure
- "Let's pivot to architecture discussion"
- Walk through docker-compose.yml in VS Code
- Explain .gitlab-ci.yml stages
- Extended Q&A

---

## Q&A PREP (8 min)

**Q: GPU workloads?**
→ "Second runner with nvidia-docker, tag jobs with `gpu`. GitLab routes automatically."

**Q: High availability?**
→ "For production: GitLab HA with multiple runners. For solo dev: single instance + nightly backups works fine. Restore: 20 min."

**Q: Security concerns?**
→ "Behind firewall, VPN-only access. All secrets in GitLab encrypted store. Add SSO via SAML/OAuth for teams."

**Q: vs Jenkins?**
→ "Jenkins needs plugin management. GitLab is batteries-included - registry, CI/CD, issues in one. YAML vs Groovy preference."

**Q: Maintenance?**
→ "Docker Compose makes updates easy: `pull && up -d`. Maybe 2 hours/month. Automated backups via cron."

**Q: Production use?**
→ "Yes - AI-List-Assist in production, real eBay listings. 30-40 deploys/month across 3 projects."

---

## POST-DEMO ACTIONS

### Immediately
- [ ] Share slides link in chat
- [ ] Share GitHub repo
- [ ] Connect with attendees on LinkedIn

### Within 24 Hours
- [ ] Post recording to YouTube
- [ ] Write blog post
- [ ] Share on X/LinkedIn with #AIInfrastructure

### Within 1 Week
- [ ] Follow up with interested people
- [ ] Update GitHub README with "As seen at..."
- [ ] Submit to other meetups

---

## SPEAKING TIPS

**Do:**
- ✅ Speak slowly (pause after technical points)
- ✅ Make eye contact across room
- ✅ Show enthusiasm for your work
- ✅ Admit "I don't know - I'll research that"

**Don't:**
- ❌ Apologize for setup
- ❌ Spend >1 min on broken demo (pivot!)
- ❌ Read slides verbatim
- ❌ Use undefined jargon
- ❌ Go over time

---

## FINAL CHECKLIST (5 min before)

- [ ] GitLab UI loaded and responsive
- [ ] Terminal windows positioned
- [ ] VS Code open to .gitlab-ci.yml
- [ ] Phone on silent (hotspot ready)
- [ ] Water bottle in reach
- [ ] **Deep breath - you've got this!**

---

**Good luck! 🚀**
