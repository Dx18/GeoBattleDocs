# Взаимодействие с сервером

События клиента, информация о которых отсылается на сервер (пока только постройка / снос зданий):

- Запрос состояния (`StateRequestEvent`) &mdash; игрок запрашивает информацию об игре. Сервер возвращает всё состояние игры;
- Запрос обновления (`UpdateRequestEvent`) &mdash; игрок запрашивает изменения состояния от сервера. Сервер возращает все изменения состояния игры;
- Постройка здания (`BuildEvent`) &mdash; игрок строит какое-либо здание. Сервер возвращает результат постройки (успешность или неуспешность) и уведомляет других игроков о новом здании;
- Снос здания (`DestroyEvent`) &mdash; игрок сносит какое-либо здание. Сервер возвращает результат сноса (успешность или неуспешность) и уведомляет других игроков о сносе;
- Расширение территории (`SectorBuildEvent`) &mdash; игрок расширяет свою территорию. Сервер возвращает результат сноса (успешность или неуспешность) и уведомляет других игроков о новом секторе;
- Постройка юнита (`UnitBuildEvent`) &mdash; игрок строит юнита на одном из своих ангаров. Сервер возвращает результат постройки (успешность или неуспешность) и уведомляет других игроков о новом юните).
- Нападение (`AttackEvent`) &mdash; игрок собирается напасть на врага. Сервер возвращает результат нападения (успешность или неуспешность) и объект `AttackScript` и уведомляет других игроков о нападении.
- Исследование (`ResearchEvent`) &mdash; игрок запрашивает исследование. Сервер возвращает результат исследования (успешность или неуспешность).

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
  "unit": "<?: Unit>"
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

```json
{
  "type": "StateRequestSuccess",
  "gameState": "<GameState>"
}

{
  "type": "WrongAuthInfo"
}
```

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
  "type": "UpdateRequestSuccess",
  "time": "<float>",
  "updates": ["<?: GameStateUpdate>"]
}

{
  "type": "WrongAuthInfo"
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
  "type": "BuildingBuilt",
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
  "type": "SectorBlocked"
}

{
  "type": "WrongAuthInfo"
}

{
  "type": "MalformedJson"
}

{
  "type": "IncorrectData",
  "field": "<String>"
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
  "type": "BuildingDestroyed",
  "info": "<BuildTransactionInfo>"
}

{
  "type": "NotOwningBuilding"
}

{
  "type": "SectorBlocked"
}

{
  "type": "WrongAuthInfo"
}

{
  "type": "MalformedJson"
}

{
  "type": "IncorrectData",
  "field": "<String>"
}
```

**Дополнительные действия**:
- здание сносится;
- игроки уведомляются о сносе здания.

## SectorBuildEvent

**Клиент -> Сервер**:
- авторизационная информация;
- координаты нового сектора (левый нижний угол).

```json
{
  "type": "SectorBuildEvent",
  "authInfo": "<AuthInfo>",
  "x": "<int>",
  "y": "<int>"
}
```

**Сервер -> Клиент**:
- результат постройки.

```json
{
  "type": "SectorBuilt",
  "info": "<SectorTransactionInfo>"
}

{
  "type": "NotEnoughResources",
  "required": "<int>"
}

{
  "type": "IntersectsWithEnemy",
  "enemyIndex": "<int>"
}

{
  "type": "WrongPosition"
}

{
  "type": "WrongAuthInfo"
}

{
  "type": "MalformedJson"
}

{
  "type": "IncorrectData",
  "field": "<String>"
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
  "hangarId": "<int>"
}
```

**Сервер -> Клиент**:
- результат постройки.

```json
{
  "type": "UnitBuilt",
  "info": "<UnitTransactionInfo>",
  "cost": "<int>"
}

{
  "type": "NotEnoughResources",
  "required": "<int>"
}

{
  "type": "NoPlaceInHangar"
}

{
  "type": "SectorBlocked"
}

{
  "type": "WrongAuthInfo"
}

{
  "type": "MalformedJson"
}

{
  "type": "IncorrectData",
  "field": "<String>"
}
```

**Дополнительные действия**:
- юнит добавляется в игру;
- игроки уведомляются о новом юните.

## AttackEvent

**Клиент -> Сервер**:
- авторизационная информация;
- ID нападающего игрока;
- ID игрока, на которого нападают;
- ID сектора, на который нападают;
- ангары, используемые для нападения на игрока;
- сектор, на который производится нападение.

```json
{
  "type": "AttackEvent",
  "authInfo": "AuthInfo",
  "attackerId": "<int>",
  "victimId": "<int>",
  "hangarIds": ["<int>"],
  "sectorId": "<int>"
}
```

**Сервер -> Клиент**:
- результат нападения.

```json
{
  "type": "AttackStarted",
  "attackScript": "<AttackScript>"
}

{
  "type": "NotAttackable"
}

{
  "type": "HangarsAlreadyUsed"
}

{
  "type": "WrongAuthInfo"
}

{
  "type": "MalformedJson"
}

{
  "type": "IncorrectData",
  "field": "<String>"
}
```

## ResearchEvent

**Клиент -> Сервер**:
- авторизационная информация;
- тип исследования (`"TurretDamage"` | `"UnitDamage"` | `"GeneratorEfficiency"`).

```json
{
  "type": "ResearchEvent",
  "authInfo": "<AuthInfo>",
  "researchType": "<String>"
}
```

**Сервер -> Клиент**:
- результат исследования.

```json
{
  "type": "Researched",
  "researchType": "<String>",
  "cost": "<int>"
}

{
  "type": "NoResearchCenter"
}

{
  "type": "NotEnoughResources",
  "required": "<int>"
}

{
  "type": "MaxLevel"
}

{
  "type": "WrongAuthInfo"
}

{
  "type": "MalformedJson"
}

{
  "type": "IncorrectData",
  "field": "<String>"
}
```
