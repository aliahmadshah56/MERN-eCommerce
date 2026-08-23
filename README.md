# MERN eCommerce — DevOps Project

A full-stack **MERN eCommerce application** containerized with **Docker**, orchestrated with **Docker Compose and Kubernetes (Kind)**, and monitored using **Prometheus & Grafana**.

## 🚀 Overview

This project demonstrates a practical DevOps workflow:

**MERN Application → Docker → Docker Compose → Kubernetes → Monitoring**

### Application Features

* Shopping cart, product search, pagination, reviews & ratings
* User authentication, profiles and order history
* Admin dashboard for users, products, orders and admins
* Razorpay payment integration
* Email functionality
* Database seeding

### DevOps Stack

| Area            | Technology                       |
| --------------- | -------------------------------- |
| Application     | React, Node.js, Express, MongoDB |
| Containers      | Docker                           |
| Orchestration   | Docker Compose, Kubernetes       |
| Kubernetes      | Kind                             |
| Web Server      | Nginx                            |
| Storage         | Kubernetes PVC                   |
| Monitoring      | Prometheus, Grafana              |
| Version Control | Git, GitHub                      |

---

## 🏗️ Architecture

```text
                 ┌───────────────┐
                 │ React + Nginx │
                 │   Frontend    │
                 └───────┬───────┘
                         │
                         ▼
                 ┌───────────────┐
                 │ Node + Express│
                 │    Backend    │
                 └───────┬───────┘
                         │
                         ▼
                 ┌───────────────┐
                 │    MongoDB    │
                 │ StatefulSet   │
                 │     + PVC     │
                 └───────────────┘

              Prometheus ──► Grafana
```

---

## 📁 Structure

```text
MERN-eCommerce/
├── backend/                  # Node.js / Express API
├── frontend/                 # React application
├── k8s/                      # Kubernetes manifests
│   ├── kind/config.yml
│   ├── prometheus/
│   ├── *-deployment.yml
│   ├── *-service.yml
│   └── mongo-db-*.yml
├── monitoring/               # Monitoring configuration
├── uploads/                  # Product images
├── docker-compose.yml
└── README.md
```

---

## ⚙️ Local Development

```bash
git clone https://github.com/aliahmadshah56/MERN-eCommerce.git
cd MERN-eCommerce

npm install
cd frontend && npm install && cd ..
npm run dev
```

Backend only:

```bash
npm run server
```

Create `.env` with your MongoDB, JWT, Razorpay and email credentials. **Never commit secrets to Git.**

---

## 🐳 Docker

Build images:

```bash
docker build -t mern-backend ./backend
docker build -t mern-frontend ./frontend
```

Run:

```bash
docker run -d -p 5000:5000 mern-backend
docker run -d -p 3000:80 mern-frontend
```

Useful commands:

```bash
docker ps
docker logs <container>
docker exec -it <container> sh
```

---

## 🐳 Docker Compose

Start the application stack:

```bash
docker compose up -d
```

Useful commands:

```bash
docker compose ps
docker compose logs -f
docker compose up -d --build
docker compose down
```

---

## ☸️ Kubernetes

Create the Kind cluster:

```bash
kind create cluster --config k8s/kind/config.yml
```

Deploy:

```bash
kubectl apply -f k8s/
```

Verify:

```bash
kubectl get pods
kubectl get svc
kubectl get pvc
```

### Kubernetes Components

* Frontend Deployment + Service
* Backend Deployment + Service
* MongoDB StatefulSet + Service
* PersistentVolumeClaim
* Prometheus Deployment + Service
* Grafana Deployment + Service

MongoDB is accessed through Kubernetes DNS:

```text
mongodb://mongodb:27017/mernecommerce
```

---

## 📊 Monitoring

**Prometheus** collects metrics and **Grafana** visualizes them.

```text
Kubernetes / Application
          ↓
      Prometheus
          ↓
       Grafana
```

Check:

```bash
kubectl get pods | grep -E "prometheus|grafana"
kubectl get svc | grep -E "prometheus|grafana"
```

---

## 🔍 Troubleshooting

```bash
kubectl get pods
kubectl logs <pod>
kubectl logs <pod> --previous
kubectl describe pod <pod>
kubectl get events --sort-by=.lastTimestamp
kubectl get svc
kubectl get endpoints
```

Test service connectivity:

```bash
kubectl exec -it <pod> -- sh
nc -zv mongodb 27017
```

Useful for diagnosing:

`CrashLoopBackOff` • `ImagePullBackOff` • `ECONNREFUSED` • Service/DNS issues • Pod connectivity

---

## 🌱 Database Seeder

```bash
npm run data:import
npm run data:destroy
```

---

## 🧹 Cleanup

```bash
kubectl delete -f k8s/
kind delete cluster
docker compose down
```

---

## 🎯 DevOps Concepts

**Git/GitHub • Docker • Docker Compose • Kubernetes • Kind • Deployments • Services • StatefulSets • Persistent Storage • Kubernetes Networking • Service Discovery • Prometheus • Grafana • Troubleshooting**

**Ali Ahmad Shah**
[GitHub — aliahmadshah56](https://github.com/aliahmadshah56?utm_source=chatgpt.com)


