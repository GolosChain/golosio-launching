# Golos.io

## Запуск микросервисов

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

`CYBERWAY_HTTP_URL` - адрес ноды блокчейна
`BLOCKCHAIN_BROADCASTER_URL` - адрес NATS сервера блокчейна
`GLS_PROVIDER_PUBLIC_KEY` - Публичный ключ аккаунта бендвич провайдера
`GLS_PROVIDER_WIF` - Приватный ключ аккаунта бендвич провайдера
`GLS_PROVIDER_USERNAME` - Имя аккаунта бендвич провайдера

#### Запуск

```bash
docker-compose up -d --build
```

После успешной сборки контейнеров автоматически начнется синхронизация которая занимает продолжительное время

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

`CYBERWAY_HTTP_URL` - адрес ноды блокчейна
`GATE_CONNECT` - адрес микросервиса `gate`
`FACADE_CONNECT` - адрес микросервиса `facade`

#### Запуск

```bash
docker-compose up --build
```