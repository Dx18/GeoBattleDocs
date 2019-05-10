# AttackScript

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

Тип `AttackScript`:

```json
{
  "attackerId": "<int>",
  "victimId": "<int>",
  "sectorId": "<int>",
  "unitGroupMoving": ["<UnitGroupMovingInfo>"],
  "timePoints": ["<TimePoint>"]
}
```

Минимальное количество `TimePoint`'ов - 4.

Первый `TimePoint`:
- начало выполнения сценария;
- все юниты и сектор имеют максимальное здоровье;

Второй `TimePoint`:
- хотя бы одна группа юнитов прибыла на сектор;
- все юниты и сектор имеют максимальное здоровье;

Предпоследний `TimePoint`:
- начало возвращения юнитов обратно;
- все юниты или сектор имеют минимальное здоровье;

Последний `TimePoint`:
- конец выполнения сценария;
- здоровье юнитов и секторов соответствует предпоследнему `TimePoint`'у;

Коэффициент локальной интерполяции между `TimePoint`'ами `prev` и `next` во время `time`:

```
factor = (time - prev.time) / (next.time - prev.time)
```

Уровень здоровья группы юнитов `unitGroup` в момент времени,
соответствующий `TimePoint`'у `timePoint` &mdash;
`health(unitGroup, timePoint)`.

Позиция группы юнитов `unitGroup` в момент времени,
соответствующий `TimePoint`'у `timePoint` &mdash;
`pos(unitGroup, timePoint)`.

Здоровье и позиция группы юнитов `unitGroup`:

```
health = health(unitGroup, prev) + factor * (health(unitGroup, next) - health(unitGroup, prev))

pos = pos(unitGroup, prev) + factor * (pos(unitGroup, next) - pos(unitGroup, prev))
```

Здоровье сектора вычисляется аналогично.