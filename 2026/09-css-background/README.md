# 09. CSS: свойство background

> **Курс:** Бесплатный курс по верстке сайтов (Front Developer)  
> **Канал:** Фрилансер по жизни  
> **Урок:** №9  
> **Папка:** `09-css-background/`  
> **Тема видео:** CSS свойство BACKGROUND. Делаем фон для сайта // Уроки HTML CSS JS. Урок №9

---

## Цель урока

Изучить свойства фона в CSS: `background-color`, `background-image`,
`background-repeat`, `background-position`, `background-size`,
`background-attachment`. Научиться работать с градиентами
и множественными фонами.

---

## Что такое фон

**Фон** — это область под содержимым элемента. Фон может быть:

- сплошным цветом;
- изображением;
- градиентом;
- комбинацией нескольких слоёв.

Фон **не влияет** на размеры элемента и поток документа.

---

## `background-color` — цвет фона

```css
p {
    background-color: #18b5a4;              /* hex */
    background-color: rgb(24, 181, 164);    /* rgb */
    background-color: rgba(24, 181, 164, 0.5); /* с прозрачностью */
    background-color: transparent;          /* по умолчанию */
}
rgba() — цвет с альфа-каналом (прозрачностью от 0 до 1).
В отличие от opacity, влияет только на фон, а не на весь элемент.

Современные способы: hsl(), hsla(), oklch().

background-image — фоновое изображение
css
p {
    background-image: url("img/photo.jpg");
}
Путь к изображению указывается в url() относительно CSS-файла.

Несколько изображений — через запятую:

css
p {
    background-image: url("top.png"), url("bottom.png");
}
Порядок слоёв: первое изображение в списке — сверху, последнее — снизу.

background-repeat — повторение
css
p {
    background-repeat: no-repeat;
}
Значение	Описание
repeat	По горизонтали и вертикали (по умолчанию)
no-repeat	Без повторений
repeat-x	Только по горизонтали
repeat-y	Только по вертикали
space	Повторяется с равными промежутками
round	Повторяется с масштабированием до целого числа
background-position — позиция
css
p {
    background-position: center;          /* по центру */
    background-position: top left;        /* левый верхний угол */
    background-position: 100% 100%;       /* правый нижний угол */
    background-position: 25px 30px;       /* точные координаты */
}
Синтаксис: X Y — горизонталь и вертикаль.

Ключевые слова: left, center, right (по горизонтали);
top, center, bottom (по вертикали).

Проценты: 50% 50% — центр. 0% 0% — левый верхний угол.

background-size — размер
css
p {
    background-size: auto;          /* исходный размер */
    background-size: 100% auto;     /* ширина 100%, высота авто */
    background-size: cover;         /* покрыть всю область */
    background-size: contain;       /* поместиться целиком */
    background-size: 200px 150px;   /* точные размеры */
}
Значение	Описание
auto	Исходный размер изображения
<length>	Точный размер (px, em, rem)
<percentage>	Процент от области позиционирования
cover	Наименьший размер, полностью покрывающий область
contain	Наибольший размер, при котором изображение целиком помещается
При одном значении — задаёт ширину, высота — auto.
При двух значениях — первое ширина, второе высота.

cover vs contain
cover	contain
Покрытие	Полное	Неполное (могут быть пустые области)
Обрезка	Да (если пропорции не совпадают)	Нет
Пропорции	Сохраняются	Сохраняются
background-attachment — привязка
css
p {
    background-attachment: scroll;
}
Значение	Описание
scroll	Фон фиксирован относительно элемента (по умолчанию)
fixed	Фон фиксирован относительно вьюпорта (эффект параллакса)
local	Фон прокручивается вместе с содержимым элемента
fixed создаёт эффект параллакса: при прокрутке страницы фон остаётся на месте.

local полезен, когда у элемента есть собственная прокрутка (overflow: auto) — фон движется вместе с содержимым.

Градиенты
Градиент — это плавный переход между цветами. В CSS градиент — это
изображение, поэтому он задаётся через background-image или background.

Линейный градиент linear-gradient()
css
p {
    background: linear-gradient(to bottom, #fefcea, #f1da36);
    background: linear-gradient(45deg, red, blue);
    background: linear-gradient(to right, red 0%, green 50%, blue 100%);
}
Синтаксис: linear-gradient(направление, цвет1, цвет2, ...).

Направление: to top, to bottom, to right, to left,
to top right или угол в градусах (45deg).

Радиальный градиент radial-gradient()
css
p {
    background: radial-gradient(circle, red, blue);
    background: radial-gradient(ellipse at center, red, blue);
}
Синтаксис: radial-gradient(форма размер at позиция, цвет1, цвет2, ...).

Конический градиент conic-gradient()
css
p {
    background: conic-gradient(red, orange, yellow, green, blue);
}
Синтаксис: conic-gradient(угол, цвет1, цвет2, ...).

Конический градиент — цвета располагаются вокруг центральной точки.
Поддерживается всеми современными браузерами с 2020 года.

Повторяющиеся градиенты
css
p {
    background: repeating-linear-gradient(45deg, red, blue 20px);
}
Множественные фоны
CSS позволяет задать несколько фоновых изображений через запятую.

css
p {
    background-image: url("top.png"), url("bottom.png");
    background-repeat: no-repeat, repeat;
    background-position: top left, bottom right;
    background-size: auto, cover;
}
Правила:

Каждое свойство (background-image, background-repeat,
background-position, background-size) принимает список значений.

Значения разделяются запятыми и соответствуют слоям по порядку.

background-color — только для последнего слоя.

Первый слой — сверху, последний — снизу.

Shorthand background
css
p {
    background: url("image.png") no-repeat center / cover #eee;
}
Порядок значений (частично регламентирован):

<background-color> — только в последнем слое;

<bg-image> — url() или gradient();

<bg-position> — позиция;

/ <bg-size> — размер (строго после позиции через слэш);

<repeat-style> — повторение;

<attachment> — привязка;

<visual-box> — background-origin и/или background-clip.

Важно: если указаны position и size, они записываются через слэш:
center / cover.

Незаданные свойства сбрасываются в значения по умолчанию.

background-clip и background-origin
background-clip — обрезка фона
css
p {
    background-clip: border-box;    /* по умолчанию */
    background-clip: padding-box;   /* до внутреннего края границы */
    background-clip: content-box;   /* только под содержимым */
    background-clip: text;          /* обрезка по тексту */
}
background-clip: text — фон обрезается по форме текста. Используется
для эффекта «текст-градиент». Требует color: transparent:

css
p {
    background: linear-gradient(45deg, red, blue);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
}
background-origin — область позиционирования
css
p {
    background-origin: padding-box;   /* по умолчанию */
    background-origin: border-box;
    background-origin: content-box;
}
Определяет, относительно какой области позиционируется фон.

Практика
Задание 1. Цвет фона
Создай три блока с background-color в форматах hex, rgb, rgba.
Сравни результат.

Задание 2. Изображение и повторение
Создай блок с фоновым изображением. Попробуй все значения
background-repeat: repeat, no-repeat, repeat-x, repeat-y,
space, round.

Задание 3. Размеры
Создай три блока с одним изображением и разными background-size:
auto, cover, contain. Сравни.

Задание 4. Градиенты
Создай три блока: линейный, радиальный и конический градиенты.

Задание 5 (дополнительное). Параллакс
Создай блок с background-attachment: fixed. Убедись, что фон
не прокручивается вместе со страницей.

Задание 6 (дополнительное). practice-background.html
Создай hero-секцию с фоновым изображением, заголовком и кнопкой.
Используй linear-gradient поверх изображения для затемнения.

Полезные ссылки
MDN: background

MDN: background-image

MDN: background-size

MDN: background-attachment

MDN: Использование градиентов

MDN: Множественные фоны

CSS Gradient Generator

Итоги
background-color — цвет фона. rgba() даёт прозрачность только для фона.

background-image — изображение или градиент. Несколько — через запятую.

background-repeat — повторение: repeat, no-repeat, repeat-x, repeat-y, space, round.

background-position — позиция: ключевые слова, проценты, координаты.

background-size — размер: auto, cover, contain, <length>.

background-attachment — привязка: scroll (по умолчанию), fixed (параллакс), local (со скроллом).

Градиенты: linear-gradient(), radial-gradient(), conic-gradient().

Множественные фоны: первый слой — сверху, background-color — только для последнего.

Shorthand background: position / size — строго через слэш.

background-clip: text — текст с фоновым изображением.

Вендорные префиксы для градиентов не нужны.
