# API проекта daminov.net

## 1. Эндпоинты аутентификации

- **POST /auth/login** — Вход пользователя
  - **Запрос:**
    ```json
    {
      "email": "user@example.com",
      "password": "password123"
    }
    ```
  - **Ответ:**
    ```json
    {
      "token": "JWT_TOKEN"
    }
    ```

- **POST /auth/register** — Регистрация
  - **Запрос:**
    ```json
    {
      "email": "user@example.com",
      "password": "password123",
      "name": "John Doe"
    }
    ```
  - **Ответ:**
    ```json
    {
      "message": "Account created"
    }
    ```

## 2. Эндпоинты работы с проектами

- **GET /projects** — Получение списка проектов
- **POST /projects** — Создание проекта
