The last piece you need for a professional showing at the **AI Infra Meetup** is a developer-facing guide. This file (often named CONTRIBUTING.md or SKYPILOT.md) shows other engineers exactly how to spin up your environment in the cloud using the **SkyPilot** spec we created.

Since you're using **WSL2**, this guide is written to bridge the gap between your local Ubuntu terminal and a high-performance **CoreWeave** instance.

### ---

**\#\# SKYPILOT\_GUIDE.md**

Markdown

\# ☁️ SkyPilot Deployment Guide for AI List Assist

This project is optimized for deployment on distributed cloud infrastructure via **\*\*SkyPilot\*\***. This allows us to run our heavy asynchronous agents on high-performance GPUs (like NVIDIA L4s) across **\*\*CoreWeave\*\***, **\*\*Lambda\*\***, or **\*\*GCP\*\***.

\#\# 🚀 One-Click Cloud Launch

If you have SkyPilot configured, you can launch the entire stack (API \+ Worker \+ Redis) from your local **\*\*WSL2\*\*** terminal with:

\`\`\`bash  
sky launch \-c ai-cluster sky-deploy.yaml

### **What happens under the hood:**

1. **Provisioning:** SkyPilot finds the cheapest available GPU/CPU instance (prioritizing CoreWeave/GCP).  
2. **Syncing:** Your local workdir (synced from WSL2) is automatically uploaded to the remote VM.  
3. **Setup:** The remote instance installs **Docker** and builds the containers defined in our docker-compose.yml.  
4. **Execution:** The FastAPI server starts on port 8000\.

## **🛠️ Common CLI Commands**

| Command | Purpose |
| :---- | :---- |
| sky status | Check the health and IP of your active clusters. |
| sky tail ai-cluster | Stream logs from the remote containers. |
| sky stop ai-cluster | Pause the instance to save costs (disk remains). |
| sky down ai-cluster | Fully terminate the instance and delete all data. |

## **📡 Accessing the Demo**

Once launched, SkyPilot will provide a public IP. You can access your frontend at:

http://\<CLUSTER\_IP\>:8000/static/index.html

## **🧠 Scaling with SkyServe (Beta)**

To handle high-traffic periods (like an r/AI\_Agents Demo Day), we use **SkyServe** for automatic load balancing across multiple replicas:

Bash

sky serve up \-n ai-service sky-deploy.yaml

\---

\#\#\# 🎨 Visualizing Your Stack  
To help Jules or the meetup engineers understand your "Modern Pattern" architecture, you can describe it as a \*\*Distributed Agentic Workflow\*\*.

\---

\#\#\# 🎒 Final "SF Meetup" Checklist  
1\. \*\*The Pitch:\*\* You're building a niche, high-accuracy agent for collectibles.  
2\. \*\*The Demo:\*\* Use your \*\*WSL2\*\* browser to show the FastAPI \+ Chart.js frontend.  
3\. \*\*The Infra:\*\* Show the \`sky-deploy.yaml\` to prove you can move from a laptop to a 100-node cluster in one command.

\*\*Your Next Step:\*\*  
Since the SF Meetup is on \*\*Wednesday\*\*, would you like me to draft a quick \*\*"30-second intro"\*\* you can use when you meet the SkyPilot or CoreWeave developers? It'll help you jump straight into the technical conversation.  
