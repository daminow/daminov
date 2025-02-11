Я создаю сайт. Сайт будет на домене daminov.net.
На сайте будет 2 страницы. Персональная, и проекты. Ссылки на проект должны соответствовать: projectlink.daminov.net
Также на сайте должна быть реализована система учетной записи. Человек сможет создать ее с помощью входа в свой аккаунт например google и т.д. или с помощью электронной почты. Также у пользователя должна быть возможность восстановления учетной записи с помощью письма на почту. Также должна быть возможность смены почты а также смены пароля в личном кабинете. Должна быть реализована возможность двухфакторной аутентификации разными способами.
Должна быть реализована система админ кабинета, где должны отображаться все пользователи, возможность изменения пользователя и возможность изменения типа пользователя ( админ или обычный пользователь). Также должна быть реализована возможность создания и редактирования проектов. При создании проекта должна быть возможность импортирования разными способами. Также должна быть возможность интеграции учетной записи в проект ( у пользователя в ЛК тоже будет отображаться в какие проекты интегрирована его учетная запись ). При создании можно будет добавить название/ссылку на проект которая будет отображаться перед .daminov.net, также создать название проекта, добавить описание и лого. И при заходе через админ панель в настройки проекта показывались все пользователи которые использовали этот проект. Нужно создать такой бек который при создании проекта автоматический создавал нужные файлы для работоспособности сайта и проекта.
Тебе надо продумать весь стек и архитектуру, все файлы проекта, логику и связи, чтобы проект был максимально оптимизированным, безопасным. Весь код будет создавать ИИ, и он должен понимать исходя из твоего ответа что надо реализовать и как, я буду при реализации импортировать твой результат и ничего более. Нужно написать backend, api и postgresql. Сайт будет стоять на виртуальной машине на домене daminov.net. Должна существовать глобальная регистрация и учетная запись. Затем с каждой учетной записи можно будет использовать один из проектов и он будет отображаться у пользователя в глобально области видимости. Также у пользователя должна быть возможность создать учетную запись с помощью входа через google, apple. Также возможность восстановить пароль через почту и подключить почту или создать учетную запись на почту. Также функция смены пароля в личном кабинете. Также возможность подключить аутентификацию. Продумай логику и защиту продукта. Продукт должен быть полностью защищен. Также в глобальной админ панели нужно добавить функцию добавления проектов в общий список, изменения статуса и разной другой информации. Также должна быть возможность импорта проекта из github. Продумай все что возможно.

Персональный сайт.
Домен: daminov.net
Хостинг: виртуальная машина
БД: виртуальная машина.

# Итоговый План Реализации Проекта ToDo Листа с Учетом Безопасности, Оптимизации и Напоминаний

## 1. Обзор Проекта

### 1.1. Цель

Создание многофункционального ToDo листа с пользовательской аутентификацией, возможностью создавать задачи, события (календарь), напоминания на сайте и в Telegram, а также с административной панелью. Проект должен быть безопасным, оптимизированным и масштабируемым.

### 1.2. Целевая Аудитория

Зарегистрированные пользователи, желающие управлять своими задачами и событиями, а также администраторы для управления пользователями.

### 1.3. Основные Функциональные Требования

- **Пользователи:**
  - Регистрация и аутентификация (JWT, OAuth 2.0).
  - Управление профилем.
  - Создание, просмотр, редактирование и удаление задач.
  - Создание, просмотр, редактирование и удаление событий календаря.
  - Установка напоминаний (на сайте и в Telegram).
  - Связывание учетной записи с Telegram-ботом.
- **Напоминания:**
  - Установка напоминаний для задач и событий (дата, время).
  - Уведомления на сайте (WebSocket или SSE).
  - Уведомления в Telegram.
- **Административная панель:**
  - Просмотр списка пользователей.
  - Просмотр информации о пользователях.
  - Возможность управления пользователями.
- **Общие:**
  - Защита от DDoS, brute-force, XSS, SQL-инъекций.
  - Кэширование.
  - Мониторинг.
  - Разделение на frontend и backend.
  - Использование Docker для контейнеризации.

## 2. Технологический Стек

- **Backend:**
  - Язык: TypeScript.
  - Фреймворк: Nest.js.
  - База данных: PostgreSQL.
  - ORM: TypeORM.
  - Аутентификация: JWT, OAuth 2.0.
  - Кэширование: Redis или Memcached.
  - Уведомления: WebSocket/SSE, Telegram API.
- **Frontend:**
  - Язык: TypeScript.
  - Фреймворк: React.
  - Управление состоянием: Redux/Context API.
  - UI-библиотека: Chakra UI, Material UI или Ant Design.
  - Работа с формами: React Hook Form.
  - Работа с API: Axios или fetch API.
  - Кэширование данных: React Query или SWR.
- **Инфраструктура:**
  - Docker.
  - Nginx.
  - CI/CD (GitHub Actions, GitLab CI, Jenkins).
  - Мониторинг: Prometheus, Grafana, ELK Stack.

## 3. Подробное Описание Функционала

### 3.1. Backend (Nest.js)

#### 3.1.1. Модели Данных (PostgreSQL)

- **users:**
  - id (integer, primary key)
  - username (text, unique)
  - email (text, unique)
  - password (text)
  - created_at (timestamp)
  - updated_at (timestamp)
  - telegram_id (text, nullable)
