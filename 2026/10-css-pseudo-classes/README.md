# 10. CSS: псевдоклассы

> **Курс:** Бесплатный курс по верстке сайтов (Front Developer)
> **Канал:** Фрилансер по жизни
> **Урок:** №10
> **Папка:** `10-css-pseudo-classes/`
> **Тема видео:** CSS псевдоклассы. Псевдокласс HOVER и другие. Уроки HTML CSS JS. Урок №10

---

## Цель урока

Изучить псевдоклассы CSS: научиться стилизовать элементы в зависимости
от их состояния (`:hover`, `:focus`, `:active`) и положения в документе
(`:first-child`, `:nth-child`). Понять, как псевдоклассы помогают
создавать интерактивные интерфейсы без JavaScript.

---

## Что такое псевдоклассы

**Псевдокласс** — это ключевое слово, которое добавляется к селектору
через двоеточие и позволяет выбрать элементы в определённом **состоянии**
или **положении**.

**Синтаксис:**

```css
селектор:псевдокласс {
    свойство: значение;
}
```

Примеры:

```css
a:hover { color: red; }           /* при наведении */
li:first-child { font-weight: bold; }  /* первый элемент списка */
input:focus { border-color: blue; }    /* поле в фокусе */
```

**Важно:** псевдокласс отличается от псевдоэлемента. Псевдокласс выбирает
элемент в особом состоянии (`:hover`), псевдоэлемент создаёт виртуальную
часть элемента (`::before`). Подробнее — в уроке №11.

## Псевдоклассы состояния

Эти псевдоклассы срабатывают при взаимодействии пользователя с элементом.

### `:hover` — наведение

Срабатывает, когда курсор мыши находится над элементом.

```css
a:hover {
    color: red;
    text-decoration: underline;
}

.block:hover {
    background-color: rgba(165, 240, 255, 0.5);
}
```

**Современная практика:** на сенсорных устройствах `:hover` может
«залипать» после тапа. Оборачивайте `:hover`-правила в медиа-запрос:

```css
@media (hover: hover) {
    .btn:hover { background: darkgrey; }
}
```

### `:active` — активный (нажатие)

Срабатывает в момент нажатия на элемент. Обычно применяется к ссылкам
и кнопкам.

```css
.btn:active {
    background-color: green;
    transform: scale(0.98);
}
```

### `:focus` — фокус

Срабатывает, когда элемент получает фокус. Часто используется для
полей ввода.

```css
.inpt:focus {
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
}
```

**Проблема:** `:focus` срабатывает и при клике мышью, и при навигации
с клавиатуры. При клике контур фокуса может быть не нужен.

### `:focus-visible` — фокус для клавиатуры

Срабатывает только когда браузер считает, что пользователю действительно
нужен индикатор фокуса — обычно при навигации с клавиатуры, но не при
клике мышью.

```css
button:focus-visible {
    outline: 2px solid blue;
    outline-offset: 2px;
}
```

**Современная практика:** использовать `:focus-visible` вместо `:focus`
для интерактивных элементов. Это решает проблему «лишнего» контура
при клике мышью и сохраняет доступность для клавиатурных пользователей.

### `:focus-within` — фокус внутри

Срабатывает на родителе, когда фокус находится на одном из его
дочерних элементов.

```css
.form:focus-within {
    border-color: blue;
    box-shadow: 0 0 10px rgba(0, 0, 255, 0.2);
}
```

Полезно для подсветки всей формы при работе с любым её полем.

### `:visited` — посещённая ссылка

Срабатывает для ссылок, на которые пользователь уже заходил.

```css
a:visited {
    color: green;
}
```

**Ограничение безопасности:** браузеры разрешают менять у `:visited`
только ограниченный набор свойств (`color`, `background-color`,
`border-color`, `outline-color`, `text-decoration-color`).
Свойства `font-size`, `font-weight`, `display` и другие игнорируются.

### Порядок псевдоклассов ссылок (LVHA)

```css
a:link { ... }      /* L — link */
a:visited { ... }   /* V — visited */
a:hover { ... }     /* H — hover */
a:focus { ... }     /* F — focus */
a:active { ... }    /* A — active */
```

## Псевдоклассы положения

Эти псевдоклассы выбирают элементы по их позиции среди соседей.

### `:first-child` — первый ребёнок

Выбирает элемент, который является первым среди своих братьев и сестёр.

```css
li:first-child {
    color: crimson;
}
```

**Важно:** `:first-child` выбирает первый элемент в родителе, а не
первый элемент определённого типа. Если вы добавите новый элемент в начало,
`:first-child` выберет уже его.

### `:last-child` — последний ребёнок

Выбирает последний элемент в родителе.

```css
li:last-child {
    color: purple;
    font-weight: 700;
}
```

### `:nth-child()` — по порядковому номеру

Выбирает элементы по их позиции в родителе. Принимает:

- число: `:nth-child(3)` — третий элемент;
- `odd`: `:nth-child(odd)` — нечётные (1, 3, 5, ...);
- `even`: `:nth-child(even)` — чётные (2, 4, 6, ...);
- формулу An+B: `:nth-child(3n)` — каждый третий; `:nth-child(n+3)` — начиная с третьего; `:nth-child(-n+3)` — первые три.

