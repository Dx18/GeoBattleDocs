# Взаимодействие с сервером

События клиента, информация о которых отсылается на сервер (пока только постройка / снос зданий):

- Запрос состояния (`StateRequestEvent`) &mdash; игрок запрашивает информацию об игре. Сервер возвращает всё состояние игры;
- Запрос обновления (`UpdateRequestEvent`) &mdash; игрок запрашивает изменения состояния от сервера. Сервер возращает все изменения состояния игры;
- Постройка здания (`BuildEvent`) &mdash; игрок строит какое-либо здание. Сервер возвращает результат постройки (успешность или неуспешность) и уведомляет других игроков о новом здании;
- Снос здания (`DestroyEvent`) &mdash; игрок сносит какое-либо здание. Сервер возвращает результат сноса (успешность или неуспешность) и уведомляет других игроков о сносе;
- Расширение территории (`ExpandEvent`) &mdash; игрок расширяет свою территорию. Сервер возвращает результат сноса (успешность или неуспешность) и уведомляет других игроков о новом секторе;
- Постройка юнита (`UnitBuildEvent` &mdash; игрок строит юнита на одном из своих ангаров. Сервер возвращает результат постройки (успешность или неуспешность) и уведомляет других игроков о новом юните).

## Вспомогательные типы для ответов сервера

Тип `BuildTransactionInfo`:

```json
{
  "playerIndex": "<int>",
  "building": "<?: Building>"
}
```

Тип `SectorTransactionInfo`:

```json
{
  "playerIndex": "<int>",
  "x": "<int>",
  "y": "<int>",
  "id": "<int>"
}
```

Тип `UnitTransactionInfo`:

```json
{
  "playerIndex": "<int>",
  "type": "<String>",
  "hangarId": "<int>",
  "hangarSlot": "<int>"
}
```

## StateRequestEvent

**Клиент -> Сервер**:
- авторизационная информация.

```json
{
  "type": "StateRequestEvent",
  "authInfo": "<AuthInfo>"
}
```

**Сервер -> Клиент**:
- данные об игре (`GameState`).

## UpdateRequestEvent

**Клиент -> Сервер**:
- авторизационная информация.

```json
{
  "type": "UpdateRequestEvent",
  "authInfo": "<AuthInfo>"
}
```

**Сервер -> Клиент**:
- изменения игрового состояния, которые нужно передать игроку.

```json
{
  "updates": ["<?: GameStateUpdate>"]
}
```

**Дополнительные действия**: очередь обновлений для игрока очищается.

## BuildEvent

**Клиент -> Сервер**:
- авторизационная информация;
- тип здания;
- координаты постройки.

```json
{
  "type": "BuildEvent",
  "authInfo": "<AuthInfo>",
  "buildingType": "<String>",
  "x": "<int>",
  "y": "<int>"
}
```

**Сервер -> Клиент**:
- результат постройки.

```json
{
  "type": "Built",
  "info": "<BuildTransactionInfo>",
  "cost": "<int>"
}

{
  "type": "CollisionFound"
}

{
  "type": "NotEnoughResources",
  "required": "<int>"
}

{
  "type": "BuildingLimitExceeded",
  "max": "<int>"
}

{
  "type": "NotInTerritory"
}

{
  "type": "OnSectorBound"
}
```

**Дополнительные действия**:
- здание добавляется в игру;
- игроки уведомляются о новом здании.

## DestroyEvent

**Клиент -> Сервер**:
- авторизационная информация;
- идентификатор здания.

```json
{
  "type": "DestroyEvent",
  "authInfo": "<AuthInfo>",
  "id": "<int>"
}
```

**Сервер -> Клиент**:
- результат сноса.

```json
{
  "type": "Destroyed",
  "info": "<BuildTransactionInfo>"
}

{
  "type": "BuildingIsRequired"
}
```

**Дополнительные действия**:
- здание сносится;
- игроки уведомляются о сносе здания.

## ExpandEvent

**Клиент -> Сервер**:
- авторизационная информация;
- координаты нового сектора (левый нижний угол).

```json
{
  "type": "ExpandEvent",
  "authInfo": "<AuthInfo>",
  "x": "<int>",
  "y": "<int>"
}
```

**Сервер -> Клиент**:
- результат постройки.

```json
{
  "type": "SectorTaken"
}

{
  "type": "NotEnoughResources",
  "required": "<int>"
}

{
  "type": "WrongPosition"
}
```

**Дополнительные действия**:
- сектор добавляется в игру;
- игроки уведомляются о новом секторе.

## UnitBuildEvent

**Клиент -> Сервер**:
- авторизационная информация;
- тип юнита;
- здание, на котором строится юнит.

```json
{
  "type": "UnitBuildEvent",
  "authInfo": "<AuthInfo>",
  "unitType": "<String>",
  "building": "<BuildTransactionInfo>"
}
```

**Сервер -> Клиент**:
- результат постройки.

```json
{
  "type": "Built",
  "info": "<UnitTransactionInfo>",
  "cost": "<int>"
}

{
  "type": "NotEnoughResources",
  "required": "<int>"
}

{
  "type": "NotHangar"
}

{
  "type": "NoPlaceInHangar"
}
```

**Дополнительные действия**:
- юнит добавляется в игру;
- игроки уведомляются о новом юните.