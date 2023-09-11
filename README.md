
# Возможные варианты подключения стилей для Laravel версии 9 и 10

## Вариант 1: Загрузка CSS непосредственно из каталога `/public`

**1.** Создайте или используйте существующую папку в директории `/public` и сохраните в ней свой файл CSS. Например, вы можете сохранить его как `/public/css/styles.css`.

**2.** Добавьте следующий код в ваш шаблон blade в разделе `head` blade-файла вашей страницы:
```
<link rel="stylesheet" href="{{ asset('css/styles.css') }}">
```

## Вариант 2: Загрузка CSS из каталога `/resources` с помощью Vite

**1.** Создайте или используйте существующую папку в каталоге `/resources` и сохраните в ней свой CSS-файл. Например, вы можете сохранить его как `/resources/css/style.css`, но лучше не менять название по-умолчанию `app.css`.

**2.** Посмотреть файл `vite.config.js`, который из коробки должен иметь следующий вид:
```
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
    ],
});
```

**3.** Выполните следующую команду npm для создания минифицированного файла CSS, который будет храниться в папке `/public`:

#### **npm**:
```
npm run build
```
#### **yarn**:
```
yarn build
```

*Перед использование этих команд, убедитесь, что у вас установлены все пакеты командами:*
#### **npm**:
```
npm i
```
#### **yarn**:
```
yarn
```

**4.** Добавьте следующую директиву `@vite` в ваш шаблон blade для подключения CSS:
```
@vite(['resources/css/app.css'])
```

**5.** Теперь перезагрузите страницу, и стилизация CSS будет применена корректно.

## Вариант 3: Загрузка CSS из CDN URL

**1.** Найдите URL CDN, где размещён файл CSS, который вы хотите использовать.

**2.** Добавьте приведённый ниже код в файл шаблона blade вашего приложения Laravel:
```
# Пример подключения стилей bootstrap через CDN

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet">
```