- **tasks:**
  - id (integer, primary key)
  - user_id (integer, foreign key references users)
  - title (text)
  - description (text)
  - due_date (timestamp)
  - completed (boolean)
  - created_at (timestamp)
  - updated_at (timestamp)
- **events:**
  - id (integer, primary key)
  - user_id (integer, foreign key references users)
  - title (text)
  - description (text)
  - start_date (timestamp)
  - end_date (timestamp)
  - created_at (timestamp)
  - updated_at (timestamp)
- **invitations:**
  - id (integer, primary key)
  - inviter_id (integer, foreign key references users)
  - invitee_id (integer, foreign key references users, nullable)
  - code (text, unique)
  - created_at (timestamp)
- **reminders:**
  - id (integer, primary key)
  - user_id (integer, foreign key references users)
  - task_id (integer, foreign key references tasks, nullable)
  - event_id (integer, foreign key references events, nullable)
  - reminder_time (timestamp)
  - is_sent (boolean)

#### 3.1.2. Контроллеры и Сервисы

- **users:**
  - Контроллер: создание, получение, обновление и удаление пользователей.
  - Сервис: бизнес-логика, шифрование пароля (bcrypt), работа с БД.
- **tasks:**
  - Контроллер: CRUD для задач пользователя.
  - Сервис: бизнес-логика, работа с БД.
- **events:**
  - Контроллер: CRUD для событий пользователя.
  - Сервис: бизнес-логика, работа с БД.
- **auth:**
  - Сервис: генерация и проверка JWT.
  - Passport стратегии для JWT, OAuth 2.0.
- **admin/users:**
  - Контроллер: получение списка и информации о пользователях.
  - Сервис: бизнес-логика, доступ только для администраторов.
- **reminders:**
  - Контроллер: установка, изменение, удаление напоминаний.
  - Сервис: бизнес-логика, отправка уведомлений (WebSocket/SSE, Telegram).
  - Планировщик: проверка напоминаний.

#### 3.1.3. Аутентификация (JWT)

Реализация аутентификации пользователей с использованием JWT и Passport. Защита эндпоинтов с помощью `@UseGuards(AuthGuard('jwt'))`.

#### 3.1.4. Telegram Bot

- Интеграция с Telegram API.
- Регистрация и привязка пользователя к боту.
- Отправка уведомлений.
- Возможность просмотра списка задач и предстоящих событий через бота.

#### 3.1.5. Безопасность

- Валидация входящих данных.
- Защита от инъекций.
- Шифрование конфиденциальных данных.
- Защита JWT и других ключей.
- Rate limiting, throttling.
- CORS.

#### 3.1.6 Оптимизация

- Использование асинхронности (async/await).
- Кэширование (Redis, Memcached).
- Оптимизация запросов к БД.
- Мониторинг (Prometheus, Grafana).

### 3.2. Frontend (React/TypeScript)

#### 3.2.1. Структура Проекта

- Навигация с помощью React Router.
- Базовые компоненты навигации (header, footer).
- Стилизация с помощью styled-components/CSS Modules.

#### 3.2.2. UI Компоненты

- Формы: для задач, событий, логина, регистрации, профиля пользователя.
- Календарь: отображение событий, добавление, редактирование.
- Список задач.
- Уведомления (на сайте).
- Модальное окно.
- Компонент для подключения телеграм бота.

#### 3.2.3. Логика

- Интеграция с API backend.
- Управление состоянием (Redux/Context).
- Обработка ошибок API.
- Кэширование данных (react-query/SWR).
- Интеграция с WebSocket/SSE.

#### 3.2.4. Безопасность

- Защита от XSS.
- Content Security Policy (CSP).
- Санитация пользовательского ввода.

#### 3.2.5. Оптимизация

- Code Splitting.
- Image Optimization.
- Caching статики.
- Performance Monitoring (Lighthouse, Chrome DevTools).

#### 3.2.6. Административная панель

- Страница со списком всех пользователей.
- Страница с информацией о пользователях.
- Страница статистики.

### 3.3. Развертывание

#### 3.3.1. Docker

- Контейнеризация всех компонентов.
- Оптимизация Dockerfile.
- `docker-compose.yml`.

#### 3.3.2. Nginx

- Обратный прокси.
- SSL.
- Маршрутизация (`damivon.net/todo/_`, `daminov.net/admin/_`).

#### 3.3.3. CI/CD

- Автоматическое тестирование, сборка, развертывание.

### 3.4. Тестирование

- Unit тестирование (frontend, backend).
- Integration тестирование (API).
- End-to-end тестирование.
- Security тестирование (SAST, DAST).
- Performance тестирование.

### 3.5. Мониторинг и Поддержка

- Logging (централизованное).
- Monitoring (Prometheus, Grafana).
- Alerting (сигнализация об ошибках).
- Regular Updates.

## 4. Инструкции для ИИ

- Писать чистый, понятный и хорошо документированный код.
- Соблюдать стандарты кодирования.
- Использовать Git для контроля версий.
- Следовать архитектурным принципам, таким как разделение ответственности.
- Обеспечить модульность и возможность повторного использования компонентов.
- Использовать CamelCase для названий полей в моделях.
- Использовать API keys из переменных окружения.
- Реализовать DTO для валидации входящих данных.
- Использовать Passport стратегии для JWT и OAuth 2.0.

