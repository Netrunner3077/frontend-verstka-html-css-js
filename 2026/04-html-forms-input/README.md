# 04. HTML-теги форм. HTML input

> **Курс:** Бесплатный курс по верстке сайтов (Front Developer)
> **Канал:** Фрилансер по жизни
> **Урок:** №4
> **Папка:** `04-html-forms-input/`
> **Тема видео:** HTML уроки. HTML теги форм. HTML input. Уроки HTML CSS JS. Урок №4

---

## Цель урока

Научиться создавать HTML-формы: `<form>`, `<input>`, `<textarea>`,
`<select>`, `<button>`. Понять, как передаются данные на сервер
и какие атрибуты управляют поведением полей.

---

## Что такое форма

**Форма** — это набор полей ввода, объединённых в один блок,
который отправляет данные на сервер. Форма нужна везде, где пользователь
что-то вводит: регистрация, вход, поиск, обратная связь, оформление заказа.

---

## Тег `<form>`

`<form>` — оболочка для формы. Она группирует поля и отвечает за отправку.

### Атрибут `action`

Указывает **адрес**, куда браузер отправит данные после нажатия
кнопки «Отправить».

```html
<form action="/submit">
```

Если `action` не указан, данные уйдут на текущий URL.

### Атрибут `method`

HTTP-метод отправки. Два основных значения:

- `get` — данные добавляются в URL после знака `?`;
- `post` — данные передаются в теле HTTP-запроса.

```html
<form action="/search" method="get">
<form action="/register" method="post">
```

### Атрибут `enctype`

Способ кодирования данных:

- `application/x-www-form-urlencoded` — по умолчанию;
- `multipart/form-data` — обязательно для загрузки файлов (`<input type="file">`);
- `text/plain` — редко используется.

Работает только с `method="post"`. С `get` игнорируется.

```html
<form action="/upload" method="post" enctype="multipart/form-data">
```

### Атрибут `novalidate`

Отключает встроенную браузерную валидацию (например, проверку `required`).

```html
<form action="/register" method="post" novalidate>
```

### Атрибут `autocomplete`

Управляет автозаполнением браузером.

- `on` (по умолчанию) — браузер может предлагать значения;
- `off` — отключено.

```html
<form action="/login" method="post" autocomplete="off">
```

## GET и POST

| | GET | POST |
| --- | --- | --- |
| Где данные | В URL (`?key=value&...`) | В теле запроса |
| Видны в адресной строке | Да | Нет |
| Шифрование | Нет (только через HTTPS) | Нет (только через HTTPS) |
| Объём | Ограничен длиной URL | Большой |
| Файлы | Нет | Да (с `enctype`) |
| Кэширование | Да | Нет |
| Закладка | Да | Нет |
| Применение | Поиск, фильтры | Регистрация, вход, загрузка |

**Важно:** POST не «безопаснее» GET сам по себе. Ни один из них не шифрует данные.
Безопасность обеспечивает HTTPS.

Пароли и чувствительные данные — только POST. С GET пароль попадёт в URL,
историю браузера и логи сервера.

## Тег `<input>`

`<input>` — основной элемент формы. Пустой (void) элемент: закрывающего тега нет.
Внешний вид и поведение определяет атрибут `type`.

### Основные типы

| Тип | Назначение |
| --- | --- |
| `text` | Однострочный текст |
| `password` | Пароль (символы скрыты) |
| `email` | Email (с валидацией формата) |
| `tel` | Телефон |
| `number` | Число |
| `date` | Дата |
| `file` | Файл |
| `radio` | Радиокнопка (один из нескольких) |
| `checkbox` | Флажок (несколько из нескольких) |
| `hidden` | Скрытое поле |
| `submit` | Кнопка отправки |
| `reset` | Кнопка сброса |
| `color` | Выбор цвета |
| `range` | Ползунок |
| `search` | Поле поиска |

```html
<input type="text" name="username">
<input type="password" name="userpass">
<input type="email" name="email">
<input type="tel" name="phone">
<input type="file" name="photo">
<input type="radio" name="gender" value="male">
<input type="checkbox" name="subscribe" value="yes">
```

### Атрибут `name`

Имя поля. Формирует пару «имя → значение» при отправке.

```html
<input type="text" name="username" value="Иван">
```

На сервер уйдёт: `username=Иван`.

**Важно:** если у поля нет `name`, оно не отправится на сервер.
У всех radio в одной группе `name` должен быть одинаковым.

### Атрибут `value`

Значение по умолчанию (для `text`, `password`) или значение, которое
отправится при выборе (для `radio`, `checkbox`).

```html
<input type="radio" name="sex" value="male">
```

При выборе этой радиокнопки уйдёт `sex=male`.

### Атрибут `placeholder`

Подсказка внутри поля. Исчезает при начале ввода.

```html
<input type="text" name="username" placeholder="Введите логин">
```

**Важно:** `placeholder` не заменяет `<label>`. Он не читается
скринридерами как подпись поля и исчезает при вводе — пользователь может
забыть, что вводил.

