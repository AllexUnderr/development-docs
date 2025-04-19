# 0. Перед компиляцией
## 1. Gradle Configuration & Dependency Resolution
`Gradle` читает `build.gradle` и обрабатывает зависимости. При использовании плагинов(`com.android.application`) применяет их

## 2. Preprocessing Tasks (Pre-Build)
### Генерация источников:
`Gradle` таски генерируют необходимые файлы необходимые для основного кода(`BuildConfig.java`, `R.java`), включая значения из `gradle.properties` и `AndroidManifest.xml`

### Выполнение AAPT2 (Android Asset Packaging Tool)
- Компиляция `XML` ресурсов(`res/layout`, `res/values`) в бинарники
- Генерация `R.java` класса - связывает значения из `Java`/`Kotlin` с `XML` ресурсами

### Выполнение Code Generation Plugins
Выполнение `Gradle` плагинов(`protobuf`, `Dagger Hilt CodeGen`)

## Annotation Processing
* [[KSP]] исполняется первым
* [[KAPT]] исполняется вторым

# 1. Compilation (Исходный код → DEX)
- `Java`/`Kotlin` код компилируется в **Java bytecode** (`.class` файлы)
- `D8`/`R8` компилятор конвертирует `.class` & `.jar` файлы в `DEX`(`Dalvik Executable`) файлы(`classes.dex`), которые `Android Runtime` (`ART`) может запустить

# 2. Resource Processing
- `XML` файлы(`layouts`, `strings`, `drawables`) компилируются в бинарник через`aapt2` (Android Asset Packaging Tool).
- `AndroidManifest.xml` файл(***Ы???***) также обрабатываются и конвертируются в бинарный формат

# 3. Packaging (DEX + Resources → APK)
Упаковка в `APK`:
-  `DEX` файлы
- Скомпилированных ресурсов
- Обработанного(***ЫХ???***) `AndroidManifest.xml`
- Нативных(написанных на `C`/`C++`) библиотек (`.so` файлы) если есть
- Ассетов и других необходимых файлов

# 4. Signing
`APK` подписывается цифровой подписью. Подпись обеспечивает безопасность и целостность