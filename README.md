# Restful Booker API — тестирование

Тестовое задание: изучение API [restful-booker](https://restful-booker.herokuapp.com/apidoc/index.html) и составление коллекции Postman с позитивными и негативными тест-кейсами.

## Что внутри

| Файл | Описание |
|---|---|
| `Restful Booker API Tests.json` | Экспортированная Postman-коллекция с запросами и тестами |
| `test-cases.xlsx` | Позитивные и негативные тест-кейсы по всем эндпоинтам |
| `bug-report.xlsx` | Баг-репорт по найденным дефектам |
| `README.md` | Описание проекта |

## Покрытые эндпоинты

- `GET /ping` — health-check
- `POST /auth` — получение токена
- `POST /booking` — создание брони
- `GET /booking` — список ID (без параметров и с фильтрами `firstname`, `lastname`, `checkin`, `checkout`)
- `GET /booking/:id` — чтение брони
- `PUT /booking/:id` — полное обновление
- `PATCH /booking/:id` — частичное обновление
- `DELETE /booking/:id` — удаление

## Структура коллекции
01. Ping
02. Auth
03. Booking - Create
04. Booking - GetIds
05. Booking - GetById
06. Booking - Update (PUT)
07. Booking - PartialUpdate (PATCH)
08. Booking - Delete


## Как запустить

1. Импортировать `Restful Booker API Tests.postman_collection.json` в Postman.
2. Убедиться, что переменные коллекции заполнены:
   - `baseUrl` = `https://restful-booker.herokuapp.com`
   - `token` = пусто (заполнится автоматически после `POST /auth`)
   - `bookingId` = пусто (заполнится после `POST /booking`)
   - `uniqueCheckin` = `2030-01-01`
   - `uniqueCheckout` = `2030-12-31`
3. Запускать запросы **по порядку** (сверху вниз). Порядок важен:
   - `Auth` → до `PUT` / `PATCH` / `DELETE`.
   - `Create` → до `GetById` / `PUT` / `PATCH` / `Delete`.

## Результаты тестирования

- **Всего тест-кейсов:** 15
- **Passed:** 13
- **Failed:** 2
- **Позитивных:** 10
- **Негативных:** 5

## Найденные баги

| ID | Заголовок | Severity |
|---|---|---|
| BUG-001 | `POST /auth` возвращает 200 OK вместо 401 Unauthorized при неверных кредах | Low |
| BUG-002 | Фильтр `GET /booking` по датам `checkin` / `checkout` не работает | High |

Подробности — в `bug-report.xlsx`.

## Технологии

- Postman 12.27.1
- JavaScript (тесты на вкладке Tests)
- REST API
