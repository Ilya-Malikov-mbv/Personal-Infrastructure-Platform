# VPS Infrastructure Platform

Современная инфраструктура для размещения веб-приложений на VPS с использованием Docker, Nginx и собственного стека мониторинга.

Проект представляет собой полностью настроенный сервер с HTTPS, обратным прокси, автоматическим развёртыванием через GitHub Actions, мониторингом инфраструктуры и сервисов, а также защищенным удаленным доступом через собственный VPN.

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Docker Compose](https://img.shields.io/badge/Docker%20Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white)
![Uptime Kuma](https://img.shields.io/badge/Uptime%20Kuma-5CDD8B?style=for-the-badge&logo=uptimekuma&logoColor=black)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-121011?style=for-the-badge&logo=gnubash&logoColor=white)
![SSH](https://img.shields.io/badge/SSH-222222?style=for-the-badge&logo=openssh&logoColor=white)
![Amnezia VPN](https://img.shields.io/badge/Amnezia%20VPN-1E88E5?style=for-the-badge)

---

# Архитектура

```mermaid
flowchart TB

    User["👤 Пользователь"]

    Nginx["Nginx<br/>Reverse Proxy"]

    Site["mal-mbv.ru"]

    Grafana["grafana.mal-mbv.ru"]

    Kuma["status.mal-mbv.ru"]

    Docker["Docker Engine"]

    Prometheus["Prometheus"]

    Exporter["Node Exporter"]

    VPS["Ubuntu Server 24.04 LTS"]

    User --> Nginx

    Nginx --> Site
    Nginx --> Grafana
    Nginx --> Kuma

    Grafana --> Prometheus
    Prometheus --> Exporter

    Site -. Static files .-> VPS

    Grafana -. Container .-> Docker
    Prometheus -. Container .-> Docker
    Kuma -. Container .-> Docker

    Exporter -. Installed on host .-> VPS
```

---

# Реализовано

- размещение веб-приложений на VPS;
- Reverse Proxy на базе Nginx;
- HTTPS для всех сервисов с использованием Let's Encrypt;
- контейнеризация сервисов с помощью Docker Compose;
- настройка собственного VPN-сервера на базе Amnezia VPN;
- защищенное подключение к инфраструктуре с различных устройств через приложение Amnezia;
- мониторинг ресурсов сервера через Prometheus и Node Exporter;
- визуализация метрик в Grafana;
- мониторинг доступности сервисов через Uptime Kuma;
- автоматический деплой через GitHub Actions;
- защита SSH с использованием Fail2Ban;
- изоляция внутренних сервисов от внешней сети;
- подробная техническая документация проекта.

---

# Используемые технологии

| Категория         | Технологии              |
| ----------------- | ----------------------- |
| ОС                | Ubuntu Server 24.04 LTS |
| Web Server        | Nginx                   |
| Контейнеризация   | Docker, Docker Compose  |
| CI/CD             | GitHub Actions          |
| Мониторинг        | Prometheus              |
| Экспорт метрик    | Node Exporter           |
| Визуализация      | Grafana                 |
| Uptime Monitoring | Uptime Kuma             |
| SSL               | Let's Encrypt           |
| Защита SSH        | Fail2Ban                |
| Контроль версий   | Git, GitHub             |
| VPN-доступ        | Amnezia VPN             |

---

# Развёрнутые сервисы

| Адрес                  | Назначение    |
| ---------------------- | ------------- |
| **mal-mbv.ru**         | основной сайт |
| **grafana.mal-mbv.ru** | Grafana       |
| **status.mal-mbv.ru**  | Uptime Kuma   |

---

# CI/CD

Для автоматизации развёртывания используется GitHub Actions.

После каждого изменения в основной ветке репозитория автоматически выполняется:

```text
        Push в main
             │
             ▼
       GitHub Actions
             │
             ▼
     Подключение по SSH
             │
             ▼
          git pull
             │
             ▼
   Обновление контейнеров
             │
             ▼
Проверка успешного выполнения
```

Такой подход позволяет публиковать изменения без ручного копирования файлов на сервер и обеспечивает единый процесс развёртывания.

---

# Скриншоты

### Grafana

![Grafana](screenshots/05-monitoring/4.дашборд%20Grafana.png)

---

### Uptime Kuma

![Grafana](screenshots/06-uptime-kuma/2.добавление%20проверок.png)

---

# Структура репозитория

```text
vps-infrastructure-platform
│
├── README.md
│   └── обзор проекта
│
├── docs/
│   ├── architecture.md
│   │   └── архитектура инфраструктуры
│   ├── deployment.md
│   │   └── процесс развёртывания
│   ├── monitoring.md
│   │   └── стек мониторинга
│   └── security.md
│       └── безопасность сервера
│
├── docker/
│   ├── docker-compose.yml
│   │   └── запуск контейнеров
│   └── README.md
│       └── описание контейнеров
│
├── nginx/
│   ├── README.md
│   │   └── описание конфигурации
│   └── sites/
│       ├── site.conf
│       ├── grafana.conf
│       └── status.conf
│
├── diagrams/
│   ├── architecture.mmd
│   ├── deployment-flow.mmd
│   ├── monitoring.mmd
│   ├── request-flow.mmd
│   └── README.md
│
└── screenshots/
    ├── 01-security/
    ├── 02-infrastructure/
    ├── 03-site-deployment/
    ├── 04-reverse-proxy/
    ├── 05-monitoring/
    ├── 06-uptime-kuma/
    ├── 07-cicd/
    └── 08-security-hardening/
```

---

# Документация

Подробное описание инфраструктуры находится в каталоге `docs`.

| Документ            | Содержание                                              |
| ------------------- | ------------------------------------------------------- |
| **architecture.md** | архитектура инфраструктуры и взаимодействие компонентов |
| **deployment.md**   | процесс развёртывания и обновления сервисов             |
| **monitoring.md**   | Prometheus, Grafana, Node Exporter и Uptime Kuma        |
| **security.md**     | SSH, Firewall, Fail2Ban и HTTPS                         |

---

# Планы по развитию

- централизованный сбор логов через Loki;
- Alertmanager для уведомлений в Telegram;
- резервное копирование данных Grafana и Uptime Kuma;
- мониторинг WireGuard через exporter;
- автоматическое обновление контейнеров;
- управление инфраструктурой через Terraform или Ansible.
