# 🧠 M1NERVA — OSINT-агрегатор

<div align="center">

![Version](https://img.shields.io/badge/version-1.5-red?style=for-the-badge&logo=github)
![License](https://img.shields.io/badge/license-GPLv3-red?style=for-the-badge&logo=gnu)
![Python](https://img.shields.io/badge/python-3.11%2B-red?style=for-the-badge&logo=python)
![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20Android%20%7C%20Windows-red?style=for-the-badge)

**M1NERVA** — мощный CLI-инструмент для поиска информации по открытым источникам (OSINT).  
Объединяет **23+ API и утилит** в едином интерфейсе. Работает по принципу BYO-key (принеси свой ключ).

[Установка](#установка) • [Настройка](#настройка) • [Использование](#использование) • [Модули](#поддерживаемые-модули) • [Лицензия](#лицензия) • [ToS & Privacy](#-юридические-документы)

</div>

---

## ⚠️ Дисклеймер

<div align="center">

**Инструмент разработан исключительно для ОБРАЗОВАТЕЛЬНЫХ целей и этических расследований с СОГЛАСИЯ всех участников.**  
Вся ответственность за использование лежит исключительно на пользователе.

</div>

---

## ✨ Возможности

| Особенность | Описание |
|-------------|----------|
| 🚀 **23 модуля** | Телефон, Email, IP, Username, Лицо, Криптокошельки, DNS, SSL, GitHub, Утечки, Транспорт, Документы, Недвижимость, Юрлица и другие |
| ⚡ **Асинхронность** | Все запросы параллельны (`asyncio.gather`) — быстрее в разы |
| 🔄 **Автообновление** | Команда `--update` проверяет и устанавливает новые версии с GitHub |
| 🔑 **BYO-key** | Вы вставляете свои API-ключи — никаких скрытых сборов |
| 🛡️ **Безопасность** | Ключи хранятся локально, поддерживается `.env`, есть `.gitignore` |
| 📊 **Кэширование** | In-memory кэш с TTL, ограничение размера |
| 🔁 **Retry + backoff** | Автоматические повторные запросы при ошибках |
| 🧩 **Гибкость** | CLI + интерактивное меню, поддержка прокси |

---

## 📦 Установка

### 🐳 Docker (рекомендуется)

```bash
docker build -t m1nerva .
docker run -it --rm -v $(pwd)/api_keys.json:/app/api_keys.json m1nerva
```

🐍 Python (из исходников)

```bash
git clone https://github.com/nemoykimi-ui/M1NERVA-OSINT.git
cd M1NERVA-OSINT
pip install -r requirements.txt
python app.py
```

📱 Termux (Android)

```bash
pkg update && pkg install python libxml2 libxslt
pip install -r requirements.txt
python app.py
```

---

🔧 Настройка

1. API-ключи

Скопируй шаблон и заполни ключи:

```bash
cp api_keys.json.example api_keys.json   # если есть
# или просто отредактируй api_keys.json
```

Или воспользуйся интерактивной настройкой:

```bash
python app.py --setup-keys
```

2. Прокси (опционально)

Создай файл .env:

```env
PROXY=http://user:pass@host:port
```

3. GPG-подпись коммитов (для разработчиков)

Если хочешь подписывать коммиты:

```bash
gpg --full-generate-key
gpg --armor --export <KEY_ID>   # добавить в GitHub → Settings → GPG keys
git config --global user.signingkey <KEY_ID>
git config --global commit.gpgsign true
```

---

🚀 Использование

Интерактивное меню

```bash
python app.py
```

После подтверждения дисклеймера (yes, I understand) откроется меню с 23 пунктами.

CLI-режим

```bash
# Автоопределение типа
python app.py --auto --query "+79991234567"

# Конкретный тип
python app.py --type ip --query 8.8.8.8

# Очистка метаданных фото + поиск лица
python app.py --file photo.jpg --type face

# Настройка ключей
python app.py --setup-keys

# Обновление
python app.py --update
```

---

🔍 Поддерживаемые модули

# Модуль Источники Тип
1 Телефон Numverify, AbstractAPI, Veriphone, IPQualityScore, PhoneInfoga 🔑 / 🆓
2 Email EmailRep, Hunter, DeHashed, IntelX, Leak-Lookup, Epieos, RocketReach, HIBP, Holehe 🔑 / 🆓
3 Username Sherlock, Maigret, Blackbird, Social Analyzer 🆓
4 IP-адрес ipinfo, ip-api.com, Shodan, Censys, AbuseIPDB, VirusTotal, SecurityTrails 🔑 / 🆓
5 Фото лица PimEyes, FaceCheck, Betaface, SkyBiometry, Face++, Lenso 🔑
6 ФИО / адрес PDL, Pipl, FullContact, Clearbit, Spokeo, BeenVerified, Whitepages, Melissa 🔑
7 Утечки HIBP, DeHashed, IntelX, Leak-Lookup 🔑 / 🆓
8 Бонусный поиск DuckDuckGo, Wikipedia 🆓
9 Транспорт NHTSA (VIN), Autocode (номер РФ) 🆓 / 🔑
10 Документы Проверка ИНН, Контур.Фокус, ФНС 🆓 / 🔑
11 Соцсети (расш.) Sherlock, Maigret, Social-Searcher 🆓 / 🔑
12 Telegram Telethon (требует api_id/api_hash) 🔑
13 Домен WHOIS, SecurityTrails, WhoisXML 🆓 / 🔑
14 Недвижимость DaData, Росреестр (платно) 🆓 / 🔑
15 Юрлица ИНН/ОГРН (валидация), Контур.Фокус, Налог.ру 🆓 / 🔑
16 Криптокошельки Blockchain.info (BTC), Etherscan (ETH) 🆓 / 🔑
17 DNS / Поддомены DNS-записи, crt.sh, SecurityTrails 🆓 / 🔑
18 SSL-сертификаты crt.sh, real SSL check 🆓
19 GitHub Поиск пользователей и кода (токен) 🔑
20 Pastebin / Leak Psbdmp, Pastebin (dev-ключ) 🆓 / 🔑
21 Файлы по хешу VirusTotal, Hybrid-Analysis 🔑
22 Wi-Fi / BSSID WiGLE API 🔑
23 BIN карты binlist.net, BINDB 🆓 / 🔑

🆓 — бесплатный (с лимитами) / 🔑 — требуется ключ

---

📁 Структура проекта

```
M1NERVA/
├── app.py                 # Точка входа
├── api_manager.py         # HTTP-клиент (кэш, лимитер, прокси)
├── key_manager.py         # Настройка и проверка ключей
├── logger.py              # Логирование с ротацией
├── utils.py               # Автоопределение типа
├── metadata_cleaner.py    # Очистка EXIF
├── modules/               # 23 модуля поиска
├── api_keys.json          # API-ключи (не в репозитории!)
├── .env                   # Переменные окружения (не в репозитории!)
├── Dockerfile
├── requirements.txt
├── LICENSE
├── ToS.txt
├── Privacy.txt
└── README.md
```

---

🤝 Вклад в проект

Если хочешь помочь развитию M1NERVA:

1. Сообщай об ошибках — создавай Issue с подробным описанием.
2. Предлагай новые модули — если есть идеи для новых API или утилит.
3. Улучшай документацию — помогай с README, примерами, инструкциями.
4. Делай Pull Request — исправляй баги и добавляй функциональность.

---

📄 Юридические документы

· Terms of Service
· Privacy Policy

---

⚖️ Лицензия

M1NERVA распространяется под лицензией GNU GPL v3.
Подробнее см. LICENSE.

---

📬 Контакты

· Разработчик: @styx_phax
· Соавтор: DeepSeek
· Репозиторий: github.com/nemoykimi-ui/M1NERVA-OSINT

---

🙏 Благодарности

Всем разработчикам открытых API и утилит, без которых этот инструмент был бы невозможен:

· Sherlock
· Maigret
· crt.sh
· HaveIBeenPwned
· Shodan
· VirusTotal
· и всем остальным сервисам, перечисленным в документации.

---

<div align="center">

⚠️ Помни: с большой силой приходит большая ответственность. Используй инструмент мудро и этично.

https://img.shields.io/badge/-%F0%9F%A9%B8%20M1NERVA%20%F0%9F%A9%B8-red?style=for-the-badge

</div>
