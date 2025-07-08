# Микросервис Сокращения Ссылок

**Простой микросервис для сокращения ссылок и контроля посещений**

## Стек
- **FastAPI**
- **SQLAlchemy**
- **SQLite + aiosqlite драйвер**

## Установка

### 1. Клонируйте репозиторий

```bash
git clone https://github.com/XCraiteX/tiny-link-service.git
```

### 2. Замените ссылки в `settings.py`

```bash
# Ссылка для редиректа, если ссылка не найдена
DEFAULT_LINK = 'https://google.com'
# Ваша ссылка развёртывания на локал хосте для использования
SERVICE_LINK = 'http://localhost:8000/lnk/'
```

### 3. Запуск сервера

```bash
cd app
uvicorn api:app --port 3400  
```

### 4. Конфигурация Nginx

```nginx
location /lnk/ {
    proxy_pass http://localhost:3400;
    proxy_http_version 1.1;
}
```

### 5. Использование API в своих проектах
<br>

# Использование API

### 1. Создание ссылки | `POST` - `service_link` `/api`

- **Параметры**

```json
{
    "link": "your_link_here" ,
    "limit": 5
}
```
  
> **Лимит не обязательный аргумент, но при наличии, ограничивает максимальное кол-во переходов по ссылке  
> (После исчерпания лимита, ссылка удаляется)**

###  > Ответ

- Successfull

```json
{
    "status": "OK",
    "shorted": "received_link",
    "views": 6
}
```

- Error

```json
{
    "status": "Error",
    "details": "Invalid link"
}
```
