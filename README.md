# Python_Magic_Methods
---

# Method Lookup
## `__getattribute__`

The `__getattribute__` method is called whenever an attribute is accessed on an object. It's a general attribute access method and is used to customize how attributes are retrieved from an object.

```python
class MyClass:
    def __init__(self, value):
        self.value = value
    
    def __getattribute__(self, name):
        print(f"Accessing attribute: {name}")
        return super().__getattribute__(name)

obj = MyClass(42)
print(obj.value)  # Calls __getattribute__ and prints "Accessing attribute: value"
```

## `__getattr__`

The `__getattr__` method is called when an attribute that doesn't exist is accessed using the dot notation. It allows you to define a default behavior when trying to access nonexistent attributes.

```python
class MyClass:
    def __getattr__(self, name):
        return f"Attribute {name} not found"

obj = MyClass()
print(obj.some_attribute)  # Calls __getattr__ and prints "Attribute some_attribute not found"
```

## `__delattr__`

The `__delattr__` method is called when an attribute is deleted using the `del` statement. It lets you define custom behavior when attributes are deleted.

```python
class MyClass:
    def __init__(self):
        self.value = 42
    
    def __delattr__(self, name):
        print(f"Deleting attribute: {name}")
        super().__delattr__(name)

obj = MyClass()
del obj.value  # Calls __delattr__ and prints "Deleting attribute: value"
```

## `__getitem__`

The `__getitem__` method is used to access elements in an object using index notation. It's commonly used in classes that implement container-like behavior.

```python
class MyList:
    def __init__(self, items):
        self.items = items
    
    def __getitem__(self, index):
        return self.items[index]

my_list = MyList([1, 2, 3])
print(my_list[1])  # Calls __getitem__ and prints "2"
```

## `__setitem__`

The `__setitem__` method is used to set elements in an object using index notation. It's used in conjunction with `__getitem__` to provide container-like behavior.

```python
class MyList:
    def __init__(self):
        self.items = []
    
    def __setitem__(self, index, value):
        self.items[index] = value

my_list = MyList()
my_list[0] = 42  # Calls __setitem__ and sets the first item to 42
```



# **Binary Operators:**


## `__add__`

This method is called when the `+` operator is used between two objects.


```python
class MyClass:
    def __init__(self, value):
        self.value = value
    
    def __add__(self, other):
        return MyClass(self.value + other.value)

obj1 = MyClass(5)
obj2 = MyClass(10)
result = obj1 + obj2  # Calls obj1.__add__(obj2)
print(result.value)  # Output: 15
```

## `__and__`

This method is called when the `&` operator is used between two objects.


```python
class BitwiseClass:
    def __init__(self, value):
        self.value = value
    
    def __and__(self, other):
        return BitwiseClass(self.value & other.value)

obj1 = BitwiseClass(0b1010)
obj2 = BitwiseClass(0b1100)
result = obj1 & obj2  # Calls obj1.__and__(obj2)
print(bin(result.value))  # Output: '0b1000'
```

## `__divmod__`

This method is called when the built-in `divmod()` function is used with two objects.


```python
class DivModClass:
    def __init__(self, value):
        self.value = value
    
    def __divmod__(self, other):
        quotient = self.value // other.value
        remainder = self.value % other.value
        return quotient, remainder

obj1 = DivModClass(20)
obj2 = DivModClass(3)
result = divmod(obj1, obj2)  # Calls obj1.__divmod__(obj2)
print(result)  # Output: (6, 2)
```

## `__floordiv__`

This method is called when the `//` operator is used for floor division between two objects.


```python
class FloorDivClass:
    def __init__(self, value):
        self.value = value
    
    def __floordiv__(self, other):
        return FloorDivClass(self.value // other.value)

obj1 = FloorDivClass(15)
obj2 = FloorDivClass(4)
result = obj1 // obj2  # Calls obj1.__floordiv__(obj2)
print(result.value)  # Output: 3
```

## `__lshift__`

This method is called when the `<<` operator is used for left bitwise shifting.


```python
class ShiftClass:
    def __init__(self, value):
        self.value = value
    
    def __lshift__(self, other):
        return ShiftClass(self.value << other.value)

obj1 = ShiftClass(5)
obj2 = ShiftClass(2)
result = obj1 << obj2  # Calls obj1.__lshift__(obj2)
print(result.value)  # Output: 20
```

