# 11. CSS-псевдоэлементы. before и after

> **Курс:** Бесплатный курс по верстке сайтов (Front Developer)  
> **Канал:** Фрилансер по жизни  
> **Урок:** №11  
> **Папка:** `11-css-pseudo-elements/`  
> **Тема видео:** CSS псевдоэлементы. Псевдоэлементы BEFORE и AFTER. Уроки HTML CSS JS. Урок №11

---

## Цель урока

Познакомиться с псевдоэлементами CSS: `::first-line`, `::first-letter`,
`::before`, `::after`. Научиться создавать генерируемый контент
и применять псевдоэлементы на практике.

---

## Что такое псевдоэлементы

**Псевдоэлемент** — это селектор, который создаёт **новую сущность**,
которой нет в HTML-документе. Браузер «достраивает» её при отрисовке.

Псевдоэлементы позволяют:

- стилизовать часть элемента, к которой нельзя обратиться через HTML
  (первая строка, первая буква);
- добавлять декоративный контент до или после элемента.

### Псевдокласс vs псевдоэлемент

| Псевдокласс | Псевдоэлемент |
|---|---|
| Выбирает элемент в состоянии | Создаёт новую сущность |
| `:hover`, `:focus`, `:first-child` | `::before`, `::after`, `::first-line` |
| Одно двоеточие | Двойное двоеточие |

---

## Синтаксис

Стандартный синтаксис CSS3 — **двойное двоеточие**:

