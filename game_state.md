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

(**Вот здесь надо подумать (про наследование)...**)

Тип `CommandCenter`: `Beacon`.

Тип `Beacon`: `Building`.

Тип `ResearchCenter`: `Building`.

Тип `Turret`: `Building`.

Тип `Generator`: `Building`.

Тип `Mine`: `Building`.

Тип `Hangar`: `Building`: (**Лучше не читать!!!**)

```json
{
  "unitIds": ["<int>"]
}
```

Тип `Unit`: (**Этот раздел будет дорабатываться. Не читать!!!!**)

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

Тип `Spotter`: `Unit`.

Тип `Color`:

```json
{
  "r": "<int>",
  "g": "<int>",
  "b": "<int>"
}
```

Тип `GameState`:

```json
{
  "resources": "<float>",
  "playerId": "<int>",
  "playerIndex": "<int>",
  "players": [
    {
      "name": "<String>",
      "playerId": "<int>",
      "color": "<Color>",
      "commandCenter": "<CommandCenter>",
      "sectors": [
        {
          "health": "<float>",
          "maxHealth": "<float>",
          "energy": "<int>",
          "beacon": "<Beacon>",
          "buildings": ["<?: Building>"]
        }
      ],
      "units": ["<?: Unit>"]
    }
  ]
}
```