## `__matmul__`

This method is called when the `@` operator is used for matrix multiplication (Python 3.5+).


```python
class MatrixMultiplyClass:
    def __init__(self, matrix):
        self.matrix = matrix
    
    def __matmul__(self, other):
        result = []
        for row in self.matrix:
            new_row = []
            for col in zip(*other.matrix):
                dot_product = sum(a * b for a, b in zip(row, col))
                new_row.append(dot_product)
            result.append(new_row)
        return MatrixMultiplyClass(result)

matrix1 = MatrixMultiplyClass([[1, 2], [3, 4]])
matrix2 = MatrixMultiplyClass([[2, 0], [1, 2]])
result = matrix1 @ matrix2  # Calls matrix1.__matmul__(matrix2)
print(result.matrix)  
# Output: [[4, 4], [10, 8]]
```

## `__mod__`

This method is called when the `%` operator is used for modulus calculation.


```python
class ModulusClass:
    def __init__(self, value):
        self.value = value
    
    def __mod__(self, other):
        return ModulusClass(self.value % other.value)

obj1 = ModulusClass(17)
obj2 = ModulusClass(5)
result = obj1 % obj2  # Calls obj1.__mod__(obj2)
print(result.value)  # Output: 2
```

## `__mul__`

This method is called when the `*` operator is used for multiplication between two objects.


```python
class MultiplyClass:
    def __init__(self, value):
        self.value = value
    
    def __mul__(self, other):
        return MultiplyClass(self.value * other.value)

obj1 = MultiplyClass(3)
obj2 = MultiplyClass(7)
result = obj1 * obj2  # Calls obj1.__mul__(obj2)
print(result.value)  # Output: 21
```

## `__or__`

This method is called when the `|` operator is used for bitwise OR between two objects.


```python
class BitwiseORClass:
    def __init__(self, value):
        self.value = value
    
    def __or__(self, other):
        return BitwiseORClass(self.value | other.value)

obj1 = BitwiseORClass(0b1010)
obj2 = BitwiseORClass(0b1100)
result = obj1 | obj2  # Calls obj1.__or__(obj2)
print(bin(result.value))  # Output: '0b1110'
```

## `__pow__`

This method is called when the `**` operator is used for exponentiation.


```python
class ExponentiateClass:
    def __init__(self, value):
        self.value = value
    
    def __pow__(self, other):
        return ExponentiateClass(self.value ** other.value)

obj1 = ExponentiateClass(2)
obj2 = ExponentiateClass(3)
result = obj1 ** obj2  # Calls obj1.__pow__(obj2)
print(result.value)  # Output: 8
```

## `__rshift__`

This method is called when the `>>` operator is used for right bitwise shifting.


```python
class ShiftRightClass:
    def __init__(self, value):
        self.value = value
    
    def __rshift__(self, other):
        return ShiftRightClass(self.value >> other.value)

obj1 = ShiftRightClass(16)
obj2 = ShiftRightClass(2)
result = obj1 >> obj2  # Calls obj1.__rshift__(obj2)
print(result.value)  # Output: 4
```

## `__sub__`

This method is called when the `-` operator is used for subtraction between two objects.


```python
class SubtractClass:
    def __init__(self, value):
        self.value = value
    
    def __sub__(self, other):
        return SubtractClass(self.value - other.value)

obj1 = SubtractClass(18)
obj2 = SubtractClass(16)
result = obj1 - obj2  # Calls obj1.__sub__(obj2)
print(result.value) # output: 4
```
## `__truediv__`

This method is called when the `/` operator is used for true division between two objects.


```python
class TrueDivClass:
    def __init__(self, value):
        self.value = value
    
    def __truediv__(self, other):
        return TrueDivClass(self.value / other.value)

obj1 = TrueDivClass(10)
obj2 = TrueDivClass(3)
result = obj1 / obj2  # Calls obj1.__truediv__(obj2)
print(result.value)  # Output: 3.333...
```

## `__xor__`

This method is called when the `^` operator is used for bitwise XOR between two objects.


