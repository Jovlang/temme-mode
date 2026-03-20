# temme-mode

`temme-mode` is a small Emacs minor mode that implements a focused subset of
Emmet-style abbreviations from scratch.

## Features

- Tag expansion: `div`
- `#id` and `.class` parsing: `section#app.shell`
- Arbitrary attributes: `input[type=text disabled]`
- `id` and `class` merging across shorthand and bracket attributes: `div#app.hero[class='wide tall']`
- Self-closing tags, including void HTML elements and explicit `.../`: `input[type=text]`, `custom-element/`
- Child, sibling, and climb-up operators: `>`, `+`, `^`
- Grouping, including multi-root group children: `(header+main)>p`
- Multipliers: `li*3`
- Text nodes: `p{Hello}`
- Indented output starting at the current line indentation
- Interactive expansion command: `M-x temme-expand` or `C-c ,`

## Examples

Default tag from shorthand-only input:

```text
#root.card
```

Output:

```html
<div id="root" class="card"></div>
```

Repeated children:

```text
ul>li.item*2
```

Output:

```html
<ul>
  <li class="item"></li>
  <li class="item"></li>
</ul>
```

Grouped children:

```text
(header+main)>p
```

Output:

```html
<header>
  <p></p>
</header>
<main>
  <p></p>
</main>
```

Mixed shorthand and bracket attributes:

```text
div#app.hero[class='wide tall'][data-role=card]
```

Output:

```html
<div id="app" class="hero wide tall" data-role="card"></div>
```

Text nodes and siblings:

```text
h1.title{Hello}+p{World}
```

Output:

```html
<h1 class="title">Hello</h1>
<p>World</p>
```

Self-closing elements:

```text
figure>img.hero[src=cover.jpg]/+figcaption{Cover}
```

Output:

```html
<figure>
  <img class="hero" src="cover.jpg" />
  <figcaption>Cover</figcaption>
</figure>
```

Climb-up operator:

```text
div>section>p^aside
```

Output:

```html
<div>
  <section>
    <p></p>
  </section>
  <aside></aside>
</div>
```

Nested layout:

```text
div>(header>h1{Title})+(main>p{Done})
```

Output:

```html
<div>
  <header>
    <h1>Title</h1>
  </header>
  <main>
    <p>Done</p>
  </main>
</div>
```

Repeated groups:

```text
ul>(li>a)*2
```

Output:

```html
<ul>
  <li>
    <a></a>
  </li>
  <li>
    <a></a>
  </li>
</ul>
```

## Running tests

```sh
emacs -Q --batch -l test-temme-mode.el -f ert-run-tests-batch-and-exit
```
