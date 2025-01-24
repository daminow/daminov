# Архитектура проекта daminov.net

## 1. Введение

Проект daminov.net – это веб-приложение, включающее персональную страницу и страницу проектов. В проекте реализована система управления учетными записями с возможностью регистрации через Google, Apple или email. Также предусмотрены функции восстановления пароля, смены email и пароля, а также двухфакторной аутентификации.

---

## 2. Технологический стек

### **Frontend:**

- **React.js + Vite** – для быстрого рендеринга и SSR.
- **TypeScript** – для обеспечения безопасности и типизации кода.
- **Redux Toolkit** – управление глобальным состоянием.
- **React Router** – маршрутизация страниц.
- **TailwindCSS** – удобная стилизация интерфейса.
- **Axios** – взаимодействие с API.
- **Next.js** – для реализации SSR страниц проектов.

### **Backend:**

- **FastAPI** – асинхронный веб-фреймворк на Python для быстрого API.
- **PostgreSQL** – реляционная база данных.
- **Redis** – кеширование данных и управление сессиями.
- **Celery** – асинхронная обработка задач.
- **JWT + OAuth2** – безопасная аутентификация и авторизация.
- **Docker** – контейнеризация приложения.
- **Traefik** – реверс-прокси.

### **DevOps/Безопасность:**

- **NGINX** – веб-сервер для обработки запросов.
- **Certbot** – автоматическое обновление SSL-сертификатов.
- **Sentry** – мониторинг ошибок.
- **Prometheus + Grafana** – сбор и анализ метрик.
- **Fail2Ban** – защита от брутфорс-атак.
- **Argon2** – безопасное хеширование паролей.

---

## 3. Структура проекта

```
.
|-- backend/
|-- frontend/
|-- db/
|-- projects/
|-- docs/
|-- docker-compose.yml
|-- .env
|-- README.md
```

---

## 4. Логика работы

### **Аутентификация**

1. Регистрация через Google, Apple, email.
2. OAuth2 для соцсетей и JWT для email.
3. Двухфакторная аутентификация (TOTP, Email, SMS).
4. Восстановление пароля через email.
5. Смена почты и пароля в личном кабинете.

### **Проекты**

1. Создание проектов с параметрами: название, ссылка, описание, логотип.
2. Автоматическое создание поддомена `projectlink.daminov.net`.
3. Интеграция учетной записи пользователя в проект.
4. Импорт проектов с GitHub.
5. Управление проектами через админ-панель.

### **Админ-панель**

1. Управление пользователями (редактирование, удаление, смена ролей).
2. Управление проектами (создание, редактирование, удаление).
3. Логирование действий пользователей.

---

## 5. Безопасность

- Хеширование паролей с помощью Argon2.
- Ограничение частоты запросов API.
- Настройка CORS для предотвращения межсайтовых атак.
- Защита от CSRF, XSS и SQL-инъекций.
- Регулярное резервное копирование базы данных.
- Логирование и мониторинг действий пользователей.

---

## 6. Развертывание и CI/CD

1. Автоматическое развертывание через GitHub Actions.
2. Использование Docker для контейнеризации.
3. Реверс-прокси через NGINX + Traefik.
4. Мониторинг с помощью Prometheus и Grafana.

---

## 7. Подробное описание API

### **Аутентификация**

```
POST /api/v1/auth/register
POST /api/v1/auth/login
POST /api/v1/auth/forgot-password
POST /api/v1/auth/reset-password
POST /api/v1/auth/2fa-enable
POST /api/v1/auth/2fa-verify
POST /api/v1/auth/logout
```

### **Проекты**

```
POST /api/v1/projects/create
GET /api/v1/projects/list
GET /api/v1/projects/{project_id}
PUT /api/v1/projects/{project_id}/update
DELETE /api/v1/projects/{project_id}/delete
```

### **Админ**

```
GET /api/v1/admin/users
PUT /api/v1/admin/users/{user_id}
DELETE /api/v1/admin/users/{user_id}
GET /api/v1/admin/projects
PUT /api/v1/admin/projects/{project_id}
```

---

## 8. Структура базы данных PostgreSQL

### **Таблица users (пользователи)**

- `id` (UUID, primary key)
- `email` (VARCHAR, unique, not null)
- `hashed_password` (TEXT, not null)
- `is_active` (BOOLEAN, default=True)
- `role` (VARCHAR, default='user')
- `created_at` (TIMESTAMP)

### **Таблица projects (проекты)**

- `id` (UUID, primary key)
- `user_id` (UUID, foreign key to users.id)
- `name` (VARCHAR, not null)
- `description` (TEXT)
- `domain` (VARCHAR, unique, not null)
- `created_at` (TIMESTAMP)

### **Таблица audit_logs (логи действий)**

- `id` (UUID, primary key)
- `user_id` (UUID, foreign key to users.id)
- `action` (VARCHAR, not null)
- `timestamp` (TIMESTAMP)

---

Такая структура позволяет эффективно управлять пользователями, проектами и логами.