### Атрибут `required`

Поле обязательно для заполнения. Браузер не отправит форму, пока оно пустое.

```html
<input type="text" name="username" required>
```

### Атрибут `disabled`

Отключает поле:

- не фокусируется;
- не участвует в валидации;
- не отправляется на сервер.

```html
<input type="tel" name="phone" disabled>
```

### Атрибут `readonly`

Только для чтения: пользователь не может изменить значение,
но поле отправляется на сервер. Работает для текстовых полей и textarea.

```html
<input type="text" name="id" value="123" readonly>
```

### Атрибут `checked`

Для radio и checkbox — выбран по умолчанию.

```html
<input type="radio" name="sex" value="male" checked>
<input type="checkbox" name="rules" value="yes" checked>
```

**Правило radio:** в одной группе (одинаковый `name`) может быть выбран
только один radio. Если поставить `checked` на два — браузер выберет последний.

### Атрибут `tabindex`

Порядок перехода между элементами при нажатии Tab.

- `tabindex="0"` — стандартный порядок (по разметке);
- `tabindex="-1"` — элемент исключён из Tab, но доступен программно;
- `tabindex="N>0"` — жёсткий порядок (1, 2, 3...).

**Современная практика:** положительные значения не рекомендуются —
они ломают естественный порядок обхода и вредят доступности.
Лучше полагаться на порядок элементов в разметке.

### Атрибуты `maxlength` и `minlength`

Максимальное и минимальное количество символов.

```html
<input type="text" name="username" minlength="3" maxlength="20">
```

## Тег `<label>` — метка поля

`<label>` связывает подпись с полем. Клик по тексту фокусирует поле
или переключает radio/checkbox. Это критично для доступности:
скринридеры читают label вслух.

### Способ 1: через `for` и `id`

```html
<label for="username">Имя пользователя</label>
<input id="username" type="text" name="username">
```

Атрибут `for` у `<label>` должен совпадать с `id` у `<input>`.

### Способ 2: обёртка

```html
<label>
    Имя пользователя
    <input type="text" name="username">
</label>
```

### Для radio и checkbox

```html
<label>
    <input type="radio" name="sex" value="male">
    Мужчина
</label>
```

Теперь клик по тексту «Мужчина» выбирает радиокнопку.

## `<fieldset>` и `<legend>`

`<fieldset>` группирует связанные поля, `<legend>` — заголовок группы.

```html
<fieldset>
    <legend>Пол</legend>
    <label><input type="radio" name="sex" value="male"> Мужчина</label>
    <label><input type="radio" name="sex" value="female"> Женщина</label>
</fieldset>
```

Особенно полезно для radio-групп: скринридер прочитает заголовок
перед вопросами.

## `<textarea>` — многострочное поле

Для ввода длинного текста (комментарии, описания, сообщения).

```html
<textarea name="comment" rows="5" cols="30"></textarea>
```

Особенности:

- это не пустой элемент, у него есть закрывающий тег;
- значение задаётся не через `value`, а между тегами:

```html
<textarea name="comment">Текст по умолчанию</textarea>
```

## `<select>` и `<option>` — выпадающий список

```html
<select name="country">
    <option value="ru">Россия</option>
    <option value="us">США</option>
    <option value="cn" selected>Китай</option>
</select>
```

- `<select>` — сам список;
- `<option>` — пункт списка;
- `selected` у `<option>` — выбран по умолчанию;
- атрибут `multiple` у `<select>` позволяет выбрать несколько значений.

## `<button>` — кнопка

```html
<button type="submit">Отправить</button>
<button type="reset">Очистить</button>
<button type="button">Просто кнопка</button>
```

### Типы

- `submit` — отправляет форму (по умолчанию, если `type` не указан);
- `reset` — сбрасывает все поля к начальным значениям;
- `button` — ничего не делает сам по себе (для JS).

**Важно:** внутри формы всегда указывай `type` явно. Без указания
`<button>` ведёт себя как `submit`, что может быть неожиданно.

## Валидация

Браузер умеет проверять поля до отправки — без JavaScript.

| Атрибут | Что проверяет |
| --- | --- |
| `required` | Поле заполнено |
| `minlength` / `maxlength` | Длина текста |
| `min` / `max` | Диапазон числа или даты |
| `type="email"` | Формат email |
| `type="url"` | Формат URL |
| `type="number"` | Что введено число |
| `pattern` | Регулярное выражение |

```html
<input type="email" name="email" required>
<input type="number" name="age" min="18" max="99">
```

Если поле не проходит валидацию, браузер покажет подсказку и не отправит форму.

Отключить валидацию можно атрибутом `novalidate` на `<form>`.

## Пример: полная форма

