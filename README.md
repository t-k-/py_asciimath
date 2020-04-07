## py_asciimath [![Build Status](https://travis-ci.com/belerico/py_asciimath.svg?branch=master)](https://travis-ci.com/belerico/py_asciimath)

AsciiMath is an easy-to-write markup language for mathematics: for more information check out the main website at http://asciimath.org/.  
The parser utility takes an ASCIIMath string in input and returns the corresponding LaTeX translation, via a syntactic and semantic transformation.

## Install

To install the package run `pip install py-asciimath` or `pip3 install py-asciimath`

## Usage

### As python module
```python
from py_asciimath.parser.parser import ASCIIMath2Tex
from py_asciimath.transformer.const import asciimath_grammar

if __name__ == "__main__":
    parser = ASCIIMath2Tex(asciimath_grammar, inplace=False,)
    asciimath = "sum_(i=1)^n i^3=((n(n+1))/2)^2"
    latex = parser.asciimath2tex(asciimath, pprint=True)
    print(latex)
```
results in:
`\sum_{i = 1}^{n} i^{3} = \left(\frac{\left(n \left(n + 1\right)\right)}{2}\right)^{2}`

### From the command line
```
py_asciimath: a simple ASCIIMath converter.

Usage:
  py_asciimath.py ASCIIMATH ... (-o OLANG | --output=OLANG) [--log]
  py_asciimath.py (-h | --help)
  py_asciimath.py --version

Options:
  -h --help                     Show this screen.
  -o OLANG --output=OLANG       Output language.
  --log                         Log the transformation process.
  --version                     Show version.
```

For example, `py_asciimath "sum_(i=1)^n i^3=((n(n+1))/2)^2" -o latex` prints:

```
Translating ...
\sum_{i = 1}^{n} i^{3} = \left(\frac{n \left(n + 1\right)}{2}\right)^{2}
```
If the option `--log` is present, then it prints also every transformation of the input, so `py_asciimath "sum_(i=1)^n i^3=((n(n+1))/2)^2" -o latex --log` prints:

```
Translating ...
INFO:Calling symbol with args:
INFO:	items = [Token(SUM, 'sum')]
INFO:Calling const with args:
INFO:	items = [Token(LETTER, 'i')]
INFO:Calling exp_interm with args:
INFO:	items = ['i']
INFO:Calling symbol with args:
INFO:	items = [Token(EQUAL, '=')]
INFO:Calling exp_interm with args:
INFO:	items = ['=']
INFO:Calling const with args:
INFO:	items = [Token(NUMBER, '1')]
INFO:Calling exp_interm with args:
INFO:	items = ['1']
INFO:Calling exp with args:
INFO:	items = ['1']
INFO:Calling exp with args:
INFO:	items = ['=', '1']
INFO:Calling exp with args:
INFO:	items = ['i', '= 1']
INFO:Calling exp_par with args:
INFO:	items = [Token(LPAR, '('), 'i = 1', Token(RPAR, ')')]
INFO:Calling const with args:
INFO:	items = [Token(LETTER, 'n')]
INFO:Calling exp_under_super with args:
INFO:	items = ['\\sum', '\\left(i = 1\\right)', 'n']
INFO:Calling remove_parenthesis with args:
INFO:	s = '\\left(i = 1\\right)'
INFO:Calling remove_parenthesis with args:
INFO:	s = 'n'
INFO:Calling const with args:
INFO:	items = [Token(LETTER, 'i')]
INFO:Calling const with args:
INFO:	items = [Token(NUMBER, '3')]
INFO:Calling exp_super with args:
INFO:	items = ['i', '3']
INFO:Calling remove_parenthesis with args:
INFO:	s = '3'
INFO:Calling symbol with args:
INFO:	items = [Token(EQUAL, '=')]
INFO:Calling exp_interm with args:
INFO:	items = ['=']
INFO:Calling const with args:
INFO:	items = [Token(LETTER, 'n')]
INFO:Calling exp_interm with args:
INFO:	items = ['n']
INFO:Calling const with args:
INFO:	items = [Token(LETTER, 'n')]
INFO:Calling exp_interm with args:
INFO:	items = ['n']
INFO:Calling symbol with args:
INFO:	items = [Token(PLUS, '+')]
INFO:Calling exp_interm with args:
INFO:	items = ['+']
INFO:Calling const with args:
INFO:	items = [Token(NUMBER, '1')]
INFO:Calling exp_interm with args:
INFO:	items = ['1']
INFO:Calling exp with args:
INFO:	items = ['1']
INFO:Calling exp with args:
INFO:	items = ['+', '1']
INFO:Calling exp with args:
INFO:	items = ['n', '+ 1']
INFO:Calling exp_par with args:
INFO:	items = [Token(LPAR, '('), 'n + 1', Token(RPAR, ')')]
INFO:Calling exp_interm with args:
INFO:	items = ['\\left(n + 1\\right)']
INFO:Calling exp with args:
INFO:	items = ['\\left(n + 1\\right)']
INFO:Calling exp with args:
INFO:	items = ['n', '\\left(n + 1\\right)']
INFO:Calling exp_par with args:
INFO:	items = [Token(LPAR, '('), 'n \\left(n + 1\\right)', Token(RPAR, ')')]
INFO:Calling const with args:
INFO:	items = [Token(NUMBER, '2')]
INFO:Calling exp_frac with args:
INFO:	items = ['\\left(n \\left(n + 1\\right)\\right)', '2']
INFO:Calling remove_parenthesis with args:
INFO:	s = '\\left(n \\left(n + 1\\right)\\right)'
INFO:Calling remove_parenthesis with args:
INFO:	s = '2'
INFO:Calling exp with args:
INFO:	items = ['\\frac{n \\left(n + 1\\right)}{2}']
INFO:Calling exp_par with args:
INFO:	items = [Token(LPAR, '('), '\\frac{n \\left(n + 1\\right)}{2}', Token(RPAR, ')')]
INFO:Calling const with args:
INFO:	items = [Token(NUMBER, '2')]
INFO:Calling exp_super with args:
INFO:	items = ['\\left(\\frac{n \\left(n + 1\\right)}{2}\\right)', '2']
INFO:Calling remove_parenthesis with args:
INFO:	s = '2'
INFO:Calling exp with args:
INFO:	items = ['\\left(\\frac{n \\left(n + 1\\right)}{2}\\right)^{2}']
INFO:Calling exp with args:
INFO:	items = ['=', '\\left(\\frac{n \\left(n + 1\\right)}{2}\\right)^{2}']
INFO:Calling exp with args:
INFO:	items = ['i^{3}', '= \\left(\\frac{n \\left(n + 1\\right)}{2}\\right)^{2}']
INFO:Calling exp with args:
INFO:	items = ['\\sum_{i = 1}^{n}', 'i^{3} = \\left(\\frac{n \\left(n + 1\\right)}{2}\\right)^{2}']
\sum_{i = 1}^{n} i^{3} = \left(\frac{n \left(n + 1\right)}{2}\right)^{2}
```

