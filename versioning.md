# Версионирование клиентской части

Используется семантическое версионирование ([https://semver.org](https://semver.org)). В качестве сборочных метаданных используется название сборки (обычно `official`, но также возможны неофициальные).

Примеры:

- `1.0.0+official` - официальная сборка версии 1.0.0.
- `1.10.16+official` - официальная сборка версии 1.10.16.
- `2.0.8+expensive_units` - неофициальная сборка версии 2.0.8 с названием `expensive_units`.

Версия устанавливается в файле `android/build.gradle`:

```gradle
...
defaultConfig {
    ...
    versionCode 1
    versionName "1.0.0+official"
}
...
```