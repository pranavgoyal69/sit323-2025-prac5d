# SIT323/SIT737 - 5.2D: Cloud Microservice Deployment

![Google Cloud](https://img.shields.io/badge/Google_Cloud-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)

## 📋 Deployment Summary
**Published Image**:  
`us-central1-docker.pkg.dev/sit323-25t1-goyal-a326b43/my-docker-repo/my-microservice:v1`

## 🚀 Quick Deployment

### 1. Authenticate with GCP
```bash
gcloud auth login
gcloud auth configure-docker us-central1-docker.pkg.dev

2. Run the Published Microservice
bash

docker run -p 3000:3000 us-central1-docker.pkg.dev/sit323-25t1-goyal-a326b43/my-docker-repo/my-microservice:v1
Access: http://localhost:3000

🔧 Complete Implementation Steps
A. Build & Tag
bash

docker build -t us-central1-docker.pkg.dev/sit323-25t1-goyal-a326b43/my-docker-repo/my-microservice:v1 .
B. Push to Registry
bash

docker push us-central1-docker.pkg.dev/sit323-25t1-goyal-a326b43/my-docker-repo/my-microservice:v1
C. Verify
bash

# List image versions
gcloud artifacts docker tags list us-central1-docker.pkg.dev/sit323-25t1-goyal-a326b43/my-docker-repo/my-microservice

# Test fresh deployment
docker run --rm -it -p 3000:3000 us-central1-docker.pkg.dev/sit323-25t1-goyal-a326b43/my-docker-repo/my-microservice:v1
📂 Files Included

.
├── app/
│   ├── server.js         # Microservice code
│   └── package.json     # Dependencies
├── Dockerfile           # Production build
├── .dockerignore        # Exclusion rules
└── README.md            # This file
🛠️ Dockerfile
dockerfile

FROM node:16-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install --production
COPY . .
EXPOSE 3000
USER node
CMD ["node", "server.js"]