```python
class BitwiseXORClass:
    def __init__(self, value):
        self.value = value
    
    def __xor__(self, other):
        return BitwiseXORClass(self.value ^ other.value)

obj1 = BitwiseXORClass(0b1010)
obj2 = BitwiseXORClass(0b1100)
result = obj1 ^ obj2  # Calls obj1.__xor__(obj2)
print(bin(result.value))  # Output: '0b0110'
```


# **Right Binary Operators:**

These methods are called when the left operand does not support the operation, and the right operand does. They are used when the order of operands matters.

## `__radd__`
Called when the right operand of the `+` operator doesn't support the addition operation.

```python
class MyNumber:
    def __init__(self, value):
        self.value = value
    
    def __radd__(self, other):
        return MyNumber(self.value + other)

obj = MyNumber(5)
result = 10 + obj  # Calls __radd__
print(result.value)  # Output: 15
```

Similarly, there are right-side counterparts for the other binary operators:
```python
    __radd__
    __rand__
    __rdiv__
    __rdivmod__
    __rfloordiv__
    __rlshift__
    __rmatmul__
    __rmod__
    __rmul__
    __ror__
    __rpow__
    __rrshift__
    __rsub__
    __rtruediv__
    __rxor__
```
# **In-Place Operators:**

In-place operators modify the value of the left operand with the result of the operation. They provide a way to update an object's value in a more concise manner.

## `__iadd__`
Called when the `+=` operator is used.

```python
class Counter:
    def __init__(self, value):
        self.value = value
    
    def __iadd__(self, other):
        self.value += other.value
        return self

counter1 = Counter(5)
counter2 = Counter(3)
counter1 += counter2  # Calls __iadd__
print(counter1.value)  # Output: 8
```

Similarly, there are in-place counterparts for the other binary operators:
```python
    __iadd__
    __iand__
    __ifloordiv__
    __ilshift__
    __imatmul__
    __imod__
    __imul__
    __ior__
    __ipow__
    __irshift__
    __isub__
    __itruediv__
    __ixor__
```


# **Unary Operators**

Unary operators are operations that involve only one operand. Python provides a set of special methods, often referred to as "dunder" methods (short for double underscore), that allow you to define the behavior of unary operators for custom objects. Here are some commonly used unary operator methods:

## `__abs__`

The `__abs__` method is used to define the behavior of the built-in `abs()` function when applied to an object. It should return the absolute value of the object.



```python
class Number:
    def __init__(self, value):
        self.value = value
    
    def __abs__(self):
        return abs(self.value)

num = Number(-5)
abs_value = abs(num)  # This calls num.__abs__()
print(abs_value)  # Output: 5
```

## `__neg__`

The `__neg__` method defines the behavior of the unary minus (`-`) operator when applied to an object. It should return the negation of the object.



```python
class Number:
    def __init__(self, value):
        self.value = value
    
    def __neg__(self):
        return -self.value

num = Number(8)
neg_value = -num  # This calls num.__neg__()
print(neg_value)  # Output: -8
```

## `__pos__`

The `__pos__` method determines the behavior of the unary plus (`+`) operator when used with an object. It should return the object itself, typically without any changes.



```python
class Number:
    def __init__(self, value):
        self.value = value
    
    def __pos__(self):
        return self

num = Number(3)
pos_value = +num  # This calls num.__pos__()
print(pos_value.value)  # Output: 3
```

## `__invert__`

The `__invert__` method is used to define the behavior of the bitwise inversion (`~`) operator when applied to an object. It should return the bitwise inversion of the object.



```python
class BitSequence:
    def __init__(self, value):
        self.value = value
    
    def __invert__(self):
        return ~self.value

bits = BitSequence(0b1010)
inverted_bits = ~bits  # This calls bits.__invert__()
print(bin(inverted_bits))  # Output: '-0b1011'
```


# **Context Manager Methods**

Context managers are objects in Python that are used with the `with` statement to set up and tear down resources or define a specific context of execution. Context managers use the `__enter__` and `__exit__` dunder methods.

## `__enter__` and `__exit__`

The `__enter__` method is called when entering the context defined by the `with` statement. It sets up resources or initializes the context. The `__exit__` method is called when exiting the context and is responsible for cleaning up resources or handling exceptions.