## 5. Prompt для ИИ (по этапам)

### 5.1. Backend (Nest.js)

**Prompt 5.1.1:** Создать модели базы данных PostgreSQL согласно описанию.
**Prompt 5.1.2:** Создать контроллеры и сервисы для управления пользователями, задачами, событиями и напоминаниями.
**Prompt 5.1.3:** Реализовать аутентификацию с JWT и OAuth 2.0.
**Prompt 5.1.4:** Реализовать API для административной панели.
**Prompt 5.1.5:** Реализовать интеграцию с Telegram API для отправки уведомлений.
**Prompt 5.1.6:** Добавить сервис для WebSocket/SSE уведомлений.
**Prompt 5.1.7:** Реализовать планировщик для проверки напоминаний.

### 5.2. Frontend (React/TypeScript)

**Prompt 5.2.1:** Создать базовую структуру React проекта.
**Prompt 5.2.2:** Создать UI-компоненты с выбранной UI-библиотекой.
**Prompt 5.2.3:** Интегрировать с backend API, а также WebSocket/SSE.
**Prompt 5.2.4:** Создать административную панель.
**Prompt 5.2.5:** Создать компонент подключения телеграм бота.

### 5.3. Развертывание

**Prompt 5.3.1:** Создать Dockerfile и `docker-compose.yml`.
**Prompt 5.3.2:** Создать конфигурационный файл Nginx.

## 6. Дополнительные Рекомендации

- **DDoS защита:** Используйте Cloudflare или аналогичные сервисы для защиты от DDoS атак.
- **Безопасность:** Проводите регулярные аудиты безопасности, используйте статический и динамический анализ кода.
- **Тестирование:** Покройте код тестами (unit, integration, end-to-end). Начните с TDD (Test-Driven Development).
- **Мониторинг:** Внедрите систему мониторинга (Prometheus + Grafana или ELK).
- **Масштабируемость:** Проектируйте приложение с учетом возможности масштабирования по горизонтали и вертикали.

# Улучшенный План Реализации Проекта с Упором на Безопасность и Оптимизацию

## Анализ и Улучшения

Предыдущий план охватывает большую часть функционала, но для достижения максимальной безопасности и оптимизации необходимо уделить внимание следующим аспектам:

1.  **Безопасность:**

    - **Комплексная защита:** Необходимо применять защиту на всех уровнях (frontend, backend, база данных, сеть).
    - **OWASP:** Ориентироваться на рекомендации OWASP (Open Web Application Security Project) для предотвращения наиболее распространенных веб-уязвимостей.
    - **Безопасность API:** Реализовать надежные методы аутентификации и авторизации, а также защиту от атак (DDoS, brute-force, injection).
    - **Безопасность данных:** Хранить конфиденциальные данные (пароли, ключи API) в зашифрованном виде.
    - **Регулярные обновления и аудиты:** Необходимо регулярно обновлять все зависимости и проводить аудиты безопасности.

2.  **Оптимизация:**

    - **Производительность:** Применять кэширование, оптимизировать запросы к БД и использовать асинхронные операции.
    - **Масштабируемость:** Обеспечить возможность масштабирования приложения по горизонтали и вертикали.
    - **Минимизация зависимостей:** Сократить количество библиотек и зависимостей для уменьшения размера приложения.
    - **Оптимизация frontend:** Ленивая загрузка, оптимизация изображений, сборка кода с помощью webpack или Vite.
    - **Мониторинг:** Внедрить инструменты мониторинга для отслеживания производительности и выявления проблем.

3.  **Использование ИИ:**

    - **Безопасная генерация кода:** Обеспечить проверку сгенерированного ИИ кода на уязвимости (статический анализ, тестирование).
    - **Кодификатор для ИИ:** Предоставлять ИИ подробные инструкции и спецификации для генерации безопасного и эффективного кода.

## Улучшенный План Реализации

1.  **Планирование и Подготовка:**

    - **Структура проекта:**
      - Мультипроектная архитектура с разделением URL (как было ранее).
      - Ясное разделение ответственности между frontend, backend и БД.
    - **Безопасность:**
      - **OWASP:** Изучение и применение рекомендаций OWASP.
      - **Threat modeling:** Определение потенциальных угроз и мер защиты.
      - **Выбор безопасных библиотек:** Использовать проверенные и безопасные библиотеки.
    - **Оптимизация:**
      - **Кэширование:** Планирование стратегии кэширования (сервер, клиент).
      - **База данных:** Выбор оптимальной структуры и индексации.
    - **ИИ:**
      - **Кодификатор:** Создание подробного кодификатора для ИИ.
      - **Инструменты:** Выбор ИИ инструментов.
    - **Инфраструктура:**
      - Docker, CI/CD, Kubernetes (если потребуется).

