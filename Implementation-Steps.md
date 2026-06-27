# Complete Implementation Guide

## 1. Install Docker
```bash
curl -fsSL https://get.docker.com | sudo sh
sudo usermod -aG docker $USER
```

## 2. Deploy GitLab
```bash
export GITLAB_HOME=/srv/gitlab
sudo mkdir -p $GITLAB_HOME/{config,logs,data}
cd $GITLAB_HOME
# Add docker-compose.yml
docker-compose up -d
```

## 3. Get Password
```bash
docker exec gitlab grep Password /etc/gitlab/initial_root_password
```

## 4. Register Runner
```bash
docker exec -it gitlab-runner gitlab-runner register \
  --url "http://gitlab.local" \
  --executor "docker" \
  --docker-image "python:3.11-slim"
```

## Commands
```bash
# Status
docker ps | grep gitlab
docker exec -it gitlab-runner gitlab-runner verify

# Logs
docker logs -f gitlab

# Restart
docker-compose restart
```

See GitLab-AI-Infra-Setup.md for full details