## Grammar

The grammar used to parse the input is:
```
start: i start* -> exp
i: s -> exp_interm
    | s "/" s -> exp_frac
    | s "_" s -> exp_under
    | s "^" s -> exp_super
    | s "_" s "^" s -> exp_under_super
s: l start? r -> exp_par
    | u s -> exp_unary
    | b s s -> exp_binary
    | latex -> symbol
    | c -> const
    | QS -> q_str
c: /d[A-Za-z]/ // derivatives
  | NUMBER
  | LETTER
l: {} // left parenthesis
r: {} // right parenthesis
b: {} // binary functions
u: {} // unary functions
latex: {}
QS: "\"" /(?<=").+(?=")/ "\"" // Quoted String
```
For the complete list of symbols, please refer to http://asciimath.org/#syntax. The only symbol that I've added is `dstyle`, that stands for `displaystyle` as a unary function.

## Rendering (semantics)

A parsed ASCIIMath string is rendered as follows:

* `latex`, `u` and `c` symbols are converted to their LaTeX equivalent
* `text` and `ul` correspond to the `\textrm` and `\underline` functions
* `bb`, `bbb`, `cc`, `tt`, `fr` and `sf` correspond to the `\boldsymbol`, `\mathbb`, `\mathcal`, `\texttt`, `\mathfrak` and `\textsf` functions
* `frac` is rendered as a fraction, `root n x` as the n-th root of x and `stackrel x y` displays x upon y
* Any text placed between a pair of `"` is rendered in the same font as normal text.
* `/` stands for a fraction. The `_` and `^` tokens have the same behaviour as in LaTeX but the subscript must be placed before the superscript if they are both present

### Delimiters

Left and right delimiters are preceded by the `\left` and `\right` commands to be well-sized. `(:` and `:)` are chevrons (angle parenthesis). `{:` and `:}` are invisible delimiters like LaTeX's {. `|:` is converted to `\lvert` , while `||:` is converted to `\lVert`. The other delimiters are rendered as expected.  
Useless delimiters are automatically removed in expressions like: 

* `(...)/(...)`
* `(...)_(...)`, `(...)^(...)` and the combination of sub and superscript
* `u (...)`, `b (...) (...)` where u and b are unary and binary operators
  
If you want them to be rendered, you have to double them, for example: `((x+y))/2` or `{: (x+y) :}/2`.

### Matrices and systems of equations

For a text to be rendered as a matrix must have a structure like 

<div align="center">
    <code>L '[' ... (, ...)* ']', '[' ... (, ...)* ']' (, '[' ... (, ...)* ']' )* R</code> 
    <br>
    or
    <br>
    <code>L '(' ... (, ...)* ')', '(' ... (, ...)* ')' (, '(' ... (, ...)* ')' )* R</code>
</div>

that is:

* It must be delimited by a left (`L`) and right (`R`) parenthesis
* Every row can be separated by `[]` XOR `()` (if one starts with `[]`, every row will be recognized with the same parenthesis, same for `()`), followed by `,` and possibly another row
* Every matrix must contain at least two rows
* Every rows contains zero or more columns, where `...` can be any ASCIIMath expression
* Every row must contain the same number of columns

Since `L` and `R` can be any left or right parenthesis, and every matrices must have the same number of columns, to render a system of equation one can write something like `{[(root n x)/(x) <= 4], [x^2=e^x]:}`.  
On the other hand a matrix can be somenthing like `[[(root n x)/(x) <= 4, int x dx], [x^2=e^x, lim_(x to infty) 1 / (x^2)]]`.
