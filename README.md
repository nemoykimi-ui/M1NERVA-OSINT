# M1NERVA — OSINT-агрегатор

CLI-инструмент для сбора информации из открытых источников. Объединяет несколько модулей поиска в едином интерфейсе. Работает по принципу BYO-key — используются ваши собственные API-ключи.

## ⚠️ Дисклеймер

> Инструмент разработан исключительно для образовательных целей и этических расследований с согласия всех участников.
> Вся ответственность за использование лежит на пользователе.

## Возможности

- Асинхронные запросы (`asyncio.gather`) — параллельная обработка
- Автообновление через `--update`
- BYO-key — свои API-ключи, никаких скрытых сборов
- Ключи хранятся локально, поддерживается `.env` и `.gitignore`
- In-memory кэш с TTL
- Retry с backoff при ошибках сети
- CLI + интерактивное меню, поддержка прокси

## Установка

### Docker (рекомендуется)

\`\`\`bash
docker build -t m1nerva .
docker run -it --rm -v $(pwd)/api_keys.json:/app/api_keys.json m1nerva
\`\`\`

### Python (из исходников)

\`\`\`bash
git clone https://github.com/nemoykimi-ui/M1NERVA-OSINT.git
cd M1NERVA-OSINT
pip install -r requirements.txt
python app.py
\`\`\`

### Termux (Android)

\`\`\`bash
pkg update && pkg install python libxml2 libxslt
pip install -r requirements.txt
python app.py
\`\`\`

## Настройка

### API-ключи

\`\`\`bash
python app.py --setup-keys
\`\`\`

Либо отредактируйте `api_keys.json` вручную.

### Прокси (опционально)

Создайте файл `.env`:

\`\`\`env
PROXY=http://user:pass@host:port
\`\`\`

### GPG-подпись коммитов (для разработчиков)

\`\`\`bash
gpg --full-generate-key
gpg --armor --export <KEY_ID>
git config --global user.signingkey <KEY_ID>
git config --global commit.gpgsign true
\`\`\`

## Использование

### Интерактивное меню

\`\`\`bash
python app.py
\`\`\`

После подтверждения дисклеймера откроется меню.

### CLI-режим

\`\`\`bash
python app.py --auto --query "<запрос>"
python app.py --type ip --query 8.8.8.8
python app.py --setup-keys
python app.py --update
\`\`\`

## Структура проекта

\`\`\`
M1NERVA/
├── app.py                 # Точка входа
├── api_manager.py         # HTTP-клиент (кэш, лимитер, прокси)
├── key_manager.py         # Настройка и проверка ключей
├── logger.py              # Логирование с ротацией
├── utils.py                # Автоопределение типа
├── metadata_cleaner.py     # Очистка EXIF
├── modules/                 # Модули поиска
├── api_keys.json            # API-ключи (не в репозитории!)
├── .env                      # Переменные окружения (не в репозитории!)
├── Dockerfile
├── requirements.txt
├── LICENSE
├── ToS.txt
├── Privacy.txt
└── README.md
\`\`\`

## Юридические документы

- [Terms of Service](ToS.txt)
- [Privacy Policy](Privacy.txt)

## Лицензия

Распространяется под лицензией GNU GPL v3. Подробнее см. [LICENSE](LICENSE).

## Контакты

- Разработчик: @styx_phax
- Соавтор: DeepSeek
- Репозиторий: github.com/nemoykimi-ui/M1NERVA-OSINT

## Благодарности

Разработчикам открытых инструментов, использованных в проекте: Sherlock, Maigret, crt.sh, HaveIBeenPwned, Shodan, VirusTotal и другим сервисам, перечисленным в документации.
