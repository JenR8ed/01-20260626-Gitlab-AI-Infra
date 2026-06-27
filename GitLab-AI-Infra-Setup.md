# GitLab Self-Hosted for AI Infrastructure
## 30-Minute Setup Guide - Optimized for Meetup Demo

**Target:** AI/ML Engineers, Infrastructure Teams  
**Hardware:** Proxmox VM (16GB RAM, 8 cores, 100GB NVMe)  
**OS:** Ubuntu 22.04 LTS

---

## Quick Deploy

### Install Docker
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh && sudo usermod -aG docker $USER
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

### Setup GitLab
```bash
export GITLAB_HOME=/srv/gitlab
sudo mkdir -p $GITLAB_HOME/{config,logs,data,runner-config}
sudo chown -R $USER:$USER $GITLAB_HOME
cd $GITLAB_HOME
```

### docker-compose.yml
```yaml
version: '3.7'
services:
  gitlab:
    image: 'gitlab/gitlab-ce:latest'
    container_name: gitlab
    restart: always
    hostname: 'gitlab.local'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://gitlab.local'
        gitlab_rails['gitlab_shell_ssh_port'] = 2424
        registry_external_url 'http://registry.local:5050'
        gitlab_rails['registry_enabled'] = true
        postgresql['shared_buffers'] = "256MB"
        sidekiq['max_concurrency'] = 25
    ports:
      - '80:80'
      - '443:443'
      - '2424:22'
      - '5050:5050'
    volumes:
      - '$GITLAB_HOME/config:/etc/gitlab'
      - '$GITLAB_HOME/logs:/var/log/gitlab'
      - '$GITLAB_HOME/data:/var/opt/gitlab'
    shm_size: '256m'
    networks:
      - gitlab-network

  gitlab-runner:
    image: 'gitlab/gitlab-runner:alpine'
    container_name: gitlab-runner
    restart: always
    depends_on:
      - gitlab
    volumes:
      - '/var/run/docker.sock:/var/run/docker.sock'
      - '$GITLAB_HOME/runner-config:/etc/gitlab-runner'
    networks:
      - gitlab-network

networks:
  gitlab-network:
    driver: bridge
```

### Launch
```bash
docker-compose up -d
docker logs -f gitlab  # Wait for "Reconfigured!"
docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
```

### Register Runner
```bash
# Get token from: Admin Area → CI/CD → Runners
docker exec -it gitlab-runner gitlab-runner register \
  --non-interactive \
  --url "http://gitlab.local" \
  --registration-token "GR1348941..." \
  --executor "docker" \
  --docker-image "python:3.11-slim" \
  --description "ai-ml-runner" \
  --tag-list "docker,python,ml" \
  --run-untagged="true"
```

---

## Demo Pipeline (.gitlab-ci.yml)

```yaml
image: python:3.11-slim

stages:
  - test
  - build
  - deploy

lint:
  stage: test
  script:
    - pip install ruff black
    - ruff check .
    - black --check .
  tags:
    - docker

unit-tests:
  stage: test
  script:
    - pip install -r requirements.txt pytest
    - pytest tests/
  tags:
    - docker

build-docker:
  stage: build
  image: docker:latest
  services:
    - docker:dind
  script:
    - docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY
    - docker build -t $CI_REGISTRY_IMAGE:$CI_COMMIT_SHORT_SHA .
    - docker push $CI_REGISTRY_IMAGE:$CI_COMMIT_SHORT_SHA
  only:
    - main
  tags:
    - docker

deploy-staging:
  stage: deploy
  script:
    - curl -X POST $DEPLOY_WEBHOOK_URL
  only:
    - main
  tags:
    - docker
```

---

## Key Metrics

- **Pipeline Time:** 4-6 minutes (commit → staging)
- **Cost:** $0/month (vs $500+/year cloud)
- **Security:** API keys never leave infrastructure
- **Scale:** Unlimited CI minutes, no rate limits

---

## Commands

```bash
# Health check
docker exec -it gitlab gitlab-rake gitlab:check

# Runner status
docker exec -it gitlab-runner gitlab-runner verify

# Logs
docker logs -f gitlab
docker logs -f gitlab-runner

# Restart
docker-compose restart gitlab
```

---

**Demo Ready! 🚀**