```css
p::first-line { color: green; }
p::before { content: '★'; }
Двойное двоеточие было введено, чтобы отличать псевдоэлементы
от псевдоклассов. Для совместимости браузеры принимают
и одинарное двоеточие (:before), но в новом коде его использовать
не рекомендуется.

Важно: в одном селекторе может быть только один псевдоэлемент.

::first-line
Стилизует первую строку текста в блоке.

css
.text::first-line {
    color: green;
}
Особенность: длина первой строки зависит от ширины блока, шрифта,
размера окна браузера. Если окно изменится — граница строки сдвинется.

Какие свойства применимы:

все свойства шрифта (font, font-size, font-weight и др.);

color, opacity;

свойства фона (background, background-color);

word-spacing, letter-spacing, text-decoration, text-transform,
line-height.

::first-letter
Стилизует первую букву текста в блоке.

css
.text::first-letter {
    font-size: 50px;
    color: red;
}
Часто используется для буквицы (drop cap) — большой первой буквы,
как в книгах.

Какие свойства применимы: шрифт, цвет, фон, отступы, границы,
float, vertical-align.

::before и ::after
Создают генерируемый контент до или после содержимого элемента.

::before — контент перед содержимым;

::after — контент после содержимого.

Обязательное условие: свойство content. Без него псевдоэлемент
не отобразится.

css
.list li::before {
    content: '';
    width: 10px;
    height: 10px;
    background-color: greenyellow;
    display: inline-block;
    border-radius: 50%;
    margin-right: 10px;
}
Свойство content
Что можно передать в content:

css
content: '';                /* пустая строка — для декоративных элементов */
content: '★';               /* символ */
content: '»';               /* кавычка */
content: url('icon.png');   /* изображение */
content: attr(data-label);  /* значение HTML-атрибута */
Ограничения display
По умолчанию ::before и ::after имеют display: inline.
Поэтому, чтобы задать width и height, нужно изменить display
на inline-block или block.

По спецификации CSS2:

если родитель — блочный элемент, display может быть none,
inline, block, list-item;

если родитель — строчный элемент, display может быть none
или inline.

На практике современные браузеры поддерживают inline-block, что делает
это ограничение менее строгим.

Вендорные псевдоэлементы
Некоторые псевдоэлементы не входят в стандарт и работают только
в конкретных браузерах:

Псевдоэлемент	Браузер	Назначение
::-ms-clear	IE, старый Edge	Кнопка очистки поля ввода
::-moz-focus-inner	Firefox	Внутренняя рамка фокуса
css
/* Убрать кнопку очистки в IE */
input::-ms-clear {
    display: none;
}

/* Убрать внутреннюю рамку фокуса в Firefox */
button::-moz-focus-inner {
    border: 0;
}
Сегодня используются редко, но полезны для кроссбраузерной стилизации.

Доступность и псевдоэлементы
Важно: контент, созданный через ::before и ::after,
не читается скринридерами и не индексируется поисковыми системами.

Поэтому:

не размещайте в псевдоэлементах смысловой контент;

используйте их только для декоративных элементов;

если контент важен — добавляйте его в HTML.

Практические применения
1. Декоративные маркеры списка
css
.list li::before {
    content: '';
    width: 8px;
    height: 8px;
    background: green;
    border-radius: 50%;
    display: inline-block;
    margin-right: 10px;
}
2. Иконки
css
.link::after {
    content: ' →';
    color: blue;
}
3. Буквица
css
p::first-letter {
    font-size: 3em;
    float: left;
    margin-right: 5px;
}
4. Очистка float (clearfix)
css
.clearfix::after {
    content: '';
    display: table;
    clear: both;
}
5. Стилизация выделения
css
::selection {
    background: yellow;
    color: black;
}
Пример: стилизация списка
html
<ul class="list">
    <li>Первый элемент</li>
    <li>Второй элемент</li>
    <li>Третий элемент</li>
</ul>
css
.list {
    list-style: none;
    padding: 0;
}

.list li {
    font-size: 24px;
    margin-bottom: 20px;
}

.list li::before {
    content: '';
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background-color: greenyellow;
    display: inline-block;
    margin-right: 10px;
}

.list li:hover::before {
    background-color: crimson;
}

.list li::after {
    content: '»';
    margin-left: 10px;
    color: gray;
}
Частые ошибки
Ошибка	Последствие	Как исправить
Забыть content	Псевдоэлемент не отображается	Добавить content: ''
Использовать :before вместо ::before	Устаревший синтаксис	Использовать ::before
Задавать width/height без display	Не работает (inline)	Добавить display: inline-block
Размещать смысловой контент в ::before	Не читается скринридерами	Перенести в HTML
Несколько псевдоэлементов в одном селекторе	Невалидно	Один псевдоэлемент на селектор
Использовать ::before для маркеров списка	Работает, но устарело	Использовать ::marker
Практика
Задание 1. Буквица
Создай абзац текста и стилизуй первую букву:

font-size: 3em;

color: red;

float: left;

margin-right: 5px.

Задание 2. Декоративный список
Создай маркированный список и замени стандартные маркеры
на круглые точки через ::before:

css
.list li::before {
    content: '';
    width: 10px;
    height: 10px;
    background: green;
    border-radius: 50%;
    display: inline-block;
    margin-right: 10px;
}
Задание 3. Стрелки после ссылок
Добавь после каждой ссылки стрелку → через ::after.

Задание 4 (дополнительное). ::selection
Стилизуй выделенный текст:

css
::selection {
    background: yellow;
    color: black;
}
Выдели текст мышью — фон должен стать жёлтым.

Полезные ссылки
MDN: Псевдоэлементы

MDN: ::before

MDN: ::after

MDN: ::first-line

MDN: ::first-letter

W3C: Selectors Level 4 — Pseudo-elements

Итоги
Псевдоэлементы создают сущности, которых нет в HTML.

Стандартный синтаксис — двойное двоеточие (::before).

::first-line и ::first-letter стилизуют части текста.

::before и ::after создают генерируемый контент (нужен content).

По умолчанию ::before и ::after — строчные (display: inline).

Контент из псевдоэлементов не читается скринридерами.

Вендорные псевдоэлементы (::-ms-clear, ::-moz-focus-inner)
нужны для кроссбраузерности.