```css
li:nth-child(3) {
    color: greenyellow;
    text-decoration: underline;
}

li:nth-child(odd) {
    text-transform: uppercase;
}

li:nth-child(even) {
    background-color: yellow;
}

li:nth-child(3n) {
    font-weight: bold;   /* каждый третий */
}
```

### `:nth-of-type()` — по типу элемента

В отличие от `:nth-child()`, считает только элементы определённого типа,
игнорируя остальных.

```css
p:nth-of-type(2) {
    color: red;   /* второй <p>, даже если между ними есть <div> */
}
```

### `:only-child` — единственный ребёнок

Срабатывает, если элемент — единственный ребёнок родителя.

```css
p:only-child {
    font-weight: bold;
}
```

### `:empty` — пустой элемент

Срабатывает для элементов без дочерних элементов и текста (даже пробелы
учитываются).

```css
div:empty {
    display: none;
}
```

## Псевдоклассы форм

### `:checked` — отмеченный

Для `<input type="checkbox">` и `<input type="radio">`.

```css
input:checked + label {
    font-weight: bold;
}
```

### `:disabled` / `:enabled`

```css
input:disabled {
    background-color: #eee;
    cursor: not-allowed;
}

input:enabled {
    background-color: #fff;
}
```

### `:required` / `:optional`

```css
input:required {
    border-left: 3px solid red;
}
```

### `:valid` / `:invalid`

```css
input:valid {
    border-color: green;
}

input:invalid {
    border-color: red;
}
```

## Другие полезные псевдоклассы

### `:not()` — отрицание

Выбирает элементы, не соответствующие указанному селектору.

```css
li:not(:last-child) {
    margin-bottom: 10px;   /* отступ у всех, кроме последнего */
}
```

### `:is()` — группировка

Упрощает запись, когда несколько селекторов имеют одинаковые стили.

```css
:is(h1, h2, h3):hover {
    color: blue;
}
```

### `:where()` — как `:is()`, но с нулевой специфичностью

```css
:where(h1, h2, h3) {
    margin: 0;
}
```

### `:target` — цель якоря

Срабатывает для элемента, на который указывает якорь в URL.

```css
section:target {
    background-color: yellow;
}
```

### `:root` — корневой элемент

Соответствует `<html>`. Используется для CSS-переменных.

```css
:root {
    --color-primary: #18b5a4;
}
```

## Комбинирование псевдоклассов

Псевдоклассы можно комбинировать:

```css
a:hover:focus {
    color: purple;
}

li:first-child:hover {
    background-color: yellow;
}
```

## Практика

### Задание 1. Ссылки

Создай ссылку. Задай разные стили для `:link`, `:visited`, `:hover`,
`:focus`, `:active`. Проверь порядок LVHA.

### Задание 2. Кнопка

Создай кнопку с `:hover` (изменение фона), `:active` (уменьшение),
`:focus-visible` (контур).

### Задание 3. Список

Создай список из 6 элементов. Задай:

- первому — красный цвет;
- последнему — жирный;
- третьему — подчёркивание;
- нечётным — uppercase;
- чётным — жёлтый фон.

### Задание 4. Форма

Создай форму с полями. Задай:

- `:focus` — тень;
- `:required` — красную левую границу;
- `:valid` — зелёную границу;
- `:invalid` — красную границу.

### Задание 5 (дополнительное). practice-pseudo-classes.html

Открой файл и выполни задание: создай список задач с чекбоксами,
используя `:checked`, `:hover`, `:nth-child` и `:not()`.

## Полезные ссылки

- [MDN: Псевдоклассы](https://developer.mozilla.org/ru/docs/Web/CSS/Reference/Selectors/Pseudo-classes)
- [MDN: `:hover`](https://developer.mozilla.org/ru/docs/Web/CSS/Reference/Selectors/:hover)
- [MDN: `:focus`](https://developer.mozilla.org/ru/docs/Web/CSS/Reference/Selectors/:focus)
- [MDN: `:focus-visible`](https://developer.mozilla.org/ru/docs/Web/CSS/Reference/Selectors/:focus-visible)
- [MDN: `:nth-child()`](https://developer.mozilla.org/ru/docs/Web/CSS/:nth-child)
- [MDN: Стилизация ссылок](https://developer.mozilla.org/ru/docs/Learn_web_development/Core/Text_styling/Styling_links)
- [W3C: Selectors Level 4](https://www.w3.org/TR/selectors-4/)

## Итоги

- Псевдокласс — ключевое слово после `:`, выбирает элементы по состоянию или положению.
- Состояние: `:hover`, `:active`, `:focus`, `:focus-visible`, `:focus-within`, `:visited`.
- Положение: `:first-child`, `:last-child`, `:nth-child()`, `:nth-of-type()`, `:only-child`, `:empty`.
- Формы: `:checked`, `:disabled`, `:enabled`, `:required`, `:valid`, `:invalid`.
- Другие: `:not()`, `:is()`, `:where()`, `:target`, `:root`.
- `:focus-visible` — современная замена `:focus` для доступности.
- `:visited` — ограничен по стилизации из соображений безопасности.
- `:nth-child()` принимает число, `odd`, `even` или формулу An+B.
- Порядок псевдоклассов ссылок: LVHA (`:link` → `:visited` → `:hover` → `:focus` → `:active`).
- `:hover` на сенсорных устройствах оборачивайте в `@media (hover: hover)`.
