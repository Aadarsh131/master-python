> This module provides runtime support for type hints

## useful built-in types
```py
# For most types, just use the name of the type in the annotation
# Note that mypy can usually infer the type of a variable from its value,
# so technically these annotations are redundant
x: int = 1
x: float = 1.0
x: bool = True
x: str = "test"
x: bytes = b"test"

# For collections on Python 3.9+, the type of the collection item is in brackets
x: list[int] = [1]
x: set[int] = {6, 7}

# For mappings, we need the types of both keys and values
x: dict[str, float] = {"field": 2.0}  # Python 3.9+

# For tuples of fixed size, we specify the types of all the elements
x: tuple[int, str, float] = (3, "yes", 7.5)  # Python 3.9+

# For tuples of variable size, we use one type and ellipsis
x: tuple[int, ...] = (1, 2, 3)  # Python 3.9+

# On Python 3.10+, use the | operator when something could be one of a few types
x: list[int | str] = [3, 5, "test", "fun"]  # Python 3.10+
```

## Older versions
```py
# On Python 3.8 and earlier, the name of the collection type is
# capitalized, and the type is imported from the 'typing' module
from typing import List, Set, Dict, Tuple, Union
x: List[int] = [1]
x: Set[int] = {6, 7}
x: Dict[str, float] = {"field": 2.0}
x: Tuple[int, str, float] = (3, "yes", 7.5)
x: Tuple[int, ...] = (1, 2, 3)

# On earlier versions, use Union
x: list[Union[int, str]] = [3, 5, "test", "fun"]

```
## Type aliases
```py
type Vector = list[float]

def scale(scalar: float, vector: Vector) -> Vector:
    return [scalar * num for num in vector]

# passes type checking; a list of floats qualifies as a Vector.
new_vector = scale(2.0, [1.0, -4.2, 5.4])

#OR
from typing import TypeAlias

Vector: TypeAlias = list[float]
```

## New Types
```py
from typing import NewType

UserId = NewType('UserId', int)
# 'output' is of type 'int', not 'UserId'
output = UserId(23413) + UserId(54341)

# it is also possible to create a NewType based on a ‘derived’ NewType:
EmpId = NewType('EmpId', int)
ProEmpId = NewType('ProEmpId', EmpId)
```

# RESOURCES-
- [mypy docs](https://mypy.readthedocs.io/en/stable/cheat_sheet_py3.html)
- [python docs](https://docs.python.org/3/library/typing.html)