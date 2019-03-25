# Типы

Тип `AuthInfo`. Передаётся на сервер вместе с любым запросом, кроме авторизации и регистрации игрока.

```json
{
  "id": "<int>",
  "token": "<String>"
}
```

# Регистрация

**Клиент -> Сервер**:

```json
{
  "type": "Registration",
  "name": "<String>",
  "password": "<String>",
  "color": "<Color>"
}
```

**Сервер -> Клиент**:

```json
{
  "authInfo": "<AuthInfo>"
}
```

# Авторизация

**Клиент -> Сервер**:

```json
{
  "type": "Authorization",
  "name": "<String>",
  "password": "<String>"
}
```

**Сервер -> Клиент**:

```json
{
  "authInfo": "<AuthInfo>"
}
```