2.  **Backend:**

    - **Безопасность:**

      - **Валидация:** Строгая валидация данных.
      - **Аутентификация и авторизация:** JWT, OAuth 2.0 с надежной реализацией.
      - **Rate limiting, throttling:** Защита от DDoS и brute-force.
      - **CORS:** Правильная настройка CORS для безопасности.
      - **Защита от инъекций:** Параметризованные запросы, ORM.
      - **Шифрование:** Шифрование конфиденциальных данных (пароли с bcrypt, API ключи).
      - **Audit logging:** Аудит всех важных действий.
      - **Безопасное хранение:** Защита ключей JWT и других секретов.

    - **Оптимизация:**

      - **Асинхронность:** Async/await для неблокирующих операций.
      - **Кэширование:** Redis или Memcached.
      - **Запросы к БД:** Оптимизация запросов, использование индексов.
      - **Микросервисы (опционально):** Для масштабирования.
      - **Мониторинг:** Prometheus, Grafana.

    - **API:**
      - RESTful API.
      - Документация Swagger.

3.  **Frontend:**

    - **Безопасность:**

      - **XSS protection:** Избегание XSS уязвимостей (использование библиотек, таких как `dompurify`).
      - **Content Security Policy (CSP):** Настройка CSP для защиты от атак.
      - **Sanitization:** Санитация пользовательского ввода.

    - **Оптимизация:**

      - **Code Splitting:** Ленивая загрузка модулей.
      - **Image optimization:** WebP, сжатие.
      - **Caching:** Кэширование статики.
      - **Performance monitoring:** Lighthouse, Chrome DevTools.
      - **Webpack/Vite:** Для сборки.

    - **UI:**

      - UI-библиотека, генерируемая ИИ.
      - Собственные стили, дорабатывающие стили UI.

    - **Логика:**
      - Управление состоянием (Redux/Context).
      - Интеграция с API backend.

4.  **Развертывание:**

    - **Docker:**
      - Контейнеризация всех компонентов.
    - **Nginx:**
      - Обратный прокси, SSL.
      - Маршрутизация.
    - **CI/CD:**
      - Автоматическое тестирование, сборка и развертывание.
    - **Kubernetes (опционально):**
      - Для оркестрации контейнеров.

5.  **Тестирование:**

    - **Unit testing:** Frontend, Backend.
    - **Integration testing:** API, взаимодействие компонентов.
    - **End-to-end testing:** Тестирование всего приложения.
    - **Security testing:** Penetration testing, SAST (Static Application Security Testing), DAST (Dynamic Application Security Testing).
    - **Performance testing:** Тестирование под нагрузкой.

6.  **Мониторинг и Поддержка:**

    - **Logging:** Централизованное логирование.
    - **Monitoring:** Prometheus, Grafana.
    - **Alerting:** Сигнализация об ошибках и проблемах.
    - **Regular updates:** Регулярное обновление зависимостей и безопасности.

## Prompt для ИИ (разделены по этапам)

### 1. Backend (Nest.js)

**Prompt 1.1: Создание модели данных (PostgreSQL):**
Создай модель базы данных PostgreSQL для пользователей, задач (ToDo), событий (календарь) и общих ресурсов (если необходимо).

- Для таблицы users: id (integer, primary key), username (text, unique), email (text, unique), password (text), created_at (timestamp), updated_at (timestamp).
- Для таблицы tasks: id (integer, primary key), user_id (integer, foreign key references users), title (text), description (text), due_date (timestamp), completed (boolean), created_at (timestamp), updated_at (timestamp).
- Для таблицы events: id (integer, primary key), user_id (integer, foreign key references users), title (text), description (text), start_date (timestamp), end_date (timestamp), created_at (timestamp), updated_at (timestamp).
- Для таблицы invitations: id (integer, primary key), inviter_id (integer, foreign key references users), invitee_id (integer, foreign key references users, nullable), code (text, unique), created_at (timestamp).

Обеспечь связи между таблицами. Сгенерируй SQL скрипты.
Используй CamelCase для названий полей в моделях.

**Prompt 1.2: Генерация контроллеров и сервисов (Nest.js):**
Создай контроллеры и сервисы Nest.js для управления пользователями, задачами и событиями, используя модели, созданные в предыдущем шаге.

- Контроллер users для создания, получения, обновления и удаления пользователей.
- Сервис users для бизнес-логики, связанной с пользователями (шифрование пароля с bcrypt).
- Контроллер tasks для создания, получения, обновления и удаления задач для текущего пользователя.
- Сервис tasks для бизнес-логики, связанной с задачами.
- Контроллер events для управления событиями календаря текущего пользователя.
- Сервис events для бизнес-логики, связанной с событиями.
- Используй TypeORM для работы с базой данных.
- Реализуй DTO (Data Transfer Object) для валидации входящих данных.
- Используй Passport для аутентификации (JWT).
- Включи валидацию с помощью @nestjs/class-validator и @nestjs/class-transformer.
- Реализуй middleware для логгирования каждого запроса.
- Используй async/await.

**Prompt 1.3: Аутентификация (JWT):**
Реализуй аутентификацию пользователей с помощью JWT в Nest.js.

- Создай модуль auth.
- Сервис auth для генерации и проверки JWT.
- Создай Passport стратегии для JWT.
- Защити эндпоинты контроллеров (tasks, events) с помощью @UseGuards(AuthGuard('jwt')).

**Prompt 1.4: Админ панель:**
Создай API для административной панели.

