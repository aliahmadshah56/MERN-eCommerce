# MERN eCommerce — Kubernetes

Kubernetes deployment configuration for the **MERN eCommerce application**, including application services, persistent MongoDB storage, and monitoring with Prometheus and Grafana.

## Architecture

```text
                    ┌──────────────┐
                    │   Frontend   │
                    │ React + Nginx│
                    └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │   Backend    │
                    │ Node + Express│
                    └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │   MongoDB    │
                    │  StatefulSet │
                    │  + PVC       │
                    └──────────────┘

              ┌─────────────────────┐
              │      Monitoring     │
              │ Prometheus → Grafana│
              └─────────────────────┘
```

## Components

* **Frontend** — React application served through Nginx
* **Backend** — Node.js/Express API
* **MongoDB** — StatefulSet with persistent storage
* **Prometheus** — Metrics collection
* **Grafana** — Monitoring dashboards
* **Kind** — Local Kubernetes cluster configuration

## Directory Structure

```text
k8s/
├── kind/
├── prometheus/
├── back-end-deployment.yml
├── back-end-service.yml
├── front-end-deployment.yml
├── front-end-service.yml
├── mongo-db-service.yml
├── mongo-db-statefulset.yml
├── mongo-db-volume.yml
├── prometheus-deployment.yml
├── prometheus-service.yml
├── grafana-deployment.yml
└── grafana-service.yml
```

## Deployment

Create the Kind cluster using the configuration in `kind/`, then deploy the Kubernetes resources:

```bash
kubectl apply -f .
```

Verify the deployment:

```bash
kubectl get pods
kubectl get svc
kubectl get pvc
```

## MongoDB

The backend connects to MongoDB through the Kubernetes Service:

```text
mongodb://mongodb:27017/mernecommerce
```

MongoDB data is persisted using a **PersistentVolumeClaim**.

## Monitoring

Prometheus collects application/cluster metrics and Grafana provides visualization dashboards.

Check monitoring components:

```bash
kubectl get pods | grep -E "prometheus|grafana"
```

## Troubleshooting

```bash
kubectl logs <pod-name>
kubectl describe pod <pod-name>
kubectl get events --sort-by=.lastTimestamp
```

Check MongoDB service connectivity:

```bash
kubectl get svc mongodb
kubectl get endpoints mongodb
```

## Cleanup

```bash
kubectl delete -f .
```

---

**Technologies:** Kubernetes • Kind • Docker • React • Nginx • Node.js • Express • MongoDB • Prometheus • Grafana
