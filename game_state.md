# Структура игрового состояния

Тип `Sector`:

```json
{
  "x": "<int>",
  "y": "<int>",
  "sectorId": "<int>",
  "isBlocked": "<boolean>",
  "buildings": ["<?: Building>"]
}
```

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
  "units": "<UnitGroup>"
}
```

Тип `UnitGroup`:

```json
{
  "units": ["<Unit>"],
  "health": "<float>"
}
```

Тип `Unit` (на стороне клиента):

```json
{
  "type": "<String>",
  "x": "<double>",
  "y": "<double>",
  "direction": "<double>",
  "id": "<int>",
  "hangarId": "<int>",
  "hangarSlot": "<int>"
}
```

Тип `Unit` (на стороне сервера):

```json
{
  "type": "<String>",
  "id": "<int>",
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
  "sectorHealth": "<float>",
  "unitGroupsHealth": [
    {
      "hangarId": "<int>",
      "health": "<float>"
    }
  ]
}
```

Тип `ResearchInfo`:

```json
{
  "turretDamageLevel": "<int>",
  "unitDamageLevel": "<int>",
  "generatorEfficiencyLevel": "<int>"
}
```

Тип `GameState`:

```json
{
  "resources": "<float>",
  "playerId": "<int>",
  "time": "<double>",
  "researchInfo": "<ResearchInfo>",
  "players": [
    {
      "name": "<String>",
      "playerId": "<int>",
      "color": "<Color>",
      "sectors": ["<Sector>"]
    }
  ],
  "attackScripts": [
    {
      "id": "<int>",
      "attackerId": "<int>",
      "victimId": "<int>",
      "sectorId": "<int>",
      "unitGroupMoving": ["<UnitGroupMovingInfo>"],
      "timePoints": ["<TimePoint>"]
    }
  ]
}
```