# Configuration Files Reference

## docker-compose.yml

version: 3.7
services:
  gitlab:
    image: gitlab/gitlab-ce:latest
    container_name: gitlab
    ports: [80:80, 443:443, 2424:22]

## .gitlab-ci.yml

stages: [test, build, deploy]
lint:
  script: [pip install ruff, ruff check .]

## Commands

Start: docker-compose up -d
Status: docker ps
Logs: docker logs -f gitlab

See full docs in GitLab-AI-Infra-Setup.md