- Создай контроллер /admin/users для получения списка пользователей и информации о пользователе.
- Сервис /admin/users для получения этих данных.
- Добавь Role-Based Access Control, чтобы API был доступен только администраторам.

### 2. Frontend (React/TypeScript)

**Prompt 2.1: Создание базовой структуры React проекта:**
Создай базовый React проект с TypeScript, используя create-react-app или vite.

- Настрой React Router для навигации между проектами и страницами.
- Добавь базовые компоненты навигации (header, footer).
- Используй styled-components или CSS Modules для стилизации.

**Prompt 2.2: UI-компоненты (с использованием библиотеки):**
Используй выбранную UI-библиотеку для создания следующих UI компонентов:

- Форма для создания и редактирования задач (текстовое поле для названия, текстовая область для описания, выбор даты, checkbox для статуса).
- Календарь (отображение событий, возможность добавлять, редактировать события).
- Список задач.
- Форма логина.
- Форма регистрации.
- Форма профиля пользователя (для изменения имени, почты, пароля).
- Модальное окно для подтверждения действия (например, удаления задачи).
- Компонент навигации для переключения между проектами.
- Используй react-hook-form для управления формами.

**Prompt 2.3: Интеграция с API:**
Реализуй интеграцию с backend API для:

- Получения списка задач, событий, пользователей (для админки).
- Добавления, редактирования, удаления задач и событий.
- Логина, регистрации, аутентификации.
- Сохранения данных пользователя.
- Используй fetch или axios для запросов к API.
- Используй react-query или SWR для управления данными и кэширования.
- Обработай ошибки API.

**Prompt 2.4: Административная панель (frontend):**
Создай административную панель на React:

- Страница со списком всех пользователей, для каждого пользователя должна быть ссылка для просмотра подробной информации.
- Страница с информацией о пользователе.
- Страница статистики.

### 3. Развертывание

**Prompt 3.1: Dockerfile:**
Создай Dockerfile для backend и frontend проекта.

- Оптимизируй Dockerfile для уменьшения размера образа.
- Используй многоступенчатую сборку (multistage build).
- Создай docker-compose.yml для запуска всех контейнеров.

**Prompt 3.2: Nginx:**
Создай конфигурационный файл Nginx для:

- Маршрутизации запросов к backend (Nest.js) и frontend (React) приложениям.
- Завершения SSL.
- Маршрутизации запросов daminov.net/todo/_ к ToDo проекту, и /admin/_ к админ панели.

**Общие инструкции для ИИ:**

- Пиши чистый и понятный код.
- Используй комментарии.
- Следуй стандартам кодирования.
- Соблюдай разделение ответственности.
- Используй git для контроля версий.

# Техническое Задание для ИИ: Проект ToDo Лист с Учетом Безопасности и Оптимизации

## 1. Общая Информация

### 1.1. Цель Проекта

Создание многофункционального ToDo листа с пользовательской аутентификацией, возможностью создавать задачи, события (календарь), напоминания на сайте и в Telegram, а также с административной панелью. Проект должен быть безопасным, оптимизированным и масштабируемым.

### 1.2. Целевая Аудитория

Зарегистрированные пользователи, которые хотят управлять своими задачами и событиями. Также предусмотрена административная панель для управления пользователями.

### 1.3. Требования к Функциональности

- **Пользователи:**
  - Регистрация и аутентификация (JWT, OAuth 2.0).
  - Управление профилем.
  - Создание, просмотр, редактирование и удаление задач.
  - Создание, просмотр, редактирование и удаление событий календаря.
  - Установка напоминаний (на сайте и в Telegram).
  - Связывание учетной записи с Telegram-ботом.
- **Напоминания:**
  - Установка напоминаний для задач и событий (дата, время).
  - Уведомления на сайте (WebSocket или SSE).
  - Уведомления в Telegram.
- **Административная панель:**
  - Просмотр списка пользователей.
  - Просмотр информации о пользователях.
  - Возможность управления пользователями.
- **Общие:**
  - Защита от DDoS, brute-force, XSS, SQL-инъекций.
  - Кэширование.
  - Мониторинг.
  - Разделение на frontend и backend.
  - Использование Docker для контейнеризации.

## 2. Технологический Стек

- **Backend:**
  - Язык: TypeScript.
  - Фреймворк: Nest.js.
  - База данных: PostgreSQL.
  - ORM: TypeORM.
  - Аутентификация: JWT, OAuth 2.0.
  - Кэширование: Redis или Memcached.
  - Уведомления: WebSocket/SSE, Telegram API.
- **Frontend:**
  - Язык: TypeScript.
  - Фреймворк: React.
  - Управление состоянием: Redux/Context API.
  - UI-библиотека: Chakra UI, Material UI или Ant Design.
  - Работа с формами: React Hook Form.
  - Работа с API: Axios или fetch API.
  - Кэширование данных: React Query или SWR.
- **Инфраструктура:**
  - Docker.
  - Nginx.
  - CI/CD (GitHub Actions, GitLab CI, Jenkins).
  - Мониторинг: Prometheus, Grafana, ELK Stack.

## 3. Подробное Описание Функционала

### 3.1. Backend (Nest.js)

#### 3.1.1. Модели Данных (PostgreSQL)

- **users:**
  - id (integer, primary key)
  - username (text, unique)
  - email (text, unique)
  - password (text)
  - created_at (timestamp)
  - updated_at (timestamp)
  - telegram_id (text, nullable)
