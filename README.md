# PyErr
Package providing functional error handling.

## Description
Package providing functional error handling in 'monadic'-like way. Allows you to create wrapped value from success value or an error, apply functions to wrapped value and unwrap.

## Install

```
pip install pyerr
```

[Pypi link](https://pypi.org/project/pyerr/ "Pypi link")

## Usage

### Creating wrapped value

``` python
import pyerr

def plus_one(number_positive):
    if number_positive < 0:
        return pyerr.error("Number has to be positive.")
    else:
        return pyerr.ok(number_positive + 1)
```


### Checking and unwrapping

``` python
...
result = plus_one(1)
if is_ok(result):
    print(f"Yay! we got result {unwrap(result)}")
else:
    print(f"Nay:( we got an error {unwrap(result)}")
```

### Other examples

#### Handling function which could raise Exception with decorator

``` python

@pyerr.try_err
def plus_one(number_positive):
    if val_int < 0:
        raise Exception("Number has to be positive.")
    else:
        return pyerr.ok(number_positive + 1)

result_ok = target(1)
result_err = target(-1)
```

#### Applying functions to wrapped value

``` python
# Applying general function
wrapped_result = pyerr.fmap(lambda x: x + 1, pyerr.ok(1))

# Applying function that returs wrapped value from pyerr
flat_wrapped_result = pyerr.flat_map(lambda x: pyerr.ok(x+1), pyerr.ok(1))
```