```python
class FileContext:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
        self.file = None
    
    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file
    
    def __exit__(self, exc_type, exc_value, traceback):
        if self.file:
            self.file.close()

# Using the context manager to read a file
with FileContext('example.txt', 'r') as file:
    content = file.read()
    print(content)
# The file is automatically closed after exiting the 'with' block

# Using the context manager to write to a file
with FileContext('output.txt', 'w') as file:
    file.write('Hello, context managers!')
# The file is automatically closed after exiting the 'with' block
```

# **Descriptor**



## `__get__`

The `__get__` method is used to define the behavior of an attribute when it is accessed. It's commonly used to create descriptors that allow you to customize the retrieval of values from an instance. This method takes three parameters: `self` (the descriptor instance), `instance` (the instance of the class that contains the descriptor), and `owner` (the class that owns the descriptor).

```python
class Celsius:
    def __init__(self, value):
        self.value = value

    def __get__(self, instance, owner):
        return self.value

class Temperature:
    celsius = Celsius(25)

temp = Temperature()
print(temp.celsius)  # Output: 25
```

In this example, the `Celsius` class is a descriptor with a `__get__` method. When the `celsius` attribute is accessed on an instance of the `Temperature` class, the `__get__` method is invoked, and it returns the stored value.



## `__set__`

The `__set__` method is used to define the behavior of an attribute when it is assigned a value. It allows you to customize how values are assigned to attributes. This method takes three parameters as well: `self`, `instance`, `value`.

```python
class Celsius:
    def __init__(self):
        self.value = None

    def __get__(self, instance, owner):
        return self.value

    def __set__(self, instance, value):
        if value < -273.15:
            raise ValueError("Temperature below absolute zero is not valid.")
        self.value = value

class Temperature:
    celsius = Celsius()

temp = Temperature()
temp.celsius = 30
print(temp.celsius)  # Output: 30

temp.celsius = -300  # Raises ValueError
```

Here, the `Celsius` descriptor has a `__set__` method that validates the assigned temperature value. It raises a `ValueError` if the assigned value is below absolute zero.



## `__delete__`

The `__delete__` method is used to define the behavior of an attribute when it's deleted using the `del` statement. This method takes two parameters: `self` and `instance`.

```python
class DeletableAttribute:
    def __delete__(self, instance):
        print("Deleting the attribute...")
        del instance._hidden_attr

class MyClass:
    def __init__(self):
        self._hidden_attr = 42

    attr = DeletableAttribute()

obj = MyClass()
print(obj.attr)  # Output: <__main__.DeletableAttribute object at ...>
del obj.attr     # Output: Deleting the attribute...
```

## `__set_name__`

The `__set_name__` method is used to automatically associate the descriptor with its owning class and attribute name. This method is called once during the class creation process and takes three parameters: `self`, `owner` (the class that owns the descriptor), and `name` (the name of the attribute to which the descriptor is assigned).

```python
class NameBinder:
    def __set_name__(self, owner, name):
        self.name = name

    def __get__(self, instance, owner):
        if instance is None:
            return self
        return f"Accessed attribute '{self.name}' from instance"

class MyClass:
    attr = NameBinder()

obj = MyClass()
print(obj.attr)  # Output: Accessed attribute 'attr' from instance
```


# **Creation and Typing Methods**


## `__call__`

The `__call__` method allows an instance of a class to be called as a function. This is useful when you want an object to have behavior similar to a function.



```python
class Multiplier:
    def __init__(self, factor):
        self.factor = factor
        
    def __call__(self, x):
        return self.factor * x

double = Multiplier(2)
result = double(5)  # This calls the __call__ method
print(result)  # Output: 10
```



## `__class__`

The `__class__` method is used to retrieve the class of an instance. It can be accessed as a property.



```python
class MyClass:
    pass

obj = MyClass()
print(obj.__class__)  # Output: <class '__main__.MyClass'>
```



## `__dir__`

The `__dir__` method returns a list of valid attributes for an object. It's used to customize the behavior of the built-in `dir()` function.



```python
class CustomDir:
    def __dir__(self):
        return ['attribute1', 'attribute2']

obj = CustomDir()
print(dir(obj))  # Output: ['attribute1', 'attribute2']
```



## `__init__`

