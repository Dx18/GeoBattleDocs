# Изменения игрового состояния

Здание построено (`BuildingBuilt`: `GameStateUpdate`):

```json
{
  "type": "BuildingBuilt",
  "info": "<BuildTransactionInfo>"
}
```

Здание разрушено (`BuildingDestroyed`: `GameStateUpdate`):

```json
{
  "type": "BuildingDestroyed",
  "info": "<BuildTransactionInfo>"
}
```

Юнит построен (`UnitBuilt`: `GameStateUpdate`):

```json
{
  "type": "UnitBuilt",
  "info": "<UnitTransactionInfo>"
}
```

Сектор построен (`SectorBuilt`: `GameStateUpdate`):

```json
{
  "type": "SectorBuilt",
  "info": "<SectorTransactionInfo>"
}
```

Игрок добавлен (`PlayerAdded`: `GameStateUpdate`):

```json
{
  "type": "PlayerAdded",
  "name": "<String>",
  "playerId": "<int>",
  "color": "<Color>"
}
```

Игрок удалён (`PlayerRemoved`: `GameStateUpdate`):

```json
{
  "type": "PlayerRemoved",
  "playerId": "<int>"
}
```

Атака началась (`AttackStarted`: `GameStateUpdate`):

```json
{
  "type": "AttackStarted",
  "attackScript": "<AttackScript>"
}
```