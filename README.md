# temme-mode

`temme-mode` is a small Emacs minor mode that implements a basic subset of
Emmet-style abbreviations from scratch.

## Features

- Tag expansion: `div`
- `#id` and `.class` parsing: `section#app.shell`
- Child and sibling operators: `>`, `+`
- Multipliers: `li*3`
- Text nodes: `p{Hello}`
- Interactive expansion command: `M-x temme-expand` or `C-c ,`

## Example

Input:

```text
ul>li.todo*2+p{done}
```

Output:

```html
<ul><li class="todo"></li><li class="todo"></li><p>done</p></ul>
```

## Running tests

```sh
emacs -Q --batch -l test-temme-mode.el -f ert-run-tests-batch-and-exit
```