The `__init__` method is a constructor that initializes the attributes of an instance when it is created.



```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
        
person = Person("Alice", 30)
print(person.name)  # Output: Alice
print(person.age)   # Output: 30
```



## `__init_subclass__`

The `__init_subclass__` method is called when a subclass is created. It can be used to perform operations on subclasses during their creation.



```python
class MyBaseClass:
    def __init_subclass__(cls, **kwargs):
        super().__init_subclass__(**kwargs)
        print(f"A subclass of MyBaseClass was created: {cls.__name__}")

class SubClassA(MyBaseClass):
    pass

class SubClassB(MyBaseClass):
    pass

# Output:
# A subclass of MyBaseClass was created: SubClassA
# A subclass of MyBaseClass was created: SubClassB
```



## `__prepare__`

The `__prepare__` method is used in metaclasses to customize the dictionary used for class attribute storage.

Example (Note: Metaclasses are more advanced and less commonly used):

```python
class CustomMeta(type):
    def __prepare__(name, bases):
        return {'custom_attribute': 42}

class MyClass(metaclass=CustomMeta):
    pass

print(MyClass.custom_attribute)  # Output: 42
```



## `__new__`

The `__new__` method is responsible for creating a new instance of a class. It's often overridden in custom classes to customize instance creation.



```python
class Singleton:
    _instance = None
    
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance

a = Singleton()
b = Singleton()

print(a is b)  # Output: True (Both variables reference the same instance)
```



## `__subclasses__`

The `__subclasses__` method returns a list of immediate subclasses of a class. It's a method of the `type` class and can be called on any class.



```python
class MyBaseClass:
    pass

class SubClassA(MyBaseClass):
    pass

class SubClassB(MyBaseClass):
    pass

subclasses = MyBaseClass.__subclasses__()
print(subclasses)  # Output: [<class '__main__.SubClassA'>, <class '__main__.SubClassB'>]
```


# **Async Methods**

The `async` keyword is used to define an asynchronous function in Python. An asynchronous function can contain `await` expressions, allowing it to pause its execution while waiting for asynchronous operations to complete. This is useful for non-blocking I/O operations and concurrent execution.


```python
async def fetch_data(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.text()

async def main():
    data = await fetch_data("https://example.com")
    print(data)

import asyncio
asyncio.run(main())
```

## `__aenter__`

The `__aenter__` method is used in asynchronous context managers. It's called when entering an `async with` block and can be used to set up resources or perform tasks before the context block's code execution starts.


```python
class AsyncContext
    async def __aenter__(self):
        print("Entering async context")
        return self

    async def __aexit__(self, exc_type, exc_value, traceback):
        print("Exiting async context")

async with AsyncContextExample() as context:
    # Inside the async context
    print("Doing something asynchronously")

# Exiting async context
```

## `__aexit__`

The `__aexit__` method is the asynchronous version of the context manager's `__exit__`. It's called when exiting an `async with` block and can be used to clean up resources or perform tasks after the context block's code execution finishes.


```python
class AsyncContext
    async def __aenter__(self):
        print("Entering async context")
        return self

    async def __aexit__(self, exc_type, exc_value, traceback):
        print("Exiting async context")

async with AsyncContextExample() as context:
    print("Doing something asynchronously")

# Exiting async context
```

## `__aiter__`

The `__aiter__` method is used to define an asynchronous iterator. It returns an asynchronous iterator object that implements the `__anext__` method.


```python
class AsyncCounter:
    def __init__(self, limit):
        self.limit = limit
        self.current = 0

    def __aiter__(self):
        return self

    async def __anext__(self):
        if self.current < self.limit:
            self.current += 1
            return self.current
        else:
            raise StopAsyncIteration

async def main():
    async for number in AsyncCounter(5):
        print(number)

import asyncio
asyncio.run(main())
```

## `__anext__`

The `__anext__` method is used in asynchronous iterators to define how the next value is retrieved. It's called for each iteration to obtain the next value asynchronously.

Example is included in the `__aiter__` example above.

## `__await__`

The `__await__` method allows an object to define a custom awaitable behavior. It's used to provide an alternative to the regular await expression for a specific object.