- **tasks:**
  - id (integer, primary key)
  - user_id (integer, foreign key references users)
  - title (text)
  - description (text)
  - due_date (timestamp)
  - completed (boolean)
  - created_at (timestamp)
  - updated_at (timestamp)
- **events:**
  - id (integer, primary key)
  - user_id (integer, foreign key references users)
  - title (text)
  - description (text)
  - start_date (timestamp)
  - end_date (timestamp)
  - created_at (timestamp)
  - updated_at (timestamp)
- **invitations:**
  - id (integer, primary key)
  - inviter_id (integer, foreign key references users)
  - invitee_id (integer, foreign key references users, nullable)
  - code (text, unique)
  - created_at (timestamp)
- **reminders:**
  - id (integer, primary key)
  - user_id (integer, foreign key references users)
  - task_id (integer, foreign key references tasks, nullable)
  - event_id (integer, foreign key references events, nullable)
  - reminder_time (timestamp)
  - is_sent (boolean)

#### 3.1.2. Контроллеры и Сервисы

- **users:**
  - Контроллер: создание, получение, обновление и удаление пользователей.
  - Сервис: бизнес-логика, шифрование пароля (bcrypt), работа с БД.
- **tasks:**
  - Контроллер: CRUD для задач пользователя.
  - Сервис: бизнес-логика, работа с БД.
- **events:**
  - Контроллер: CRUD для событий пользователя.
  - Сервис: бизнес-логика, работа с БД.
- **auth:**
  - Сервис: генерация и проверка JWT.
  - Passport стратегии для JWT, OAuth 2.0.
- **admin/users:**
  - Контроллер: получение списка и информации о пользователях.
  - Сервис: бизнес-логика, доступ только для администраторов.
- **reminders:**
  - Контроллер: установка, изменение, удаление напоминаний.
  - Сервис: бизнес-логика, отправка уведомлений (WebSocket/SSE, Telegram).
  - Планировщик: проверка напоминаний.

#### 3.1.3. Аутентификация (JWT)

Реализация аутентификации пользователей с использованием JWT и Passport. Защита эндпоинтов с помощью @UseGuards(AuthGuard('jwt')).

#### 3.1.4. Telegram Bot

- Интеграция с Telegram API.
- Регистрация и привязка пользователя к боту.
- Отправка уведомлений.
- Возможность просмотра списка задач и предстоящих событий через бота.

#### 3.1.5. Безопасность

- Валидация входящих данных
- Защита от инъекций
- Шифрование конфиденциальных данных
- Защита JWT и других ключей
- Rate limiting, throttling
- CORS

#### 3.1.6 Оптимизация

- Использование асинхронности (async/await)
- Кэширование (Redis, Memcached)
- Оптимизация запросов к БД
- Мониторинг (Prometheus, Grafana)

### 3.2. Frontend (React/TypeScript)

#### 3.2.1. Структура Проекта

- Навигация с помощью React Router.
- Базовые компоненты навигации (header, footer).
- Стилизация с помощью styled-components/CSS Modules.

#### 3.2.2. UI Компоненты

- Формы: для задач, событий, логина, регистрации, профиля пользователя.
- Календарь: отображение событий, добавление, редактирование.
- Список задач.
- Уведомления (на сайте).
- Модальное окно.
- Компонент для подключения телеграм бота

#### 3.2.3. Логика

- Интеграция с API backend
- Управление состоянием (Redux/Context)
- Обработка ошибок API
- Кэширование данных (react-query/SWR)
- Интеграция с WebSocket/SSE

#### 3.2.4. Безопасность

- Защита от XSS
- Content Security Policy (CSP)
- Санитация пользовательского ввода

#### 3.2.5. Оптимизация

- Code Splitting
- Image Optimization
- Caching статики
- Performance Monitoring (Lighthouse, Chrome DevTools)

#### 3.2.6. Административная панель

- Страница со списком всех пользователей
- Страница с информацией о пользователях
- Страница статистики

### 3.3. Развертывание

#### 3.3.1. Docker

- Контейнеризация всех компонентов
- Оптимизация Dockerfile
- docker-compose.yml

#### 3.3.2. Nginx

- Обратный прокси
- SSL
- Маршрутизация (damivon.net/todo/_ , daminov.net/admin/_ )

#### 3.3.3. CI/CD

- Автоматическое тестирование, сборка, развертывание.

### 3.4. Тестирование

- Unit тестирование (frontend, backend)
- Integration тестирование (API)
- End-to-end тестирование
- Security тестирование (SAST, DAST)
- Performance тестирование

### 3.5. Мониторинг и Поддержка

- Logging (централизованное)
- Monitoring (Prometheus, Grafana)
- Alerting (сигнализация об ошибках)
- Regular Updates

## 4. Инструкции для ИИ

- Писать чистый, понятный и хорошо документированный код.
- Соблюдать стандарты кодирования.
- Использовать Git для контроля версий.
- Следовать архитектурным принципам, таким как разделение ответственности.
- Обеспечить модульность и возможность повторного использования компонентов.
- Использовать CamelCase для названий полей в моделях.

## 5. Prompt для ИИ (по этапам)

