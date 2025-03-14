# Prometheus Stack

## Стэк для мониторинга инфраструктуры

Данный проект представляет собой готовый набор инструментов для построения комплексной системы мониторинга ИТ-инфраструктуры. Стэк включает в себя популярные открытые решения, которые позволяют собирать, хранить, анализировать метрики и алертить при обнаружении проблем.

## Компоненты стэка

### Prometheus

[Prometheus](https://prometheus.io/) - система мониторинга и база данных временных рядов. Основные особенности:
- Многомерная модель данных (временные ряды определяются именем метрики и парами ключ/значение)
- Мощный язык запросов PromQL
- Не полагается на распределенное хранилище; автономные серверы являются независимыми
- Сбор данных происходит по HTTP pull-модели

### Grafana

[Grafana](https://grafana.com/) - платформа для аналитики и мониторинга с открытым исходным кодом:
- Создание интерактивных дашбордов
- Визуализация метрик из различных источников данных
- Настраиваемые алерты
- Богатая библиотека готовых дашбордов

### InfluxDB

[InfluxDB](https://www.influxdata.com/) - высокопроизводительная база данных временных рядов:
- Оптимизирована для операций с данными временных рядов высокой доступности
- Быстрая запись и чтение
- SQL-подобный язык запросов InfluxQL

### Zabbix

[Zabbix](https://www.zabbix.com/) - продвинутая система мониторинга с открытым исходным кодом:
- Мониторинг сетей, серверов, виртуализации и сервисов
- Поддержка push и pull моделей сбора данных
- Гибкие пороговые значения и уведомления
- Автоматическое обнаружение устройств

### Alertmanager

[Alertmanager](https://prometheus.io/docs/alerting/latest/alertmanager/) - компонент, обрабатывающий алерты:
- Группировка и маршрутизация уведомлений
- Подавление дублирующих алертов
- Отправка уведомлений через различные каналы (email, мессенджеры, etc.)

## Требования

Для работы с проектом вам потребуется:

1. Docker (версия 19.03.0+)
2. Docker Compose (версия 1.27.0+)
3. Минимум 4 ГБ оперативной памяти
4. Минимум 10 ГБ свободного места на диске

## Установка и настройка

### Подготовка к запуску

1. Клонируйте репозиторий:
```bash
git clone https://github.com/gofckyourself/prometheus_stack.git
cd prometheus_stack
```

2. Создайте файл с переменными окружения:
```bash
cp env-template .env
```

3. Отредактируйте файл `.env`, установив необходимые параметры. Не используйте .env для паролей в продакшн, воспользуйтесь безопасными способами хранения, например docker secret

### Запуск

Запустите весь стэк с помощью Docker Compose:

```bash
docker-compose up -d
```

Для запуска только определенных компонентов:

```bash
docker-compose up -d prometheus grafana alertmanager
```

### Проверка работоспособности

После запуска компоненты будут доступны по следующим адресам:

- Prometheus: http://localhost:9090
- Grafana: http://localhost:3000 (по умолчанию логин/пароль: admin/admin)
- Zabbix: http://localhost:8080 (по умолчанию логин/пароль: Admin/zabbix)
- InfluxDB: http://localhost:8086

## Базовая настройка

### Prometheus

Конфигурация Prometheus находится в директории `./prometheus/`. При необходимости отредактируйте `prometheus.yml` для добавления новых scrape-таргетов.

### Grafana

1. Войдите в Grafana, используя данные по умолчанию
2. Настройте источник данных Prometheus (Configuration -> Data Sources -> Add data source)
3. Импортируйте готовые дашборды или создайте свои

### Alertmanager

Конфигурация находится в директории `./alertmanager/`. Настройте `alertmanager.yml` для интеграции с вашими системами оповещения.
