# Golos.io

Для работы микросервисов необходима синхронизированная нода `cyberway` c `nats` сервисом. Если таковой нет, то необходимо выполнить инструкции:

1. Склонировать репозиторий https://github.com/cyberway/cyberway.launch

    ```bash
    git clone https://github.com/cyberway/cyberway.launch.git
    ```

2. Запустить скрипт **start_full_node.sh** под суперпользователем - для запуска полной ноды с поддержкой nats-streaming сервера

3. Дождаться полной синхронизации ноды

## Запуск микросервисов

Необходим сервер с установленным git, docker-compose, docker

Тестирование проводилось на

```bash
Ubuntu 20.04 LTS
docker version 19.03.12
docker-compose version 1.26.2
git version 2.25.1
```

#### Склонировать репозиторий

```bash
git clone https://github.com/GolosChain/golosio-launching.git
cd golosio-launching
```

#### Создать .env файл

```bash
cp .env.example .env
```

#### Указать переменные в .env файле

```bash
CYBERWAY_HTTP_URL=https://node-cyberway
BLOCKCHAIN_BROADCASTER_URL=nats://user:password@nats-cyberway:4222
GLS_PROVIDER_PUBLIC_KEY=public-key
GLS_PROVIDER_WIF=private-key
GLS_PROVIDER_USERNAME=username
```

-   `CYBERWAY_HTTP_URL` - адрес ноды блокчейна
-   `BLOCKCHAIN_BROADCASTER_URL` - адрес NATS сервера блокчейна
-   `GLS_PROVIDER_PUBLIC_KEY` - Публичный ключ аккаунта бендвич провайдера
-   `GLS_PROVIDER_WIF` - Приватный ключ аккаунта бендвич провайдера
-   `GLS_PROVIDER_USERNAME` - Имя аккаунта бендвич провайдера

Пример .env файла

```bash
CYBERWAY_HTTP_URL=https://node-cyberway.golos.io
BLOCKCHAIN_BROADCASTER_URL=nats://user:password@nats-cyberway.golos.io:4222
GLS_PROVIDER_PUBLIC_KEY=GLS7Cb1iawbNBHQkYUchYYKe1JLJevwCst8knqG7NwJASN4w3KNNr
GLS_PROVIDER_WIF=5KBJAs6FX3ebwRCfM7Ej3ydHM9a7fT6bCMWKJjsAWro9gJn7Kk7
GLS_PROVIDER_USERNAME=glscfbkhsrx
```

#### Запуск

```bash
docker-compose up -d --build
```

После выполнения команды начнется сборка контейнеров во время которой будут отображаться некоторые warning сообщения об устаревших библиотеках. Yа них не стоит обращать внимание, так как в основном это устаревшие библиотеки для сборки микросервиса, которые в свою очередь имеют зависимость старой библиотеки

После успешной сборки должны запуститься все контейнеры и начаться синхронизация.
Сначала синхронизируется genesin - данные из "старого" блокчейна (синхронизация занимает продолжительное время). После начнется синхронизация с данными из cyberway

## Запуск клиента golos.io

#### Склонировать репозиторий

```bash
git clone https://github.com/GolosChain/golos.io.git
cd golos.io
```

#### Создать .env файл

```bash
cp .env.example .env
```

#### Указать переменные в .env файле

```bash
CYBERWAY_HTTP_URL=https://node-cyberway
GATE_CONNECT=ws://gate-node:8080
FACADE_CONNECT=http://facade-node:3001
```

-   `CYBERWAY_HTTP_URL` - адрес ноды блокчейна
-   `GATE_CONNECT` - адрес микросервиса `gate`
-   `FACADE_CONNECT` - адрес микросервиса `facade`

#### Запуск

```bash
docker-compose up --build
```
