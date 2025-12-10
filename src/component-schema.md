# Компонентная схема сервисов

Схема иллюстрирует архитектуру платформы StartON Launchpad — Web3-платформы для запуска токенов на блокчейне TON.

## Компоненты

### Инфраструктура

- **Telegram Mini App** — UI на React/Next.js + TON Connect + AI-Chatbot
- **Oracle Service** — сканирует блокчейн, предоставляет данные о лаунчах
- **Manager Service** — управление пользователями, задачами, whitelist + Telegram Bot
- **Dispenser Service** — управление наградами и их распределение
- **PostgreSQL** — основная база данных
- **IPFS (своя нода)** — хранение метаданных токенов

### Смарт-контракты (в TON Network)

- **Core** → **TokenLaunch** → **UserVault** / **Jetton**
- **HighloadWallet** — массовая рассылка наград

### Внешние сервисы

- **TON Wallet** (Tonkeeper и др.) — кошельки пользователей
- **TON Network** — блокчейн TON
- **DEX** (STON.fi/DeDust) — автоматический листинг токенов
- **LLM API** — ответы AI-чатбота
- **Telegram API** — работа бота

---

## Flow взаимодействия

### Участие в лаунче (Инвестор)

```
Инвестор → TMA → Oracle (данные о лаунче)
                → Manager (регистрация, whitelist)
                → TON Connect → TON Wallet → TON Network (депозит в TokenLaunch)
```

### Создание лаунча (Создатель)

```
Создатель → TMA → Manager → IPFS (загрузка метаданных)
                → TON Connect → TON Wallet → TON Network (деплой через Core)
```

### Получение наград (Инвестор)

```
Инвестор → TMA → Dispenser (сумма для клейма)
               → TON Connect → TON Wallet → TON Network
               ← HighloadWallet (рассылка Jetton-наград)
```

### Refund при неудачном лаунче (Инвестор)

```
Инвестор → TMA → Oracle (статус лаунча)
               → TON Connect → TON Wallet → TON Network (запрос refund в TokenLaunch)
               ← UserVault (возврат TON)
```

### Администрирование

```
Админ → Telegram Bot (часть Manager) → PostgreSQL (задачи, награды)
                                     → Telegram API (уведомления)
```

### Фоновые процессы

```
Oracle ← TON Network (сканирование транзакций)
Oracle → DEX (создание пулов ликвидности)
Oracle/Manager/Dispenser ↔ PostgreSQL (хранение данных)
AI-Chatbot ↔ LLM API (ответы на вопросы)
```

---

## Диаграмма

@drawio{https://github.com/dondarubin/system-engineering-playbook/blob/main/src/diagrams/component-schema.drawio}
