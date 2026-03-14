# DevOps Platform

Демонстрационная DevOps-платформа, показывающая развёртывание контейнеризированного приложения, настройку reverse proxy, мониторинг и централизованное логирование.

Проект имитирует production-инфраструктуру с использованием Docker и observability stack.

---


# Используемые технологии

* Linux
* Docker
* Docker Compose
* Nginx (Reverse Proxy)
* Prometheus (Monitoring)
* Grafana (Metrics Visualization)
* Loki (Centralized Logging)
* GitHub Actions (CI Pipeline)



---

# Сервисы платформы

## Application

Простое веб-приложение, запущенное в Docker-контейнере.


---

## Reverse Proxy

Nginx используется как reverse proxy для маршрутизации входящих HTTP-запросов.

```
Client → Nginx → Application
```

---

# Monitoring Stack

Метрики инфраструктуры собираются с помощью Prometheus.

Node Exporter предоставляет системные метрики:

* CPU
* RAM
* Disk
* Network

Prometheus собирает метрики и передаёт их в Grafana для визуализации.

---

# Logging Stack

Логи контейнеров собираются через Docker logging driver и отправляются в Loki.

Grafana используется для просмотра и анализа логов.

Пример запроса Loki:

```
{compose_service="reverse_proxy"}
```

Поиск ошибок:

```
{compose_service="reverse_proxy"} |= "error"
```

---

# Grafana Auto Provisioning

Grafana автоматически настраивает:

* источники данных (Prometheus и Loki)
* dashboards

Это реализовано через provisioning.

---

# CI Pipeline

В проекте используется GitHub Actions.

Pipeline автоматически запускается при push в ветку main.



---

# Запуск проекта

Клонировать репозиторий:

```
git clone https://github.com/Kickkenberg/DevOps-Platform.git
```

Перейти в директорию проекта:

```
cd devops-platform
```

Запустить платформу:

```
docker compose up -d
```

---

# Доступ к сервисам

Application

```
http://localhost:8080
```

Grafana

```
http://localhost:3000
```

Prometheus

```
http://localhost:9090
```

---

# DevOps практики, реализованные в проекте

* контейнеризация приложений
* multi-container архитектура
* reverse proxy
* monitoring stack
* centralized logging
* CI pipeline
* infrastructure automation
* observability platform