```python
class Awaitable
    def __await__(self):
        yield "Hello"
        yield "Async"
        yield "World"

async def main():
    result = await AwaitableExample()
    print(result)

import asyncio
asyncio.run(main())
```

these examples might require appropriate libraries like `aiohttp` for asynchronous network operations and proper async runtime management with `asyncio`.


# **Instance / Subclass Check**

## `__instancecheck__`
This method is used to customize the behavior of the `isinstance()` function when checking if an object is an instance of a particular class.


```python
class MyInt:
    def __instancecheck__(self, instance):
        return isinstance(instance, int)

obj = 5
print(isinstance(obj, MyInt))  # Output: True
```

## `__subclasscheck__`
Similar to `__instancecheck__`, this method customizes the behavior of the `issubclass()` function when checking if a class is a subclass of another class.


```python
class MyList:
    def __subclasscheck__(self, subclass):
        return issubclass(subclass, list)

class CustomList(list):
    pass

print(issubclass(CustomList, MyList))  # Output: True
```

# **Generic Types**

## `__class_getitem__`
This method allows you to define behavior for when a class is subscripted, typically used for creating generic types.


```python
class GenericList:
    def __class_getitem__(self, item):
        return list

IntList = GenericList[int]
str_list = IntList([1, 2, 3])
print(str_list)  # Output: [1, 2, 3]
```


# **Iterator Methods**

## \_\_iter\_\_ and  \_\_next\_\_

An iterator is an object that implements the methods `__iter__` and `__next__`. It allows you to loop through a sequence of values one at a time.



```python
class MyIterator:
    def __init__(self, data):
        self.data = data
        self.index = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.index < len(self.data):
            value = self.data[self.index]
            self.index += 1
            return value
        else:
            raise StopIteration

my_list = [1, 2, 3, 4, 5]
my_iterator = MyIterator(my_list)

for item in my_iterator:
    print(item)
```

## \_\_iter\_\_

The `__iter__` method returns the iterator object itself. It's called when you use the `iter()` function on an object.



```python
class MyIterable:
    def __init__(self, data):
        self.data = data
    
    def __iter__(self):
        return iter(self.data)

my_list = [1, 2, 3, 4, 5]
my_iterable = MyIterable(my_list)

for item in my_iterable:
    print(item)
```

## \_\_len\_\_

The `__len__` method returns the length of the object when you use the `len()` function on it.


```python
class MyLen:
    def __init__(self, data):
        self.data = data
    
    def __len__(self):
        return len(self.data)

my_list = [1, 2, 3, 4, 5]
my_len = MyLen(my_list)

length = len(my_len)
print(length)
```

## \_\_reversed\_\_

The `__reversed__` method returns a reversed iterator of the object when you use the `reversed()` function on it.



```python
class MyReversed:
    def __init__(self, data):
        self.data = data
    
    def __reversed__(self):
        return reversed(self.data)

my_list = [1, 2, 3, 4, 5]
my_reversed = MyReversed(my_list)

for item in reversed(my_reversed):
    print(item)
```

## \_\_contains\_\_

The `__contains__` method allows you to define custom behavior for the `in` operator when used with your object.



```python
class MyContains:
    def __init__(self, data):
        self.data = data
    
    def __contains__(self, value):
        return value in self.data

my_list = [1, 2, 3, 4, 5]
my_contains = MyContains(my_list)

print(3 in my_contains)
print(6 in my_contains)
```

## `__int__`

The `__int__` method allows you to define how an instance of your class should be converted to an integer.

```python
class IntConverter:
    def __init__(self, value):
        self.value = value
    
    def __int__(self):
        return int(self.value)

converter = IntConverter(10.5)
result = int(converter)
print(result)  # Output: 10
```

## `__bool__`

The `__bool__` method is used to determine the truthiness of an instance when used in a boolean context.

```python
class BoolChecker:
    def __init__(self, value):
        self.value = value
    
    def __bool__(self):
        return self.value > 0

checker_true = BoolChecker(5)
print(bool(checker_true))  # Output: True

checker_false = BoolChecker(0)
print(bool(checker_false))  # Output: False
```


## `__complex__`

The `__complex__` method allows you to define how an instance of your class should be converted to a complex number.