### 5.1. Backend (Nest.js)

**Prompt 5.1.1:** Создать модели базы данных PostgreSQL согласно описанию.
**Prompt 5.1.2:** Создать контроллеры и сервисы для управления пользователями, задачами, событиями и напоминаниями.
**Prompt 5.1.3:** Реализовать аутентификацию с JWT и OAuth 2.0.
**Prompt 5.1.4:** Реализовать API для административной панели.
**Prompt 5.1.5:** Реализовать интеграцию с Telegram API для отправки уведомлений.
**Prompt 5.1.6:** Добавить сервис для WebSocket/SSE уведомлений.
**Prompt 5.1.7:** Реализовать планировщик для проверки напоминаний.

### 5.2. Frontend (React/TypeScript)

**Prompt 5.2.1:** Создать базовую структуру React проекта.
**Prompt 5.2.2:** Создать UI-компоненты с выбранной UI-библиотекой.
**Prompt 5.2.3:** Интегрировать с backend API, а также WebSocket/SSE.
**Prompt 5.2.4:** Создать административную панель.
**Prompt 5.2.5:** Создать компонент подключения телеграм бота

### 5.3. Развертывание

**Prompt 5.3.1:** Создать Dockerfile и docker-compose.yml.
**Prompt 5.3.2:** Создать конфигурационный файл Nginx.

## 6. Дополнительные замечания

- Используйте API keys из переменных окружения
- Реализовать DTO для валидации входящих данных
- Использовать Passport стратегии для JWT и OAuth 2.0

# Техническое задание персонального сайта daminov.net

## 1. Общие сведения

- **Название проекта:** Персональный сайт daminov.net
- **Цель проекта:** Создание многофункционального сайта с возможностью управления проектами, системой учетных записей и административным управлением.
- **Домен:** daminov.net
- **Хостинг:** Виртуальная машина с высокой доступностью и масштабируемостью.

## 2. Технические требования

### 2.1. Технологический стек

- **Фронтенд:**
  - **Фреймворк:** React.js или Vue.js
  - **Стейт-менеджмент:** Redux
  - **CSS:** Tailwind CSS или Material-UI
- **Бэкенд:**
  - **Язык:** Node.js (с использованием Express.js)
  - **База данных:** PostgreSQL
- **Аутентификация:**
  - OAuth 2.0 для интеграции с Google и другими сервисами
- **Хостинг и деплой:**
  - Docker для контейнеризации
  - CI/CD: GitHub Actions или GitLab CI
- **Безопасность:**
  - SSL/TLS сертификаты
  - Защита от XSS, CSRF, SQL-инъекций
  - Регулярные обновления и патчи

### 2.2. Архитектура

- **Микросервисная архитектура:** Разделение на сервисы для пользователей, проектов, админки и т.д. для улучшения масштабируемости и обслуживания.
- **RESTful API:** Для взаимодействия между фронтендом и бэкендом.
- **Система аутентификации и авторизации:** JWT для токенов доступа, ролевая модель (Admin, User, Creator).

### 2.3. Функциональные требования

#### 2.3.1. Пользователи

- **Регистрация и авторизация:**
  - Регистрация через Google, Facebook и другие OAuth-провайдеры.
  - Регистрация через электронную почту с верификацией.
  - Восстановление учетной записи через email.
  - Смена электронной почты и пароля.
  - Двухфакторная аутентификация (TOTP, SMS, Email).
- **Личный кабинет:**
  - Просмотр и управление проектами.
  - Чаты и система друзей.
  - Настройки профиля (фото, имя пользователя, 2FA и т.д.).
  - Поддержка и отчеты.

#### 2.3.2. Административная панель

- **Управление пользователями:**
  - Просмотр списка пользователей.
  - Изменение ролей (Admin, User, Creator).
  - Блокировка и удаление пользователей.
- **Управление проектами:**
  - Создание, редактирование и удаление проектов.
  - Импорт проектов из различных источников (GitHub и др.).
  - Просмотр статистики использования проектов.
- **Отчеты и статистика:**
  - Просмотр отчетов пользователей.
  - Аналитика по новым и активным пользователям.
  - Диаграммы и графики активности.

#### 2.3.3. Панель создателя

- **Управление личными проектами:**
  - Создание и редактирование проектов.
  - Интеграция учетных записей пользователей.
  - Просмотр статистики по своим проектам.

## 3. UX/UI Оптимизация

### 3.1. Принципы дизайна

- **Простота и интуитивность:** Интерфейс должен быть понятным и легким для навигации даже для новых пользователей.
- **Консистентность:** Единый стиль оформления на всех страницах и компонентах.
- **Адаптивность:** Оптимизация под различные устройства (десктопы, планшеты, смартфоны).
- **Доступность:** Соответствие стандартам WCAG для пользователей с ограниченными возможностями.

### 3.2. Пользовательские сценарии

- **Регистрация и вход:**
  - Четкий и простой процесс регистрации с возможностью выбрать предпочитаемый метод авторизации.
  - Информативные подсказки и уведомления при ошибках.
- **Навигация по сайту:**
  - Ясное меню с доступом к основным разделам (Домашняя, Проекты, Цены, Контакты, Личный кабинет).
  - Хлебные крошки для легкой навигации внутри проектов.
