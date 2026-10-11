# 08. CSS: оформление блоков. opacity, visibility

> **Курс:** Бесплатный курс по верстке сайтов (Front Developer)
> **Канал:** Фрилансер по жизни
> **Урок:** №8
> **Папка:** `08-css-block-styling-opacity/`
> **Тема видео:** Свойства и стили оформления блоков. CSS opacity. Уроки HTML CSS JS. Урок №8

---

## Цель урока

Изучить свойства оформления блоков: границы (`border`), скругления
(`border-radius`), контур (`outline`), тени (`box-shadow`), а также
управление прозрачностью и видимостью (`opacity`, `visibility`).

---

## `border` — граница

**Shorthand** для трёх подсвойств: `border-width`, `border-style`, `border-color`.

```css
p {
    border: 1px solid #000;
}
```

Порядок значений не важен. Если `border-style` не указан — граница
не отображается (по умолчанию `none`).

### Стили границы

| Стиль | Описание |
| --- | --- |
| `solid` | Сплошная линия |
| `dotted` | Точки |
| `dashed` | Штрихи |
| `double` | Двойная линия |
| `groove` | «Вдавленная» |
| `ridge` | «Выпуклая» |
| `inset` | Внутренняя тень |
| `outset` | Внешняя тень |
| `none` | Нет границы (по умолчанию) |
| `hidden` | Скрыта (для таблиц) |

```css
p { border: 2px dotted red; }
p { border: 3px dashed #08d1df; }
```

### Границы на отдельных сторонах

```css
p {
    border-top: 1px solid red;
    border-right: 2px dashed blue;
    border-bottom: none;
    border-left: 3px dotted green;
}
```

### border на строчных элементах

На строчных элементах (`<span>`) граница рисуется вокруг каждой строки
отдельно — «по периметру», а не прямоугольником вокруг всего блока.

```html
<span style="border: 1px solid red;">
    Длинный текст, который переносится на несколько строк...
</span>
```

Каждая строка получит свою рамку.

## `border-radius` — радиус скругления

```css
p {
    border-radius: 10px;    /* все углы */
    border-radius: 50%;     /* круг, если width = height */
}
```

### Отдельные углы

```css
p {
    border-radius: 10px 20px 30px 40px;  /* верх-лево, верх-право, низ-право, низ-лево */
}
```

Порядок — по часовой стрелке, начиная с левого верхнего угла.

### Круг

```css
.avatar {
    width: 100px;
    height: 100px;
    border-radius: 50%;    /* круг, потому что width = height */
}
```

Если ширина и высота разные, получится эллипс.

### border-radius + overflow: hidden

Чтобы дочерние элементы обрезались по скруглённым углам родителя,
используют `overflow: hidden`:

```css
.card {
    border-radius: 12px;
    overflow: hidden;   /* обрезает дочерние элементы по скруглению */
}
```

**Оговорка:** в некоторых браузерах (особенно Safari) это сочетание
не всегда работает для элементов с `position: absolute`.

## `outline` — контур

Shorthand для `outline-width`, `outline-style`, `outline-color`.

```css
p {
    outline: 2px solid red;
}
```

### Отличия от border

| | border | outline |
| --- | --- | --- |
| Влияет на размер | Да | Нет |
| Стиль на отдельных сторонах | Да | Нет (только все четыре) |
| Поддерживает border-radius | Да | Нет |
| Расстояние от элемента | Нет | Есть (outline-offset) |

**Ключевое:** outline не занимает места в блочной модели. Он рисуется
поверх и не влияет на положение соседних элементов.

### outline-offset

```css
p {
    outline: 2px solid red;
    outline-offset: 4px;   /* отступ от границы */
}
```

### outline и border-radius

outline всегда прямоугольный, даже если у элемента `border-radius`.
Для скруглённого контура используйте `box-shadow`:

```css
p {
    border-radius: 8px;
    box-shadow: 0 0 0 2px red;  /* имитация скруглённого контура */
}
```

## `box-shadow` — тень блока

```css
p {
    box-shadow: 5px 5px 10px 5px rgba(0, 0, 0, 0.5);
}
```

**Синтаксис:** `X Y [blur] [spread] [color] [inset]`.

| Параметр | Описание |
| --- | --- |
| `X` | Сдвиг по горизонтали (положительный — вправо, отрицательный — влево) |
| `Y` | Сдвиг по вертикали (положительный — вниз, отрицательный — вверх) |
| `blur` | Радиус размытия: чем больше, тем мягче тень |
| `spread` | Радиус распространения: увеличивает (+) или уменьшает (−) тень |
| `color` | Цвет тени (по умолчанию currentColor) |
| `inset` | Внутренняя тень (в начале объявления) |

### Внешняя и внутренняя тень

```css
p {
    box-shadow: 5px 5px 10px 5px black;          /* внешняя */
    box-shadow: inset 5px 5px 10px 5px gray;     /* внутренняя */
}
```

### Несколько теней

Разделяются запятыми. Первая тень — самая верхняя:

```css
p {
    box-shadow: 5px 5px 10px 5px black, inset 5px 5px 10px 5px gray;
}
```

