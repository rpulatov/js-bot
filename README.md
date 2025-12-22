# bot-stars

**Описание**
- **Назначение:** Telegram-бот для управления «звёздами» (баллами) подростков, с регистрацией пользователей, просмотром рейтинга, вопросами пользователям и админскими действиями.
- **Функции:**
	- `/start` — онбординг (имя, фамилия, дата рождения, пол, телефон).
	- `/help` — справка.
	- `/viewstars` — просмотр звёзд пользователя.
	- Админ-действия: блокировка/разблокировка (`/block`, `/unblock`), просмотр списка (`/list`), добавление/удаление звёзд через кнопки, ответы на вопросы пользователей.
- **Хранение данных:** Google Sheets (через `gspread` и `oauth2client`), путь к JSON-credentials задаётся через переменную окружения.

**Требования**
- Python 3.13+
- Доступ к Google Sheets и JSON-файл сервисного аккаунта (`credentials.json`).

**Переменные окружения (.env)**
- `TELEGRAM_BOT_TOKEN`: токен бота.
- `SPREADSHEET_NAME`: имя таблицы Google Sheets.
- `CREDENTIALS_FILE`: путь к JSON-файлу сервисного аккаунта.

Пример файла `.env`:

```env
TELEGRAM_BOT_TOKEN=123456:ABCDEF...
SPREADSHEET_NAME=Jesus Stars
CREDENTIALS_FILE=credentials.json
```

## Установка зависимостей

Вариант A — через PDM (рекомендуется):

```bash
python3 -m pip install -U pdm
pdm install
```

Вариант B — через venv + pip:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install .
```

## Запуск

Перед запуском убедитесь, что `.env` и `credentials.json` доступны и корректны.

Вариант A — PDM:

```bash
pdm run start
```

Вариант B — напрямую Python:

```bash
python -m bot_stars.main
```

## Docker

Сборка образа:

```bash
docker build -t bot-stars .
```

Запуск контейнера с переменными окружения и монтированием `credentials.json`:

```bash
docker run \
	--name bot-stars \
	--env-file .env \
	-v "$(pwd)/credentials.json:/app/credentials.json:ro" \
	-e CREDENTIALS_FILE=/app/credentials.json \
	bot-stars
```

Примечание: В Dockerfile используется установка зависимостей через PDM и запуск `python -m bot_stars.main`.