```python
class ComplexConverter:
    def __init__(self, real, imag):
        self.real = real
        self.imag = imag
    
    def __complex__(self):
        return complex(self.real, self.imag)

converter = ComplexConverter(2, 3)
result = complex(converter)
print(result)  # Output: (2+3j)
```

## `__float__`

The `__float__` method allows you to define how an instance of your class should be converted to a floating-point number.

```python
class FloatConverter:
    def __init__(self, value):
        self.value = value
    
    def __float__(self):
        return float(self.value)

converter = FloatConverter(7)
result = float(converter)
print(result)  # Output: 7.0
```

# **Math Methods**

`__index__` :

   This method is called when an object needs to be converted to an integer index, usually for indexing or slicing operations.

   ```python
   class CustomIndex:
       def __init__(self, value):
           self.value = value

       def __index__(self):
           return self.value * 2

   obj = CustomIndex(5)
   index_value = obj.__index__()
   print(index_value)  # Output: 10
   ```

`__trunc__` :

   This method is called to truncate the floating-point number towards zero and return the integer part.

   ```python
   import math

   num = 7.8
   trunc_num = math.trunc(num)
   print(trunc_num)  # Output: 7
   ```

`__floor__` :

   This method is called to round down the floating-point number to the nearest integer that is less than or equal to the original number.

   ```python
   import math

   num = 4.9
   floor_num = math.floor(num)
   print(floor_num)  # Output: 4
   ```

 `__ceil__` :

   This method is called to round up the floating-point number to the nearest integer that is greater than or equal to the original number.

   ```python
   import math

   num = 2.1
   ceil_num = math.ceil(num)
   print(ceil_num)  # Output: 3
   ```

`__round__` :

   This method is called to round the floating-point number to the nearest integer or to a specified number of decimal places.

   ```python
   num = 3.14159
   rounded_num_default = round(num)
   rounded_num_2_places = round(num, 2)

   print(rounded_num_default)  # Output: 3
   print(rounded_num_2_places)  # Output: 3.14
   ```

# **Equality and Hashing:**

`__eq__`  
This method is used to define the behavior of the equality (`==`) operator. It should return `True` if two objects are considered equal, and `False` otherwise.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def __eq__(self, other):
        if isinstance(other, Person):
            return self.name == other.name and self.age == other.age
        return False

person1 = Person("Alice", 25)
person2 = Person("Alice", 25)
person3 = Person("Bob", 30)

print(person1 == person2)  # Calls __eq__, prints True
print(person1 == person3)  # Calls __eq__, prints False
```

`__ge__, __gt__, __le__, __lt__`  
These methods define the behavior of comparison operators (`>=`, `>`, `<=`, `<`).

```python
class Temperature:
    def __init__(self, value):
        self.value = value
    
    def __ge__(self, other):
        return self.value >= other.value
    
    def __gt__(self, other):
        return self.value > other.value
    
    def __le__(self, other):
        return self.value <= other.value
    
    def __lt__(self, other):
        return self.value < other.value

temp1 = Temperature(25)
temp2 = Temperature(30)

print(temp1 >= temp2)  # Calls __ge__, prints False
print(temp1 <= temp2)  # Calls __le__, prints True
```

`__ne__`  
This method defines the behavior of the inequality (`!=`) operator.

```python
class Book:
    def __init__(self, title):
        self.title = title
    
    def __ne__(self, other):
        return self.title != other.title

book1 = Book("Python Basics")
book2 = Book("Python Advanced")

print(book1 != book2)  # Calls __ne__, prints True
```

`__hash__`  
This method returns a hash value for an object. Objects that are equal should have the same hash value. Used in hash-based data structures like dictionaries and sets.

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __hash__(self):
        return hash((self.x, self.y))

point1 = Point(1, 2)
point2 = Point(1, 2)
point3 = Point(3, 4)

print(hash(point1) == hash(point2))  # Calls __hash__, prints True
print(hash(point1) == hash(point3))  # Calls __hash__, prints False
```
# **String Representation**

## `__str__`
This method defines the string representation of an object when using the `str()` function or when an object is displayed as a string.


```python
class Person:
    def __init__(self, name):
        self.name = name
    
    def __str__(self):
        return f"Person: {self.name}"

person = Person("Alice")
print(str(person))  # Output: Person: Alice
```

