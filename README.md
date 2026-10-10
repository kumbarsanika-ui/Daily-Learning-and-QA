# Daily Learning and Q&A

## 1. What is asynchronous programming in JavaScript/Node.js?

Asynchronous programming lets a program start work that may take time, such as a network request or file read, and continue with other work while waiting. When the operation completes, the program handles its result using callbacks, Promises, or `async`/`await`. Node.js uses an event loop to coordinate asynchronous operations without blocking the main thread.

```js
async function loadData() {
  const response = await fetch("/api/data");
  return response.json();
}
```

## 2. What is the Virtual DOM in React?

The Virtual DOM is a lightweight, in-memory representation of the user interface. When a component's state or props change, React compares the updated representation with the previous one and applies the necessary changes to the browser's DOM.

## 3. What is exception handling in Python?

Exception handling lets a program respond to errors that occur while it runs. A `try` block contains code that might fail, `except` handles an error, and `finally` runs whether or not an error occurred.

```python
try:
	number = int(input("Enter a number: "))
except ValueError:
	print("Please enter a valid integer.")
finally:
	print("Finished.")
```

## 4. What is a REST API, and how does it work?

A REST API allows software systems to communicate over HTTP by working with resources, such as users or orders. A client sends a request to an endpoint, and the server processes it and returns a response, often in JSON. Common HTTP methods are `GET` (read), `POST` (create), `PUT` or `PATCH` (update), and `DELETE` (remove). REST APIs are generally stateless: each request carries the information needed to process it.

## 5. What is cloud computing? Explain IaaS, PaaS, and SaaS.

Cloud computing provides computing resources over the internet, so organizations can use servers, platforms, or software without managing all the underlying infrastructure themselves.

- **IaaS (Infrastructure as a Service):** Provides virtual machines, storage, and networking. The customer manages the operating system and applications. Example: Amazon EC2.
- **PaaS (Platform as a Service):** Provides a managed platform for building and deploying applications, so developers can focus on application code. Example: Google App Engine.
- **SaaS (Software as a Service):** Provides a complete application over the internet. The provider manages the application and infrastructure. Example: Microsoft 365.

## 6. Day-2 Python Interview Programming Questions

### 1. Reverse a string

Build the reversed string by reading the input from the end to the beginning.

```python
def reverse_string(text):
	reversed_text = ""
	for index in range(len(text) - 1, -1, -1):
		reversed_text += text[index]
	return reversed_text


print(reverse_string("Python"))  # nohtyP
```

### 2. Check whether a number is a palindrome

A negative number is not considered a palindrome. Reverse the digits arithmetically and compare the result with the original number.

```python
def is_palindrome_number(number):
	if number < 0:
		return False

	original = number
	reversed_number = 0
	while number > 0:
		digit = number % 10
		reversed_number = reversed_number * 10 + digit
		number //= 10

	return original == reversed_number


print(is_palindrome_number(12321))  # True
```

### 3. Find the largest number in a list

The list must contain at least one number. Start with its first element, then keep the largest value seen so far.

```python
def find_largest(numbers):
	if not numbers:
		raise ValueError("numbers must not be empty")

	largest = numbers[0]
	for number in numbers[1:]:
		if number > largest:
			largest = number
	return largest


print(find_largest([4, 9, 2, 7]))  # 9
```

### 4. Count vowels in a string

Convert each character to lowercase so both uppercase and lowercase vowels are counted.

```python
def count_vowels(text):
	vowels = "aeiou"
	count = 0
	for character in text.lower():
		if character in vowels:
			count += 1
	return count


print(count_vowels("Interview"))  # 4
```

### 5. Calculate a factorial using a function

Factorial is defined for non-negative integers; by definition, `0!` is `1`.

```python
def factorial(number):
	if number < 0:
		raise ValueError("number must be non-negative")

	result = 1
	for value in range(2, number + 1):
		result *= value
	return result


print(factorial(5))  # 120
```

## 7. Python Interview Preparation

### 1. What is the difference between local and global variables?

A **local variable** is created inside a function and is normally available only while that function is running. A **global variable** is defined at the top level of a module, outside functions, and can be read by functions in that module.

```python
app_name = "Learning App"  # global variable

def show_message():
	message = "Welcome"  # local variable
	print(f"{message} to {app_name}")

show_message()
# Welcome to Learning App
```

Here, `message` belongs to `show_message()` and cannot normally be accessed outside it. `app_name` is defined at module scope, so the function can read it. A local variable with the same name as a global variable takes precedence inside that function; this is called **shadowing**.

To **reassign** a global variable from inside a function, declare it with `global`:

