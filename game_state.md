# Структура игрового состояния

Тип `Building`:

```json
{
  "type": "<String>",
  "x": "<int>",
  "y": "<int>",
  "id": "<int>",
  "health": "<float>"
}
```

Тип `CommandCenter`: `Building`.

Тип `Beacon`: `Building`.

Тип `ResearchCenter`: `Building`.

Тип `Turret`: `Building`.

Тип `Generator`: `Building`.

Тип `Mine`: `Building`.

Тип `Hangar`: `Building`:

```json
{
  "unitIds": ["<int>"]
}
```

Тип `Unit`:

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
  "energy": "<float>",
  "playerId": "<int>",
  "playerIndex": "<int>",
  "players": [
    {
      "name": "<String>",
      "color": "<Color>",
      "commandCenter": "<CommandCenter>",
      "beacons": ["<Beacon>"],
      "researchCenters": ["<ResearchCenter>"],
      "turrets": ["<Turret>"],
      "generators": ["<Generator>"],
      "mines": ["<Mine>"],
      "hangars": ["<Hangar>"],
      "bombers": ["<Bomber>"],
      "spotters": ["<Spotter>"]
    }
  ]
}
```