## `__repr__`
This method defines the "official" string representation of an object, typically used for debugging. It's used when the `repr()` function is called.


```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __repr__(self):
        return f"Point({self.x}, {self.y})"

point = Point(3, 5)
print(repr(point))  # Output: Point(3, 5)
```

# **Other Methods**
## `__format__`

The `__format__` method is used to define the behavior of the `format()` function when applied to an object of your class. This method takes a format specifier as an argument and should return a formatted string representation of the object.

```python
class CustomNumber:
    def __init__(self, value):
        self.value = value
    
    def __format__(self, format_spec):
        if format_spec == "hex":
            return hex(self.value)
        elif format_spec == "bin":
            return bin(self.value)
        else:
            return str(self.value)

num = CustomNumber(42)
print("Formatted as hex: {:hex}".format(num))  # Output: Formatted as hex: 0x2a
print("Formatted as binary: {:bin}".format(num))  # Output: Formatted as binary: 0b101010
print("Formatted as decimal: {}".format(num))  # Output: Formatted as decimal: 42
```


## `__bytes__`

The `__bytes__` method is used to define the behavior of an object when it's converted to bytes using the built-in `bytes()` function.



```python
class CustomBytes
    def __init__(self, value):
        self.value = value
    
    def __bytes__(self):
        return bytes(str(self.value), encoding='utf-8')

obj = CustomBytesExample(42)
bytes_representation = bytes(obj)
print(bytes_representation)  # This will output b'42'
```



## `__fspath__`

The `__fspath__` method defines the behavior of an object when it's converted to a file path using the `pathlib.Path()` constructor.



```python
from pathlib import Path

class CustomPath
    def __init__(self, path):
        self.path = path
    
    def __fspath__(self):
        return str(self.path)

obj = CustomPathExample(Path("/my/custom/path.txt"))
path = Path(obj)
print(path)  # This will output: /my/custom/path.txt
```



## `__getnewargs__`

The `__getnewargs__` method is used to customize the arguments used to recreate an object during pickling and unpickling.



```python
class CustomNewArgs
    def __init__(self, value):
        self.value = value
    
    def __getnewargs__(self):
        return (self.value,)

obj = CustomNewArgsExample(123)
new_obj = obj.__class__(*obj.__getnewargs__())
print(new_obj.value)  # This will output: 123
```



## `__reduce__`

The `__reduce__` method defines how an object should be serialized and deserialized using the `pickle` module.



```python
import pickle

class CustomReduce
    def __init__(self, value):
        self.value = value
    
    def __reduce__(self):
        return (self.__class__, (self.value,))
    
    def __setstate__(self, state):
        self.value = state

obj = CustomReduceExample(987)
pickled = pickle.dumps(obj)
unpickled = pickle.loads(pickled)
print(unpickled.value)  # This will output: 987
```



## `__reduce_ex__`

Similar to `__reduce__`, the `__reduce_ex__` method defines how an object should be serialized and deserialized using the `pickle` module, with an additional protocol argument.



```python
import pickle

class CustomReduceEx
    def __init__(self, value):
        self.value = value
    
    def __reduce_ex__(self, protocol):
        return (self.__class__, (self.value,), None, None, None)
    
    def __setstate__(self, state):
        self.value = state

obj = CustomReduceExExample(555)
pickled = pickle.dumps(obj, protocol=2)
unpickled = pickle.loads(pickled)
print(unpickled.value)  # This will output: 555
```



## `__sizeof__`

The `__sizeof__` method returns the size of an object in memory, in bytes.



```python
class CustomSize
    def __init__(self, data):
        self.data = data
    
    def __sizeof__(self):
        return len(self.data)

obj = CustomSizeExample([1, 2, 3, 4, 5])
size = obj.__sizeof__()
print(size)  # This will output the size of the list in bytes
```



## `__length_hint__`

The `__length_hint__` method provides an estimated length of an object, useful for optimizing memory allocation in certain scenarios.



```python
class CustomLengthHint
    def __init__(self, data):
        self.data = data
    
    def __length_hint__(self):
        return len(self.data)

obj = CustomLengthHintExample([1, 2, 3, 4, 5])
hint = len(obj)
print(hint)  # This will output the length of the list
```
