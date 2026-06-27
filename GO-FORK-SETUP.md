# Coders Gym — форк с поддержкой Go

Этот форк добавляет язык **Go** в [codersgym](https://github.com/GouravShDev/codersgym).
Код выполняется и проверяется на серверах самого LeetCode (slug `golang`), поэтому
отдельный «judge» не нужен — работает как и для остальных языков.

## Что изменено

- **Go в редакторе:**
  - `lib/features/code_editor/domain/model/programming_language.dart` — значение `golang`
    в enum, подсветка (`go`), отображение «Go», маппинг форматтера.
  - `lib/features/code_editor/domain/model/code_experience_sample_code.dart` — пример Go-кода.
  - Выбор языка, подстановка стартового шаблона и отправка `lang: golang` на Run/Submit
    подхватываются автоматически (приложение использует имя enum как LeetCode-slug).
- **Firebase сделан «тихим»:** аналитика и Crashlytics отключены в `lib/main.dart`
  (форк переиспользует Firebase-проект апстрима только для тех. инициализации — данные не отправляются).
- **Подпись релиза:** в `android/app/build.gradle` релиз падает на debug-ключ, если нет
  `android/key.properties` — собственный keystore не нужен.
- **CI:** `.github/workflows/build-apk.yml` собирает APK в облаке. Старый релизный
  workflow апстрима (`main.yml`, Shorebird/Fastlane/Play Store) удалён.

## Как получить APK на телефон

1. Залогинься на GitHub и сделай **Fork** этого репозитория (или запушь эти изменения в свой репозиторий).
2. Вкладка **Actions** → workflow **Build APK** → **Run workflow** (ветка `main`).
   Первая сборка идёт ~10–15 мин.
3. Открой завершённый запуск → блок **Artifacts** → скачай `codersgym-go-apk`
   (zip с `app-release.apk`).
4. Перекинь APK на телефон, разреши «Установку из неизвестных источников», установи.
5. В приложении войди в свой аккаунт **LeetCode** (встроенный логин) — Run и Submit
   пойдут уже от твоего имени.

## Использование Go

Открой задачу → в редакторе выбери **Go** в выпадающем списке языков → стартовый шаблон
подтянется с LeetCode → жми **Run** / **Submit**.

## Дальше (опционально)

- Подключить свой Firebase (`flutterfire configure`) или полностью вырезать Firebase.
- Своя подпись релиза: keystore + `android/key.properties`.
- Сменить `applicationId`, если хочешь ставить рядом с оригинальным Coders Gym
  (тогда нужен свой `google-services.json` либо удаление Firebase).
- Авто-форматирование Go сейчас отключено (не проверял эндпоинт LeetCode `lsp-go`);
  можно включить позже, убрав `golang` из `formatUnSupportedLanguages`.
