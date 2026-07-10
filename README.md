M1NERVA — OSINT-агрегатор
================================

Версия: 1.5
Лицензия: GNU GPL v3
Разработчики: @styx_phax, DeepSeek

Дисклеймер
----------
Инструмент разработан исключительно для образовательных целей и этических расследований с согласия всех участников. Вся ответственность за использование лежит на пользователе.

Возможности
-----------
+ 23+ модуля: телефон, email, IP, username, лицо, криптокошельки, DNS, SSL, GitHub, утечки, транспорт, документы, недвижимость, юрлица и другие.
+ Асинхронные запросы (asyncio.gather) — быстрее.
+ Автообновление через --update.
+ BYO-key (свои API-ключи).
+ Кэширование, ретраи, прокси, логирование.

Установка
---------
Docker (рекомендуется):
  docker build -t m1nerva .
  docker run -it --rm -v $(pwd)/api_keys.json:/app/api_keys.json m1nerva

Из исходников (Python):
  git clone https://github.com/nemoykimi-ui/M1NERVA-OSINT.git
  cd M1NERVA-OSINT
  pip install -r requirements.txt
  python app.py

Termux (Android):
  pkg update && pkg install python libxml2 libxslt
  pip install -r requirements.txt
  python app.py

Настройка ключей
----------------
+ Заполните api_keys.json (создайте из примера).
+ Или запустите: python app.py --setup-keys
+ Прокси в .env: PROXY=http://user:pass@host:port

Использование
-------------
Интерактивное меню:
  python app.py

CLI-режим:
  python app.py --auto --query "+79991234567"
  python app.py --type ip --query 8.8.8.8
  python app.py --file photo.jpg --type face
  python app.py --setup-keys
  python app.py --update

Поддерживаемые модули (кратко)
-----------------------------
Телефон, Email, Username, IP-адрес, Фото лица, ФИО/адрес, Утечки, Бонусный поиск, Транспорт, Документы, Соцсети (расшир.), Telegram, Домен, Недвижимость, Юрлица, Криптокошельки, DNS/Поддомены, SSL-сертификаты, GitHub, Pastebin/Leak, Файлы по хешу, Wi-Fi/BSSID, BIN карты.

Все модули используют ваши ключи (BYO-key). Некоторые бесплатны, другие требуют ключей.

Структура проекта
-----------------
M1NERVA/
├── app.py
├── api_manager.py
├── key_manager.py
├── logger.py
├── utils.py
├── metadata_cleaner.py
├── modules/
├── api_keys.json
├── .env
├── Dockerfile
├── requirements.txt
├── LICENSE
├── ToS.txt
├── Privacy.txt
└── README.md

Юридические документы
---------------------
+ Terms of Service: ToS.txt
+ Privacy Policy: Privacy.txt

Контакты
--------
+ Разработчик: @styx_phax
+ Соавтор: DeepSeek
+ Репозиторий: https://github.com/nemoykimi-ui/M1NERVA-OSINT

------------------------------------------------------------
Помните: инструмент только для законного использования с согласия всех сторон.