### box-shadow и border-radius

Если у элемента задан `border-radius`, тень автоматически повторяет
форму скругления.

## `opacity` — непрозрачность

```css
p {
    opacity: 0.5;   /* от 0 до 1 */
}
```

| Значение | Описание |
| --- | --- |
| `0` | Полностью прозрачен (невидим) |
| `0.5` | Полупрозрачен |
| `1` | Полностью непрозрачен (по умолчанию) |

**Важно:** `opacity` влияет на весь элемент — включая дочерние элементы
и фон. Если нужно сделать прозрачным только фон — используйте `rgba()`
или `hsla()` для `background-color`.

### opacity: 0 — элемент остаётся интерактивным

При `opacity: 0` элемент невидим, но:

- остаётся в DOM;
- занимает место;
- регистрирует клики и может получать фокус.

**Для доступности:** если элемент скрыт, но должен быть доступен
для скринридеров — используйте `opacity: 0` вместе с `position: absolute`
или `pointer-events: none` (если клики не нужны).

### Контекст наложения

`opacity < 1` создаёт новый контекст наложения (stacking context).
Это влияет на `z-index` дочерних элементов.

## `visibility` — видимость

```css
p {
    visibility: hidden;
}
```

| Значение | Описание |
| --- | --- |
| `visible` | Виден (по умолчанию) |
| `hidden` | Скрыт, но место сохраняется |
| `collapse` | Для ячеек таблиц — скрывает с сохранением структуры |

### visibility vs opacity vs display

| | display: none | visibility: hidden | opacity: 0 |
| --- | --- | --- | --- |
| Виден | Нет | Нет | Нет |
| Занимает место | Нет | Да | Да |
| Интерактивен | Нет | Нет | Да |
| Доступен скринридеру | Нет | Нет | Да |
| Анимируется | Нет | Да | Да |

**Ключевые отличия:**

- `display: none` — элемент полностью удалён из потока.
- `visibility: hidden` — элемент скрыт, но место сохраняется. Взаимодействовать нельзя.
- `opacity: 0` — элемент прозрачен, место сохраняется, взаимодействовать можно.

### Наследование visibility

`visibility` наследуется. Если у родителя `hidden`, дети тоже скрыты.
Но если ребёнку явно задать `visible` — он станет видимым:

```css
.parent { visibility: hidden; }
.child  { visibility: visible; }   /* ребёнок будет виден */
```

Это используют для «скрытия родителя с показом одного элемента».

## Практика

### Задание 1. Границы

Создай три блока с разными стилями border: `solid`, `dashed`, `dotted`.
Добавь разные цвета и толщину.

### Задание 2. Скругление

Создай круг (`width = height`, `border-radius: 50%`) и «капсулу»
(`border-radius: 9999px`).

### Задание 3. Тени

Создай карточку с внешней тенью. Добавь внутреннюю тень через `inset`.
Попробуй несколько теней через запятую.

### Задание 4. Прозрачность

Создай три блока:

- один с `opacity: 0.5`;
- второй с `visibility: hidden`;
- третий с `display: none`.

Сравни, как они отображаются и как влияют на поток документа.

### Задание 5 (дополнительное). practice-block-styling.html

Открой файл и выполни задание: свёрстай «карточку профиля» с аватаром,
именем, описанием и кнопкой. Используй `border-radius`, `box-shadow`,
`outline` и `opacity`.

## Полезные ссылки

- [MDN: `border`](https://developer.mozilla.org/ru/docs/Web/CSS/Reference/Properties/border)
- [MDN: `border-radius`](https://developer.mozilla.org/ru/docs/Web/CSS/Reference/Properties/border-radius)
- [MDN: `outline`](https://developer.mozilla.org/ru/docs/Web/CSS/Reference/Properties/outline)
- [MDN: `box-shadow`](https://developer.mozilla.org/ru/docs/Web/CSS/Reference/Properties/box-shadow)
- [MDN: `opacity`](https://developer.mozilla.org/ru/docs/Web/CSS/Reference/Properties/opacity)
- [MDN: `visibility`](https://developer.mozilla.org/ru/docs/Web/CSS/Reference/Properties/visibility)
- [CSS-Tricks: box-shadow](https://css-tricks.com/almanac/properties/b/box-shadow/)
- [CSS-Tricks: opacity vs visibility vs display](https://css-tricks.com/comparing-various-ways-to-hide-things-in-css/)

## Итоги

- `border` — shorthand для толщины, стиля и цвета. Не отображается без `border-style`.
- `border-radius` — скругление углов. `50%` даёт круг только при равных width и height.
- `outline` — контур снаружи, не влияет на размер, не поддерживает `border-radius`.
- `box-shadow` — тень: X, Y, blur, spread, color, inset. Поддерживает `border-radius`.
- `opacity` — прозрачность всего элемента. 0 — невидим, но интерактивен.
- `visibility: hidden` — скрыт, место сохраняется, взаимодействовать нельзя.
- `display: none` — удалён из потока.
- `visibility` наследуется, но ребёнок может «перебить» через `visible`.
- `opacity < 1` создаёт новый контекст наложения.
