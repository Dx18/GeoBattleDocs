# Взаимодействие с сервером

События клиента, информация о которых отсылается на сервер (пока только постройка / снос зданий):

- Запрос состояния (`StateRequestEvent`) &mdash; игрок запрашивает информацию об игре. Сервер возвращает всё состояние игры;
- Запрос обновления (`UpdateRequestEvent`) &mdash; игрок запрашивает изменения состояния от сервера. Сервер возращает все изменения состояния игры;
- Постройка здания (`BuildEvent`) &mdash; игрок строит какое-либо здание. Сервер возвращает результат постройки (успешность или неуспешность) и уведомляет других игроков о новом здании;
- Снос здания (`DestroyEvent`) &mdash; игрок сносит какое-либо здание. Сервер возвращает сноса (успешность или неуспешность) и уведомляет других игроков о сносе.

Отношения объектов игры (очень предварительный вариант):

- Игрок **(1..*)**
  - Ресурсы **(1)**
  - Энергия **(1)**
  - Здание **(1..*)**
    - Координаты **(1)**
    - Данные здания **(1)** (для каждого вида здания данные разные)
  - Единица техники **(0..*)**
    - Координаты **(1)**
    - Данные единицы **(1)** (для каждого вида единицы техники данные разные)

## Структура игры

Тип `Building`:

```
{
  "x": "<int>",
  "y": "<int>",
  "id": "<int>"
}
```

Тип `CommandCenter`: `Building`.

Тип `Beacon`: `Building`.

Тип `ResearchCenter`: `Building`.

Тип `Turret`: `Building`.

Тип `Generator`: `Building`.

Тип `Mine`: `Building`.

Тип `Hangar`: `Building`.

Тип `Color`:

```
{
  "r": "<int>",
  "g": "<int>",
  "b": "<int>"
}
```

Тип `GameState`:

```
{
  "resources": "<int>",
  "energy": "<int>",
  "playerId": "<int>",
  "playerIndex": "<int>",
  "players": [
    {
      "name": "<String>",
      "color": "<Color>",
      "commandCenter": "<CommandCenter>",
      "beacons": ["<Beacon>"],
      "researchCenters": ["<ResearchCenter>],
      "turrets": ["<Turret>"],
      "generators": ["<Generator>"],
      "mines": ["<Mine>"],
      "hangars": ["<Hangar>"]
    }
  ]
}
```

## Вспомогательные типы для ответов сервера

Тип `BuildInfo`:

```
{
  "playerIndex": "<int>",
  "buildingType": "<String>",
  "building": "<?: Building>"
}
```

Тип `DestroyInfo`:

```
{
  "playerIndex": "<int>",
  "buildingType": "<String>",
  "id": "<int>"
}
```

## StateRequestEvent

**Клиент -> Сервер**: ничего.

**Сервер -> Клиент**:
- данные об игре (`GameState`; структура показана выше).

## UpdateRequestEvent

**Клиент -> Сервер**: ничего

**Сервер -> Клиент**:
- изменения игрового состояния, которые нужно передать игроку (см. ниже).

```
{
  "updates": ["<?: GameStateUpdate>"]
}
```

**Дополнительные действия**: очередь обновлений для игрока очищается.

## BuildEvent

**Клиент -> Сервер**:
- тип здания;
- координаты постройки.

**Сервер -> Клиент**:
- результат постройки.

```
{
  "type": "Built",
  "info": "<BuildInfo>"
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
```

**Дополнительные действия**:
- здание добавляется в игру;
- игроки уведомляются о новом здании.

## DestroyEvent

**Клиент -> Сервер**:
- идентификатор здания;

**Сервер -> Клиент**:
- результат сноса.

```
{
  "type": "Destroyed",
  "info": "<DestroyInfo>"
}

{
  "type": "BuildingIsRequired"
}
```

**Дополнительные действия**:
- здание сносится;
- игроки уведомляются о сносе здания.

## Изменения игрового состояния

Здание построено (`BuildingBuilt`: `GameStateUpdate`):

```
{
  "type": "BuildingBuilt",
  "info": "<BuildInfo>"
}
```

Здание разрушено (`BuildingDestroyed`: `GameStateUpdate`):

```
{
  "type": "BuildingDestroyed",
  "info": "<DestroyInfo>"
}
```
