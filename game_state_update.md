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