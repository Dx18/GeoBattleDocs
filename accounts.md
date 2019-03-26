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

При успехе:

```json
{
  "type": "Success",
  "authInfo": "<AuthInfo>"
}
```

При неудаче:

```json
{
  "type": "NoName"
}

{
  "type": "NoPassword"
}

{
  "type": "InvalidNameLength",
  "actual": "<int>",
  "min": "<int>",
  "max": "<int>"
}

{
  "type": "InvalidPasswordLength",
  "actual": "<int>",
  "min": "<int>"
}

{
  "type": "InvalidNameSymbols"
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

При успехе:

```json
{
  "type": "Success",
  "authInfo": "<AuthInfo>"
}
```

При неудаче:

```json
{
  "type": "PairNotFound"
}
```