```html
<form action="/register" method="post" enctype="multipart/form-data">
    <fieldset>
        <legend>Регистрация</legend>

        <p>
            <label for="username">Логин</label>
            <input id="username" type="text" name="username" required>
        </p>

        <p>
            <label for="password">Пароль</label>
            <input id="password" type="password" name="userpass" required>
        </p>

        <p>
            <label for="email">Email</label>
            <input id="email" type="email" name="email" required>
        </p>

        <fieldset>
            <legend>Пол</legend>
            <label><input type="radio" name="sex" value="male" checked> Мужчина</label>
            <label><input type="radio" name="sex" value="female"> Женщина</label>
        </fieldset>

        <p>
            <label>
                <input type="checkbox" name="rules" value="yes">
                Согласие на обработку персональных данных
            </label>
        </p>

        <p>
            <label for="photo">Фотография</label>
            <input id="photo" type="file" name="photo">
        </p>

        <p>
            <label for="about">О себе</label>
            <textarea id="about" name="about" rows="4"></textarea>
        </p>

        <p>
            <label for="country">Страна</label>
            <select id="country" name="country">
                <option value="ru" selected>Россия</option>
                <option value="us">США</option>
                <option value="cn">Китай</option>
            </select>
        </p>

        <button type="submit">Отправить</button>
        <button type="reset">Очистить</button>
    </fieldset>
</form>
```

## Частые ошибки

| Ошибка | Последствие | Как исправить |
| --- | --- | --- |
| Нет `name` у поля | Поле не отправится на сервер | Добавить `name` |
| Нет `<label>` | Форма недоступна для скринридеров | Обернуть в `<label>` или связать через `for`/`id` |
| Использовать GET для пароля | Пароль попадёт в URL и логи | Использовать POST |
| `enctype` без post | Игнорируется | Указывать вместе с `method="post"` |
| Разные `name` у radio одной группы | Можно выбрать несколько | Одинаковый `name` |
| `<button>` без `type` | Ведёт себя как `submit` | Всегда указывать `type` |
| `tabindex` с положительными числами | Ломает порядок обхода | Использовать порядок в разметке |
| `placeholder` вместо `label` | Плохо для доступности | Использовать `<label>` |

## Практика

### Задание 1. Форма регистрации

Создай форму со следующими полями:

- логин (`text`, `required`);
- пароль (`password`, `required`);
- email (`email`, `required`);
- телефон (`tel`);
- пол (`radio`);
- согласие (`checkbox`);
- фотография (`file`);
- о себе (`textarea`);
- страна (`select`);
- кнопки «Отправить» и «Очистить».

Все поля должны быть обёрнуты в `<label>`.

### Задание 2. Свяжи label и input

Проверь: клик по подписи должен фокусировать поле.
Если не работает — проверь совпадение `for` и `id`.

### Задание 3. Валидация

Добавь `required` к обязательным полям.
Попробуй отправить пустую форму — браузер должен показать подсказку.

### Задание 4 (дополнительное). Методы GET и POST

Поменяй `method="get"` на `method="post"` и наоборот.
Посмотри в адресной строке, как меняется URL после отправки.
Попробуй отправить форму с `enctype="multipart/form-data"` без файла —
что произойдёт?

## Полезные ссылки

- [MDN: Формы](https://developer.mozilla.org/ru/docs/Learn_web_development/Extensions/Forms)
- [MDN: `<form>`](https://developer.mozilla.org/ru/docs/Web/HTML/Reference/Elements/form)
- [MDN: `<input>`](https://developer.mozilla.org/ru/docs/Web/HTML/Reference/Elements/input)
- [MDN: `<label>`](https://developer.mozilla.org/ru/docs/Web/HTML/Reference/Elements/label)
- [MDN: `<fieldset>`](https://developer.mozilla.org/ru/docs/Web/HTML/Reference/Elements/fieldset)
- [MDN: `<select>`](https://developer.mozilla.org/ru/docs/Web/HTML/Reference/Elements/select)
- [MDN: `<textarea>`](https://developer.mozilla.org/ru/docs/Web/HTML/Reference/Elements/textarea)
- [MDN: Валидация форм](https://developer.mozilla.org/ru/docs/Learn_web_development/Extensions/Forms/Form_validation)

## Итоги

- `<form>` — оболочка формы. Атрибуты: `action`, `method`, `enctype`, `novalidate`, `autocomplete`.
- GET — данные в URL, POST — в теле запроса. Пароли — только POST.
- `<input>` — основное поле. Типы: `text`, `password`, `email`, `tel`, `file`, `radio`, `checkbox` и др.
- `name` — имя поля для отправки; без него данные не уйдут.
- `placeholder` — подсказка, исчезает при вводе. Не заменяет `<label>`.
- `<label>` связывает подпись с полем. Критично для доступности.
- `<fieldset>` / `<legend>` — группировка полей.
- `<textarea>` — многострочное поле. Значение — между тегами.
- `<select>` / `<option>` — выпадающий список. `selected` — по умолчанию.
- `<button>` — всегда указывай `type` явно.
- Валидация: `required`, `minlength`, `maxlength`, `pattern`, `min`, `max`.
