# WIP

# pipe
UFCS for Python.  

An implementaion of [UFCS(Uniform function call syntax)](https://en.wikipedia.org/wiki/Uniform_Function_Call_Syntax) for Python. This package allows any function to be called using the syntax for member accessing. An object wrapped the `funcall.obj` function becomes to accept any function as its own member. The object is converted to a `funcall.ChainableObject`, but it behaves as expected.

```python
from pipe import chainable

x = chainable(5).range.sum
# This is equivalent to;
# x = sum(range(5))

y = x + 5
# x is a ChainableObject, but behaves as int.
```

## Installation

`pipe` has no dipendencies.

```bash
sudo pip install pipe
```

## Usage

### ChainableObject.map, filter, reduce

Implementations as methods of builtiin-functions. Arguments passed to them should be callable objects.  

```python
from pipe import chainable

chainable('pen pineapple apple pen').split.map(str.capitalize)
# This is equivalent to;
map(str.capitalize, 'pen pinapple apple pen'.split())
```

### ChainableObject.call

A method which calls function passed as an argument. This is useful when using anonymous functions or functions bound to different namespaces.

```python
from pipe import chainable

chainable('pen pineapple apple pen').split.call('-'.join)
# This is equivalent to;
'-'.join('pen pineapple apple pen'.split())

import numpy as np

chainable(5).call(np.arange)
# This is equivalent to;
np.arange(5)
# obj(5).np.arange does'nt work...
```

### Using >> as pipe operator

It is possible to use operator >> as pipe operator to create good looking pipelines like in R or Ruby.

```python
import numpy as np
from pipe import chainable, unpack

chainable(10) >> np.range >> (lambda x: map(float, x)) >> sum >> print

# or 

chainable(10) >> \
    np.range >> \
    (lambda x: map(float, x)) >> \
    sum >> \
    print
```

## TODO

- [ ] Installable package from github
- [ ] Find how to use partial function in pipelines
- [ ] Context manager for pipelines - for more convinient usage
- [ ] Something to make lambdas better, like in Julia or in siuba

## Other similar projects (where I'm going to sneak a couple of ideas and codes)

- https://github.com/kieferk/dfply - Good looking thing, not exactly what I want, but still worthy to look deeper.
- https://github.com/machow/siuba - I think the best working pipe operator with lambda built-in. Very worthy to steal from there some ideas)
- https://github.com/evhub/coconut/ - Very cool fucntional dsl in python with very good working pipes like in Julia.