```python
count = 0

def increment():
	global count
	count += 1

increment()
print(count)  # 1
```

Without `global`, an assignment such as `count += 1` makes `count` a local name in that function, and Python will raise `UnboundLocalError` because the local value is read before it has been assigned. Reading a global variable does not require `global`. In general, prefer passing values into functions and returning updated values instead of changing globals: it makes the code easier to test and reason about.

Python resolves names using the **LEGB** order: Local, Enclosing (an outer function), Global (the module), and Built-in. `nonlocal` is used when a nested function needs to reassign a name from its enclosing function, rather than a module-level global.

### 2. What is the difference between positional, keyword, and default arguments?

Arguments are the values supplied when a function is called. Parameters are the names in the function definition that receive those values.

```python
def describe_pet(name, animal="cat"):
	print(f"{name} is a {animal}.")
```

- **Positional arguments** are matched to parameters by their position. `describe_pet("Milo", "dog")` assigns `"Milo"` to `name` and `"dog"` to `animal`.
- **Keyword arguments** identify parameters by name. `describe_pet(name="Milo", animal="dog")` makes the mapping explicit, and keyword arguments can be written in a different order: `describe_pet(animal="dog", name="Milo")`.
- **Default arguments** have a value in the function definition. If the caller omits that argument, Python uses the default: `describe_pet("Milo")` uses `"cat"` for `animal`.

Parameters without defaults must be supplied. In a function definition, parameters with defaults must come after parameters without defaults. In a call, positional arguments must come before keyword arguments, and a parameter should not be given a value twice.

One important Python detail: default values are evaluated **once**, when the function is defined, not each time it is called. Avoid a mutable default such as a list or dictionary when you intend to create a fresh one per call:

```python
def add_item(item, items=None):
	if items is None:
		items = []
	items.append(item)
	return items
```

### 3. What are `*args` and `**kwargs`, and when do we use them?

`*args` collects extra **positional** arguments into a tuple. `**kwargs` collects extra **keyword** arguments into a dictionary. The names `args` and `kwargs` are conventions; the `*` and `**` markers provide the behavior.

```python
def show_inputs(*args, **kwargs):
	print(args)
	print(kwargs)

show_inputs("red", "blue", size="large", in_stock=True)
# ('red', 'blue')
# {'size': 'large', 'in_stock': True}
```

Use them when a function intentionally accepts a variable number of arguments, such as a wrapper that forwards arguments to another function or a helper that supports optional named settings. They can also **unpack** existing collections in a call:

```python
colors = ["red", "blue"]
options = {"size": "large", "in_stock": True}
show_inputs(*colors, **options)
```

The symbols also have a role in function definitions and calls: `*` unpacks an iterable into positional arguments, while `**` unpacks a mapping into keyword arguments. Use these features when they make an API more flexible; explicitly named parameters are usually clearer when the accepted inputs are known.

### 4. What is the difference between `return` and `print()`?

`print()` displays text for a person to see, usually in the terminal. `return` sends a value back to the code that called the function, where it can be stored, transformed, tested, or passed to another function. They are not interchangeable.

```python
def add_and_print(left, right):
	print(left + right)

def add_and_return(left, right):
	return left + right

result = add_and_return(3, 4)
print(result * 2)  # 14

printed_result = add_and_print(3, 4)  # displays 7
print(printed_result)  # None
```

The first function displays `7`, but it does not give that number back to its caller. Since it has no explicit `return`, it returns `None`. The second function returns `7`, allowing the caller to use it later. In reusable functions, return the result; print it separately when you want to show it to a user.

### 5. What is a lambda function, and how is it different from a normal function?

A **lambda** is a small anonymous function written as a single expression. It can accept arguments and produce a result, but its body cannot contain ordinary statements such as `return`, loops, or multiple lines of logic. The value of the expression is returned automatically.

```python
double = lambda number: number * 2
print(double(5))  # 10
```

The equivalent named function is:

```python
def double(number):
	return number * 2
```

Both can be called and return values. A `def` function has a name (unless assigned or otherwise referenced), supports a multi-line body and a docstring, and is generally easier to read, test, and reuse. A lambda is useful for a short one-off operation, often passed as an argument to a function such as `sorted()`:

```python
people = [{"name": "Ava", "age": 31}, {"name": "Ben", "age": 24}]
people_by_age = sorted(people, key=lambda person: person["age"])
```

Use `def` when the logic needs a descriptive name, more than one expression, or additional explanation. Lambdas are expressions, not a special faster kind of function; choose them for brevity only when the result remains easy to understand.
