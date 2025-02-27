# Что я сделал?

## Добавлены конфиги для локальной проверки сообщений коммитов с помощью commitlint а также проверка коммита при pull_request'е

## Настроен автоматический запуск проверок при pull request'е

- Запускаются автотесты (.github/workflows/testing.yml)
- Проверка запускается на каждый открытый PR и отображается
- Настроено ограничение на слияние если проверка еще не пройдена или завалена

## Частично настроен релизный процесс

- Автоматический запуск при появлении в git нового релизного тега
- Версия релиза соответствует тегу
- Создается issue со всей информацией
- Запускаются тесты
- После успешного прохождения тестов результат выкладывается на github pages
- (Не реализовано) изменение issue

## Как проверять это всё?

- Проверка коммитов запускается на pull request (и теперь и на пуш), работать нужно с веткой dev и потом делать pull request в master (я делал pull request'ы через интерфейс гитхаба)
- При создании pr запускаются тесты. Без них нельзя завершить pr (кнопка заблокирована в процессе проверки и при неудачном прохождении тестов)
- Для проверки релизного процесса нужно сделать пуш и затем добавить тег (которого еще не было). Это можно сделать так:
- issue обновляется если запушить тот же тег (должно, но не проверил), но информация о тестах и деплое не добавляется

```sh
# создаем тег
git tag -a v15 -m "version 15"
# Отправляем коммиты
git push
# Отправляем теги
git push --tags
```

Это запустит релизный процесс. Сперва создастся issue со всеми данными. Затем запустятся тесты. При успешном выполнении тестов результат выложится на github pages и в ветку gh-pages.

#

В этом репозитории находится пример приложения с тестами:

- [e2e тесты](e2e/example.spec.ts)
- [unit тесты](src/example.test.tsx)

Для запуска примеров необходимо установить [NodeJS](https://nodejs.org/en/download/) 16 или выше.

Как запустить:

```sh
# установить зависимости
npm ci

# запустить приложение
npm start
```

Как запустить e2e тесты:

```sh
# скачать браузеры
npx playwright install

# запустить тесты
npm run e2e
```

Как запустить модульные тесты:

```sh
npm test
```
