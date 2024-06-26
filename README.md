# Cal-cool-ator 🔢

[![PyPI Version][pypi-badge]][pypi-link]  

This package contains a `Calculator` class written in 🐍Python capable of
performing simple tasks. Let's get to know it! 🏃🏻‍♂️💨  

**Table of contents:**

1. [Installation](#0️⃣-first-things-first)
2. [Setup](#1️⃣-import-and-setup)
3. [Class overview](#2️⃣-what-are-the-differences)
4. [Features](#3️⃣-methods-and-modifiers)
5. [Conclusions](#4️⃣-afterword)

---

## 0️⃣ First things first

In order for you to use the package, you will have to download it from PyPI,
using `pip` the Python package manager:

```sh
> pip install calcoolator
```

This shouldn't take long as it's a very basic, lightweight package and doesn't
require any dependencies. ***It just works out of the box!*** 🪄
Once the setup has finished, I reccomend you checking that it has been
correctly installed by running `pip list` (although this may result in a quite
lengthy output)
> 💡 A good idea would be *piping* it to `grep` or `FINDSTR` if you are on Windows:

```sh
# macOS / Linux / UNIX
$ pip list | grep calcoolator

# Windows
> pip list | FINDSTR calcoolator
```

The result should look somewhat like this:

```sh
calcoolator        x.x.x
```

Got it? Neat! Now we can move on. ✅

---

## 1️⃣ Import and setup

This package contains two main modules: `base_class` and `handler_class`, the
first having the parent `Calculator` and the second consisting of the child
`HandlerCalculator`. We will describe both in the next section. Right now,
let's focus on imports.  

☝🏻 Once you have the package, you can import it's classes by writing the following
lines at the beginning of your module:

```py
from calcoolator.base_class import Calculator
from calcoolator.handler_class import HandlerCalculator
```

and instantiating the class like this ⬇️

```py
calculator = Calculator()
handler_calculator = HandlerCalculator()
```

🤖 Okay, let's use our brand new calculator!

---

## 2️⃣ What are the differences?

Right, so both of the classes are basically the same, with the core difference
that `Calculator` will stop if it encounters an error while `HandlerCalculator`
will display a message in the console and keep going with whatever value had in
memory before it encountered the exception. *I couldn't decide which version to
implement* 🤷🏻 and I made both so you can choose the one that suits your needs!
If that sounds a bit confusing, let me give you an example:  

🧠 Suppose you want to chain some operations, and in the middle of your code, some
unsupported type slips into the arguments of the method you're using:

```py
base = Calculator()
base.add(5, 6)              # 11 -> (5 + 6)
base.subtract(9, 3)         # -1 -> (11 - 9 - 3)
base.divide(4, "oops!")     # ValueError -> The script stops
base.multiply(7)            # Not executed
```

```py
handler = HandlerCalculator()
handler.add(5, 6)           # 11 -> (5 + 6)
handler.subtract(9, 3)      # -1 -> (11 - 9 - 3)
handler.divide(4, "oops!")  # Displays the error and continues
handler.multiply(7)         # -7 -> (-1 * 7)
```

🌟 See the difference now? 🌟  
Well, that's it! Otherwise, both calculators work in exactly the same way

---

## 3️⃣ Methods and modifiers

The calculators come with the following methods and modifiers, which alter
the default behaviour of the method. The admitted arguments type are numbers,
either int or float or valid strings (e.g. `"42"`)  

| [Methods](#methods-default-behaviour) | [Keyword modifiers](#keyword-modifiers) |
| ----- | :-----: |
| [`add()`](#addargs-onlyfalse) | [`only`](#only) |
| [`subtract()`](#subtractargs-onlyfalse-reversefalse) | [`only`](#only) + [`reverse`](#reverse) |
| [`multiply()`](#multiplyargs-number-onlyfalse-factorfalse) | [`only`](#only) + [`factor`](#factor)|
| [`divide()`](#divideargs-onlyfalse-reversefalse) | [`only`](#only) + [`reverse`](#reverse)|
| [`nth_root()`](#nth_rootn1-value0) | None |
| [`power()`](#powerp1-value0) | None |
| [`reset()`](#resetvalue0) | None |
| [`get_memory()`](#get_memory) | None |
| [`screen()`](#screenmessage) | None |

---

### Methods default behaviour

#### `add(*args, only=False)`

Takes an arbitrary number of values and adds them including the memory:

```py
# calculator.memory = 10
calculator.add(5, 10)           # 25 -> (10 + 5 + 10)
```

#### `subtract(*args, only=False, reverse=False)`

Takes an arbitrary number of values and subtracts them in sequential order
taking the memory as first argument and continuing with the passed ones from
left to right:

```py
# calculator.memory = 10
calculator.subtract(5, 10)      # -5 -> (10 - 5 - 10)
```

#### `multiply(*args: Number, only=False, factor=False)`

Takes an arbitrary number of values and multiplies them together:

```py
# calculator.memory = 10
calculator.multiply(5, 10)      # 500 -> (10 * 5 * 10)
```

#### `divide(*args, only=False, reverse=False)`

Takes an arbitrary number of values and divides them in sequential order
taking the memory as first argument and continuing with the passed ones from
left to right:

```py
# calculator.memory = 10
calculator.divide(5, 10)        # 25 -> (10 + 5 + 10)
```

#### `nth_root(n=1, value=0)`

Calculates the (n)th root of the current memory if no second parameter is
present otherwise the (n)th root of the value specified as second argument:

```py
# calculator.memory = 8
calculator.nth_root(3)          # 2 -> (³√8)
calculator.nth_root(5, 243)     # 3 -> (⁵√243)
```

⚠️ **Please note:** I have incorporated a `NegativeRootError` exception in order to
disallow complex numbers to be thrown into the mix.

```py
# calculator.memory = -45
calculator.nth_root(3)          # NegativeRootError -> (³√-45 is not allowed)
```

#### `power(p=1, value=0)`

Elevates the current memory to the p power, if a second parameter is specified,
then the base it's the value passed:

```py
# calculator.memory = 10
calculator.nth_root(3)          # 1000 -> (10³)
calculator.nth_root(6, 4)       # 4096 -> (4⁶)
```

#### `reset(value=0)`

Resets the calculator memory to 0 or the value you pass:

```py
# calculator.memory = 10
calculator.reset()              # 0
calculator.reset(123)           # 123
```

#### `get_memory()`

Returns the current memory value:

```py
# calculator.memory = 10
calculator.get_memory()         # 10
```

#### `screen(message="")`

Prints on stdout a pretty version of the calculator's memory

```py
# calculator.memory = 10
calculator.screen()
*------------------------------*
|                         10.0 |
*------------------------------*
calculator.screen("hello")
*------------------------------*
|            hello             |
*------------------------------*
```

---

### Keyword modifiers

You can mix them in the method that accepts them!

#### `only`

Available for `add`, `subtract`, `multiply` and `divide`  
Performs the operation **only** with the arguments, it ignores the memory value:

```py
# calculator.memory = 10
calculator.add(2, 5, only=True)         # 7 -> (2 + 5)
calculator.divide(8, 4, only=True)      # 2 -> (8 / 4)
```

#### `reverse`

Available for `subtract` and `divide`
Performs the operation **from right to left**:

```py
# calculator.memory = 10
calculator.subtract(2, 5, reverse=True)     # -7 -> (5 - 2 - 10)
calculator.reset(5)
calculator.divide(2, 10, reverse=True)      # 1 -> (10 / 2 / 5)
```

#### `factor`

Available just for `multiply`
Multiplies the memory value by each argument and then multiplies the results
together. Using `factor` will override `only`

```py
# calculator.memory = 5
calculator.multiply(2, 10)              # 500 -> (5*2) * (5*10)
```

*Phew!* That was quite a mouthful...

---

## 4️⃣ Afterword

**💪🏻 Now you know all the secrets of this Python package!**  
I hope you found this document informative / entertaining and helped you get the
maximum out of the classes the package contains.  
Anyway, if you ever forget something, you can always check the `help()`
function or read the `__doc__` of the precise method you need, you'll find
all this info there.  

### Thank you for your time and see you soon! 👋🏻

[![Github Badge][made]][git-hub]

<!-- Badges & links -->
[made]: https://img.shields.io/badge/made_with_%E2%9D%A4%EF%B8%8F-Berto_Polo-1A9CFF?logo=github&logoColor=FFFFFF
[git-hub]: https://github.com/berto-polo
[pypi-badge]: https://img.shields.io/pypi/v/calcoolator?logo=pypi&logoColor=FFFFFF&label=PyPI&color=303C75A
[pypi-link]: https://pypi.org/project/calcoolator/