- **Личный кабинет:**
  - Панель управления с быстрым доступом к основным функциям (проекты, чаты, друзья, настройки).
  - Удобное управление проектами с возможностью быстрого доступа к настройкам и статистике.
- **Админ-панель:**
  - Разделение функций по вкладкам для удобства управления пользователями, проектами и отчетами.
  - Использование таблиц с фильтрацией и сортировкой для управления списками пользователей и проектов.

### 3.3. Визуальные элементы

- **Цветовая палитра:** Выбор нейтральных и приятных для глаз цветов с акцентами для важных элементов (кнопок, уведомлений).
- **Типография:** Четкие и читаемые шрифты с достаточным размером и контрастностью.
- **Иконки и графика:** Использование понятных иконок для улучшения восприятия интерфейса.
- **Отзывчивость:** Быстрая реакция интерфейса на действия пользователя с анимациями и переходами, не мешающими работе.

## 4. Дополнительные рекомендации

### 4.1. Безопасность

- **Шифрование данных:** Использование HTTPS для всех соединений, шифрование чувствительных данных в базе данных.
- **Регулярные бэкапы:** Автоматическое резервное копирование данных для предотвращения потерь.
- **Мониторинг и логирование:** Внедрение системы мониторинга для отслеживания производительности и обнаружения потенциальных угроз.

### 4.2. Производительность

- **Оптимизация загрузки:** Минификация и объединение CSS и JavaScript файлов, использование CDN для статических ресурсов.
- **Кэширование:** Внедрение кэширования на уровне браузера и сервера для ускорения загрузки страниц.
- **Масштабируемость:** Возможность горизонтального масштабирования для обработки увеличивающегося трафика и данных.

### 4.3. Документация

- **Техническая документация:** Подробное описание архитектуры, API, используемых технологий и процессов разработки.
- **Пользовательская документация:** Инструкции и руководства для пользователей по использованию функционала сайта.

### 4.4. Интеграция с AI-инструментами

- **Использование Code Copilot, ChatGPT или Machinet:** Обеспечить совместимость с выбранными AI-инструментами для генерации и поддержки кода.
- **Автоматизированное тестирование:** Внедрение систем тестирования для проверки корректности генерируемого кода.
- **Контроль качества:** Регулярный ревью кода, написанного AI, для обеспечения соответствия стандартам и лучшим практикам.

# Техническое задание персонального сайта daminov.net

## 1. Техническая часть:

- **Домен:** daminov.net
- **Хостинг:** виртуальная машина

## 2. Архитектура

### 1. Types:

- User types:
  1. Admin
  2. User
  3. Creator
- Project types:
  - Project type:
    - Bases on github: (Сайт полностью отображает транслирует работу с github pages, но пользователь остается на домене daminov.net, и у пользователя справа сверху есть кнопки вернуться назад)
    - Bases on daminov.net (данные проекта хранятся на виртуальной машине и работают постоянно после загрузки, аналог github pages)
  - Project statuses:
    1. Released
       - Платный
       - Бесплатный
       - Закрытый
    2. On development
    3. Closed
    4. Opened

### 2. Pages

- Home
- Projects (page with list of projects)
  - Project
    - Enter to project
    - Project comments
- Pricing
- Connect
- Login / Sing in / Personal cabinet
  - **Login:**
    - Login by auth of another accounts
    - Login by email
      - If 2AUTH is on, enter code
    - Login by code on telegram
  - **Sing In:**
    - Register by auth of another accounts
      - enter your name
      - enter your password
      - If want he can enter his photo
      - When user create new account automaticaly gives id of user. basicaly userId = userName (userName.daminov.net), but after user can change userName which will be another from id, id is permanent
    - Sing in by email
      - enter your name
      - enter your password
      - If want he can enter his photo
      - When user create new account automaticaly gives id of user. basicaly userId = userName (userName.daminov.net), but after user can change userName which will be another from id, id is permanent
  - **Personal Cabinet:**
    - Projects (projects where worked)
    - Chats
      - Chat
    - Friends
      - Friend page (friendUserName.daminov.net)
        - delete friend
        - Send message
          - Chat with friends
    - Settings
      - Set/Delete/Change photo
      - Set/Delete/Change 2AUTH
      - Change password
        - Set previous password
        - Set twice new password
      - Connect telegram
      - Change userName
      - Support
        - Create new report
        - History of reports
        - Active reports
          - Chat with admin
    - Admin panel (if user isn't admin, he don't see this button)
      - Reports
      - Users
        - User
          - Full user settings
          - Delete user
          - Ban user
          - Change user type
      - Statistics
        - Statistics of new users
        - Statistics of users
      - Projects
        - Create new project
        - Project
          - Settings
            - Delete
            - Change name
            - Change projectName (projectName.daminov.net)
            - Change description of project
            - Change link to project on github
            - Change project type
            - Add user (if project is closed)
          - Statistics
            - Diagram
            - List of users of the project and their statistics
  - **Creator panel:**
    - Send to admins personal project
    - Personal project
      - Settings
        - Delete
        - Change name
        - Change projectName (projectName.daminov.net)
        - Change description of project
        - Change link to project on github
        - Change project type
        - Add user (if project is closed)
      - Statistics
        - Diagram
        - List of users of the project and their statistics
