# AAB
`AAB` - формат файла, для установки `Android` приложения, который позволяет экономить место, занимаемое приложением.

Система `Android` поддерживает 4 архитектуры, 6 разрешений графики и более 150 языков. Чтобы не собирать отдельный `apk` для каждого варианта или не запихивать в `apk` все ресурсы можно использовать `AAB`.
`AAB` содержит скомпилированный код и все необходимые ресурсы, однако для построения `APK` выбираются только те ресурсы и архитектура которая необходима устройству и пользователю, чтобы экономить память.

## Файловая структура
Файл формата `.aab` для установки андроид приложения содержит:
* `base` - код и ресурсы которые шарятся для всех устройств
* `splits` - дополнительные ресурсы для разных архитектур, языков и разрешений экрана
* `Metadata` - информация об конфигурации и структуре приложения

Файлы с расширением `.pb` - `Module Protocol Buffer`. Файлы содержат метаданные которые описывают контент каждого модуля приложения для магазинов приложений(`Google Play`). 
Например `BundleConfig.pb` содержит данные о самом бандле. `native.pb` и `resources.pb` описывают код и ресурсы в каждом модуле, что позволяет оптимизировать конфигурацию АПК для конкретного девайса.

## Частичное обновление
Частичное обновление - обновление при котором не скачивается `APK` полностью, а скачивается только `diff` между старым и новым `APK`.
Для `AAB` существует два варианта частичного обновления:
* Play Feature Delivery
* Instant App Updates

### Play Feature Delivery
Обновляются только те модули, которые изменились.
В андроид студии есть возможность создать такой модуль выбрав `Dynamic Feature` при создании модуля.

### Instant App Updates
Позволяет обновить приложение пока оно запущено.
В андроид студии есть возможность создать такой модуль выбрав `Instant Dynamic Feature` при создании модуля.