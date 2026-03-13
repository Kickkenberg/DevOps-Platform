# DevOps Platform

Демонстрационный DevOps-проект, показывающий развёртывание контейнеризированного приложения, настройку reverse proxy и базовый мониторинг системы.

---

# Используемые технологии

- Linux
- Docker
- Docker Compose
- Nginx (Reverse Proxy)
- Prometheus (Monitoring)
- Grafana (Metrics)
- GitHub Actions (ci.yml)

---

# Сервисы

## Приложение
Простое веб-приложение, запущенное внутри Docker-контейнера.

## Reverse Proxy
Nginx используется как reverse proxy для обработки входящих запросов и передачи их в контейнер приложения.

**Схема работы**

```
client → nginx → app
```

---

# Мониторинг

Для мониторинга используется **Prometheus**.  
Он собирает метрики с сервисов платформы.

Prometheus собирает показатели из сервисов и **Node Exporter**.

**Grafana** используется для визуализации системных показателей, таких как:

- загрузка процессора
- использование памяти
- дисковый ввод-вывод
- сетевой трафик

---

# Запуск проекта

## Клонировать репозиторий

```bash
git clone https://github.com/Kickkenberg/DevOps-Platform.git
```

## Перейти в директорию проекта

```bash
cd devops-platform
```

## Запустить платформу

```bash
docker compose up -d
```

## Проверить контейнеры

```bash
docker ps
```

---

# Доступ к сервисам

**Приложение**  
http://localhost:8080

**Prometheus**  
http://localhost:9090

**Grafana**  
http://localhost:3000

**Metrics**  
http://localhost:9100/metrics

---

# CI Pipeline (GitHub Actions)

В проекте реализован **CI pipeline** с использованием GitHub Actions.  
Pipeline автоматически запускается при каждом **push** в ветку `master`.

Основная задача pipeline — проверить, что приложение успешно собирается в **Docker-образ**.

## Зачем нужен CI pipeline

- автоматически проверяет сборку приложения
- проверяет корректность работы Dockerfile
- помогает обнаружить ошибки до деплоя
