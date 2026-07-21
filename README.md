# Restful-Booker API Testing Automation

[![API Tests and Report Deployment](https://github.com/ansamylv/restful-booker-api-tests/actions/workflows/main.yml/badge.svg)](https://github.com/ansamylv/restful-booker-api-tests/actions/workflows/main.yml)
[![HTML Report](https://img.shields.io/badge/HTML%20Report-View%20Live-brightgreen)](https://ansamylv.github.io/restful-booker-api-tests/)

Автоматизированный проект по тестированию публичного API [Restful-Booker](https://restful-booker.herokuapp.com/). Проект демонстрирует полный цикл QA Automation: от проектирования запросов в Postman до запуска через консоль с помощью Newman, настройки CI/CD в GitHub Actions и автоматической публикации интерактивных HTML-отчетов на GitHub Pages.

## Интерактивный отчет

Результаты последнего прогона тестов в CI/CD доступны в реальном времени:

[Открыть HTML-отчет (GitHub Pages)](https://ansamylv.github.io/restful-booker-api-tests/)

## Технологии и инструменты

- **Инструменты тестирования:** Postman, Newman (CLI Runner), `newman-reporter-htmlextra`
- **Языки и окружение:** JavaScript, Node.js
- **CI/CD и автоматизация:** GitHub Actions (Ubuntu runner)
- **Публикация отчетов:** GitHub Pages

## Структура проекта

- **`Restful-Booker API Testing.postman_collection.json`** — Коллекция запросов с разбиением на модули (`Auth`, `Booking`, `Ping`), включающая позитивные и негативные сценарии, а также скрипты валидации (Chai).
- **`baseUrl&token&bookingId.postman_environment.json`** — Файл переменных окружения для динамической передачи `baseUrl`, токенов авторизации и ID созданных бронирований.
- **`.github/workflows/main.yml`** — Пайплайн GitHub Actions для автоматического запуска тестов в облаке и деплоя отчетов.

## Как запустить проект локально

### Требования

Убедитесь, что у вас установлены **Node.js** и **npm**.

### Установка и запуск

1. Клонируйте репозиторий:

```bash
git clone https://github.com/ansamylv/restful-booker-api-tests.git
cd restful-booker-api-tests
```

2. Установите зависимости:

```bash
npm install
```

3. Запустите тесты через терминал (с генерацией локального HTML-отчета):

```bash
npm test
```

## Особенности проекта

- **Динамические цепочки:** Токен авторизации и ID созданной записи (`bookingId`) сохраняются в переменные окружения на лету и переиспользуются в `PUT`, `PATCH` и `DELETE` запросах.
- **Негативное тестирование:** Набор тестов проверяет поведение бэкенда при передаче некорректных данных, пустых тел запросов и недопустимых ID.
- **CI/CD и отчетность:** Каждый пуш в репозиторий автоматически инициирует прогон тестов на виртуальной машине, формирует детализированный дашборд и обновляет страницу на GitHub Pages.
