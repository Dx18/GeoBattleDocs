# Структура игрового состояния

Тип `Building`:

```json
{
  "type": "<String>",
  "x": "<int>",
  "y": "<int>",
  "id": "<int>",
  "playerId": "<int>",
  "sectorId": "<int>"
}
```

Тип `ResearchCenter`: `Building`.

Тип `Turret`: `Building`.

Тип `Generator`: `Building`.

Тип `Mine`: `Building`.

Тип `Hangar`: `Building`:

```json
{
  "unitCount": "<int>"
}
```

Тип `Unit`: (**ТОЛЬКО НА СТОРОНЕ КЛИЕНТА!!!!**)

```json
{
  "type": "<String>",
  "x": "<double>",
  "y": "<double>",
  "direction": "<double>",
  "id": "<int>",
  "health": "<float>",
  "hangarId": "<int>",
  "hangarSlot": "<int>"
}
```

Тип `Bomber`: `Unit`.

Тип `Color`:

```json
{
  "r": "<int>",
  "g": "<int>",
  "b": "<int>"
}
```

Тип `UnitGroupMovingInfo`:

```json
{
  "hangarId": "<int>",
  "arriveTime": "<double>",
  "arriveX": "<int>",
  "arriveY": "<int>",
  "returnTime": "<double>"
}
```

Тип `TimePoint`:

```json
{
  "time": "<double>",
  "sectorHealth": "<double>",
  "unitGroupsHealth": [
    {
      "hangarId": "<int>",
      "health": "<double>"
    }
  ]
}
```

Тип `GameState`:

```json
{
  "serverTime": "<double>",
  "resources": "<float>",
  "playerId": "<int>",
  "playerIndex": "<int>",
  "players": [
    {
      "name": "<String>",
      "playerId": "<int>",
      "color": "<Color>",
      "sectors": [
        {
          "x": "<int>",
          "y": "<int>",
          "sectorId": "<int>",
          "health": "<float>",
          "buildings": ["<?: Building>"]
        }
      ],
      "units": ["<?: Unit>"]
    }
  ],
  "attackEvents": [
    {
      "attackerId": "<int>",
      "victimId": "<int>",
      "sectorId": "<int>",
      "unitGroupMoving": ["<UnitGroupMovingInfo>"],
      "timePoints": ["<TimePoint>"]
    }
  ]
}
```