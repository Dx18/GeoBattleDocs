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
  "type": "RegistrationEvent",
  "name": "<String>",
  "email": "<String>",
  "password": "<String>",
  "color": "<Color>"
}
```

**Сервер -> Клиент**:

При успехе:

```json
{
  "type": "Success",
  "name": "<String>"
}
```

При неудаче:

```json
{
  "type": "InvalidEmail"
}

{
  "type": "EmailExists"
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

{
  "type": "NameExists"
}

{
  "type": "MalformedJson"
}

{
  "type": "IncorrectData",
  "field": "<String>"
}
```

# Авторизация

**Клиент -> Сервер**:

```json
{
  "type": "AuthorizationEvent",
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

{
  "type": "MalformedJson"
}

{
  "type": "IncorrectData",
  "field": "<String>"
}
```

# Подтверждение электронной почты

**Клиент -> Сервер**:

```json
{
  "type": "EmailConfirmationEvent",
  "name": "<String>",
  "code": "<int>"
}
```

**Сервер -> Клиент**:

При успехе:

```json
{
  "type": "EmailConfirmed",
  "authInfo": "<AuthInfo>"
}
```

При неудаче:

```json
{
  "type": "WrongCode",
  "triesLeft": "<int>"
}

{
  "type": "DoesNotExist"
}

{
  "type": "MalformedJson"
}

{
  "type": "IncorrectData",
  "field": "<String>"
}
```

# Переотправка эл. письма для подтверждения эл. почты

**Клиент -> Сервер**:

```json
{
  "type": "ResendEmailEvent",
  "name": "<String>"
}
```

**Сервер -> Клиент**:

При успехе:

```json
{
  "type": "EmailResent"
}
```

При неудаче:

```json
{
  "type": "DoesNotExist"
}

{
  "type": "MalformedJson"
}

{
  "type": "IncorrectData",
  "field": "<String>"
}
```