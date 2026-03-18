# 🚀 DevOps Platform (Docker + Kubernetes + Observability)

Демонстрационный DevOps-проект, показывающий развёртывание контейнеризированного приложения, настройку мониторинга, логирования и оркестрации с использованием Kubernetes.

---

# 📦 Стек технологий

## 🐳 Контейнеризация

* Docker
* Docker Compose

## ☸️ Оркестрация

* Kubernetes (Minikube)

## 📊 Мониторинг

* Prometheus (Helm)
* Grafana (Helm)
* Node Exporter
* cAdvisor

## 📜 Логирование

* Loki
* Grafana Alloy

## 🔁 CI/CD

* GitHub Actions

## ⚙️ IaC / Automation (в процессе)

* Terraform
* Ansible

---


# 📁 Структура проекта

```
DevOps-Platform
│
├── app/                  # Flask приложение
├── nginx/                # конфиг nginx
├── monitoring/           # Prometheus / Alertmanager config
├── logging/              # Alloy config
│
├── docker-compose.yml    # локальный запуск
│
├── k8s/                  # Kubernetes манифесты
│   ├── namespace.yaml
│   ├── app-deployment.yaml
│   ├── app-service.yaml
│   ├── ingress.yaml
│   ├── hpa.yaml
│   └── servicemonitor.yaml
│
└── .github/workflows     # CI/CD
```

---

# ⚙️ Функционал проекта

## ✅ Реализовано

### Docker

* Контейнеризация приложения
* Reverse proxy (Nginx)
* Monitoring stack
* Logging stack

### Kubernetes

* Deployment
* Service
* Ingress
* Namespace
* Horizontal Pod Autoscaler (HPA)

### Observability

* Prometheus через Helm
* Grafana через Helm
* ServiceMonitor
* Метрики приложения (`/metrics`)

### Приложение

* Flask app
* Prometheus metrics (prometheus-client)

---

# 🚀 Запуск проекта

---

## 🐳 1. Локально через Docker Compose

```bash
docker compose up -d
```

Доступ:

* App: http://localhost:8080
* Grafana: http://localhost:3000
* Prometheus: http://localhost:9090

---

## ☸️ 2. Kubernetes (Minikube)

### Запуск кластера

```bash
minikube start
minikube addons enable ingress
minikube addons enable metrics-server
```

---

### Сборка образа

```bash
docker build -t devops-platform:latest ./app
minikube image load devops-platform:latest
```

---

### Деплой

```bash
kubectl apply -f k8s/
```

---

### Проверка

```bash
kubectl get pods -n devops-platform
```

---

### Доступ к приложению

```bash
kubectl port-forward svc/demo-app-service 8080:80 -n devops-platform
```

Открыть:

```
http://localhost:8080
```

---

# 📊 Мониторинг (Kubernetes)

---

## Установка Prometheus + Grafana

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

kubectl create namespace monitoring

helm install monitoring prometheus-community/kube-prometheus-stack -n monitoring
```

---

## Доступ к Grafana

```bash
kubectl port-forward svc/monitoring-grafana 3000:80 -n monitoring
```

```
http://localhost:3000
```

Логин:

```
admin
```

Пароль:

```bash
kubectl get secret monitoring-grafana -n monitoring -o jsonpath="{.data.admin-password}" | base64 -d
```

---

## Доступ к Prometheus

```bash
kubectl port-forward svc/monitoring-kube-prometheus-prometheus 9090:9090 -n monitoring
```

```
http://localhost:9090
```

---

# 📈 Метрики приложения

Flask приложение поддерживает:

```
/metrics
```

Пример метрики:

```
app_requests_total
```

---

# 🔄 Автоскейлинг (HPA)

```bash
kubectl get hpa -n devops-platform
```

Логика:

```
CPU > 70% → scale up
CPU < 70% → scale down
```

---

# 🧠 Что демонстрирует проект

* Контейнеризация приложений
* Kubernetes orchestration
* Observability (metrics + logs)
* Autoscaling
* Service discovery
* Monitoring через Helm



