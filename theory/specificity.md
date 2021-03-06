<div align="center">

# Специфичность

[Главная](https://github.com/M0n0mah/css)
|
[Теория](/theory/README.md)
|
[Тесты](/tests/README.md)
|
[Задачи](/tasks/README.md)

</div>

---

**Специфичность (приоритет)** — это набор правил, которые определяют, какой стиль будет применен к элементу.

---

1. При одинаковой специфичности будут применены стили, указанные последними.

```css
p {
  color: red;
}

p {
  color: blue;
}
```

Цвет текста у параграфа будет синим.

---

2. Селекторы, указанные с помощью комбинаторов, будут иметь более высокий приоритет. Чем больше комбинаторов использовано — тем более высокий приоритет будет у селектора.

```css
body p {
  color: blue;
}

p {
  color: red;
}
```

```css
body p {
  color: red;
}

html body p {
  color: blue;
}

p {
  color: green;
}
```

В обоих случаях цвет текста у параграфа будет синим.

---

3. Селектор по классу всегда имеет более высокий приоритет, чем селектор по типу.

```html
<div class="wrapper">
  <p>Example <span class="text">text</span></p>
</div>
```

```css
.text {
  color: blue;
}

div p span {
  color: red;
}
```

Цвет текста будет синим.

Чем больше комбинаторов использовано — тем выше приоритет.

```css
.wrapper .text {
  color: blue;
}

.text {
  color: red;
}
```

---

4. Селектор по идентификатору всегда имеет более высокий приоритет, чем селектор по классу.

```html
<div>
  <p>Example <span class="text" id="text">text</span></p>
</div>
```

```css
#text {
  color: blue;
}

.text {
  color: red;
}
```

Цвет текста будет синим.

---

5. Инлайновые стили имеют самый высокий приоритет.

```html
<div>
  <p>Example <span class="text" id="text" style="color: blue">text</span></p>
</div>
```

```css
#text {
  color: green;
}

.text {
  color: red;
}
```

Цвет текста будет синим.

---

Итого приоритет применения стилей следующий:
1. Инлайновые стили
2. Селекторы по идентификатору
3. Селекторы по классу
4. Селекторы по типу

---

<div align="center">

### `!important`

</div>

---

`!important` — увеличивает приоритет текущего свойства до максимального значения.


```html
<div>
  <p>Example <span class="text" id="text" style="color: gold">text</span></p>
</div>
```

```css
#text {
  color: green;
}

.text {
  color: red;
}

span {
  color: blue !important;
}
```

При этом, если встречаются несколько `!important`, то логика определения какой из них важнее будет точно такая же, как и выше.

```html
<p class="text">Example text</p>
```

```css
.text {
  color: blue !important;
}

p {
  color: red !important;
}
```

Цвет текста будет синим.
