# UML Диаграммы

По требованиям задания необходимо описать **4 функции** с помощью UML диаграмм.

---

## 1. Участие в лаунче

**Описание:** Инвестор подключает кошелёк, выбирает лаунч, отправляет TON и получает токены.

**Акторы:**

- Инвестор
- Система (TMA, Oracle, Blockchain)

**Основные шаги:**

1. Инвестор открывает TMA в Telegram
2. Подключает кошелёк через TON Connect
3. Выбирает активный лаунч
4. Указывает сумму инвестиции
5. Подтверждает транзакцию в кошельке
6. Система регистрирует участие в смарт-контракте
7. Инвестор получает токены после завершения лаунча

### Use Case

@drawio{https://github.com/dondarubin/system-engineering-playbook/blob/main/src/diagrams/uml-use-case/use-case1.drawio}

### Activity

@drawio{https://github.com/dondarubin/system-engineering-playbook/blob/main/src/diagrams/uml-activity/activity1.drawio}

### Sequence

@drawio{https://github.com/dondarubin/system-engineering-playbook/blob/main/src/diagrams/uml-sequence/sequence1.drawio}

---

## 2. Создание лаунча

**Описание:** Создатель токена загружает метаданные и запускает новый лаунч через платформу.

**Акторы:**

- Создатель токена
- Система (Manager, IPFS, Blockchain)

**Основные шаги:**

1. Создатель заполняет форму (название, символ, описание, изображение)
2. Метаданные загружаются в IPFS
3. Создатель настраивает параметры (цена, лимиты, сроки)
4. Система деплоит смарт-контракт TokenLaunch
5. Лаунч становится доступен для инвесторов

### Use Case

@drawio{https://github.com/dondarubin/system-engineering-playbook/blob/main/src/diagrams/uml-use-case/use-case2.drawio}

### Activity

@drawio{https://github.com/dondarubin/system-engineering-playbook/blob/main/src/diagrams/uml-activity/activity2.drawio}

### Sequence

@drawio{https://github.com/dondarubin/system-engineering-playbook/blob/main/src/diagrams/uml-sequence/sequence2.drawio}

---

## 3. Получение наград (Claim Rewards)

**Описание:** Пользователь просматривает доступные награды и выводит токены на свой кошелёк.

**Акторы:**

- Пользователь (Инвестор)
- Система (Dispenser, Blockchain)

**Основные шаги:**

1. Пользователь открывает раздел "Rewards" в TMA
2. Система отображает доступные reward pools
3. Пользователь выбирает награду для вывода
4. Нажимает "Claim"
5. Система формирует транзакцию через Dispenser
6. Пользователь подтверждает в кошельке
7. Токены переводятся на кошелёк пользователя

### Use Case

@drawio{https://github.com/dondarubin/system-engineering-playbook/blob/main/src/diagrams/uml-use-case/use-case3.drawio}

### Activity

@drawio{https://github.com/dondarubin/system-engineering-playbook/blob/main/src/diagrams/uml-activity/activity3.drawio}

### Sequence

@drawio{https://github.com/dondarubin/system-engineering-playbook/blob/main/src/diagrams/uml-sequence/sequence3.drawio}

---

## 4. Refund при неудачном лаунче

**Описание:** Инвестор запрашивает возврат вложенных средств до деплоя токена.

**Условия для Refund (проверяются смарт-контрактом):**

- Время после окончания creator round
- Токен ещё не задеплоен (пул на DEX не создан)

**Акторы:**

- Инвестор
- Система (TMA, Oracle, Blockchain)
- Смарт-контракты (TokenLaunch, UserVault)

**Основные шаги:**

1. Инвестор открывает TMA и видит свой баланс в лаунче
2. Нажимает кнопку "Claim Refund"
3. Смарт-контракт проверяет условия (время, статус токена)
4. Пользователь подтверждает транзакцию в кошельке
5. UserVault возвращает TON на кошелёк инвестора

**Примечание:** Oracle фиксирует статус лаунча для отображения на UI, но логика refund работает независимо на уровне смарт-контракта.

### Use Case

@drawio{https://github.com/dondarubin/system-engineering-playbook/blob/main/src/diagrams/uml-use-case/use-case4.drawio}

### Activity

@drawio{https://github.com/dondarubin/system-engineering-playbook/blob/main/src/diagrams/uml-activity/activity4.drawio}

### Sequence

@drawio{https://github.com/dondarubin/system-engineering-playbook/blob/main/src/diagrams/uml-sequence/sequence4.drawio}
