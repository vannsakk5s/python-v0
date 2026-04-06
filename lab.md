# 1. Understand What a Function Is (Function គឺជាអ្វី?)

Function គឺជាកូដមួយក្រុម (block of code) ដែលត្រូវបានសរសេរឡើង ដើម្បីអោយវាធ្វើការងារមួយជាក់លាក់ ហើយអាចហៅប្រើបានជាច្រើនដង។

**Function ដូចជា ម៉ាស៊ីន**
* អ្នកដាក់ input (ទិន្នន័យ)
* វាដំណើរការ
* ហើយវាផ្តល់ output (លទ្ធផល)

**In Python:**
```python
def say_hello():
    print("Hello!")
```

Function គឺ កូដដែលធ្វើការងារមួយ
* វាមាន ឈ្មោះ
* អាច ហៅប្រើបានច្រើនដង
* អាចមាន input (parameter) និង output (return)

---

# 2. Create and Calling a Function (ការបង្កើត និងហៅ Function)

* **Create a function** = ការសរសេរ Function ថ្មីមួយ
* **Calling a function** = ការហៅ Function ឲ្យវាដំណើរការ

**In Python:**

*   **Create:**
    ```python
    def greet():
        print("Hello!")
    ```
*   **Call:**
    ```python
    greet()
    greet()
    ```

✅ `def` = បង្កើត function
✅ `ឈ្មោះ + ()` = ហៅ function
✅ ត្រូវហៅ ទើបវាដំណើរការ

---

# 3. Parameters (Input) (ទិន្នន័យចូលទៅក្នុង Function)

Parameters គឺជាទិន្នន័យ (input) ដែលយើងផ្តល់ឲ្យ Function ដើម្បីអោយវាធ្វើការងារ។

**Function ដូចជា ម៉ាស៊ីនគណនា** 🧮
* អ្នកដាក់លេខចូល (input)
* វាគណនា
* ហើយចេញលទ្ធផល
* លេខដែលអ្នកដាក់ = Parameter

**In Python:**
```python
def greet(name):
    print("Hello", name)
```
* `name` = Parameter
* **Call:** `greet("Dara")` `greet("Dara")`

| Parameter | Argument |
| :--- | :--- |
| នៅក្នុង function | នៅពេលហៅ function |
| ឧ. `name` | ឧ. `"Dara"` |

```python
def add(a, b):
    print(a + b)

add(3, 5)

def greet(name):
    print(name)

greet()  # ❌ (Error)
```

✅ **Parameter** = input ក្នុង function
✅ **Argument** = តម្លៃពេលហៅ
✅ អាចមាន 1 ឬ ច្រើន
✅ ត្រូវដាក់ឲ្យត្រូវចំនួន

---

# 4. Return Values (តម្លៃដែល Function ផ្ញើត្រឡប់)

Return Value គឺជាលទ្ធផលដែល Function ផ្ញើត្រឡប់មកវិញ បន្ទាប់ពីវាដំណើរការ។

*   **Create:**
    ```python
    def add(a, b):
        return a + b
    ```
*   **Call:**
    ```python
    result = add(3, 5)
    print(result) # result = 8
    ```

**`print` vs `return`**

| `print` | `return` |
| :--- | :--- |
| ```python<br>def add(a, b):<br>    print(a + b)<br>``` | ```python<br>def add(a, b):<br>    return a + b<br>``` |
| 👉 បង្ហាញលទ្ធផល ប៉ុណ្ណោះ | `x = add(2, 3)` |
| 👉 មិនអាចយកទៅប្រើបន្តបាន | `y = x * 10`<br>`print(y)   # 50` |

*Issue:*
```python
def test():
    return 1
    print("Hello")  # ❌ មិនដំណើរការ
```

✅ **return** = ផ្ញើលទ្ធផលត្រឡប់
✅ អាចយកទៅប្រើបន្តបាន
✅ function បញ្ចប់ពេល return
✅ ខុសពី print

---

# 5. Default Parameters (Parameter មានតម្លៃលំនាំដើម)

Default Parameter គឺជា parameter ដែលមានតម្លៃកំណត់ទុកជាមុន បើអ្នកមិនផ្តល់ argument ពេលហៅ function។

*   **Create:**
    ```python
    def greet(name="Guest"):
        print("Hello", name)
    ```
*   **Call without Argument:**
    ```python
    greet() # -> Hello Guest
    ```
*   **Call with Argument:**
    ```python
    greet("Dara") # -> Hello Dara
    ```

បើអ្នកដាក់ argument → វាមិនប្រើ default ទេ

✅ **Default** = តម្លៃដើម
✅ ប្រើពេលមិនដាក់ argument
✅ អាចប្ដូរបាន
✅ ត្រូវសរសេរនៅខាងក្រោយ

---

# 6. Multiple Arguments (Arguments ច្រើនក្នុង Function)

Multiple Arguments គឺជាការដាក់ទិន្នន័យច្រើនជាងមួយទៅក្នុង Function។

```python
def add(a, b):
    print(a + b)

add(3, 5) # -> 8

def add_three(a, b, c):
    print(a + b + c)

add_three(1, 2, 3) # -> 6

def add(a, b):
    print(a + b)

add(5)   # ❌ Error
```

✅ Function អាចមាន parameter ច្រើន
✅ ត្រូវដាក់ argument ត្រឹមត្រូវ
✅ លំដាប់មានសារៈសំខាន់
✅ អាចប្រើជាមួយ return

---

# 7. Keyword Arguments (Arguments ដាក់តាមឈ្មោះ)

Keyword Arguments គឺជាការផ្តល់តម្លៃទៅ Function ដោយប្រើឈ្មោះ parameter។

```python
def student(name, age):
    print("Name:", name)
    print("Age:", age)

student("Dara", 20)           # Normal Arguments
student(age=20, name="Dara")  # Keyword Arguments

student(name="Dara", 20)      # ❌ Error
student("Dara", age=20)       # ✅
```

---

# 8. Arbitrary Arguments (*args, **kwargs)

Arbitrary Arguments គឺជាវិធីអោយ Function ទទួល Arguments ច្រើន ដោយមិនចាំបាច់កំណត់ចំនួនជាមុន។

### `*args` អនុញ្ញាតឲ្យ Function ទទួល Arguments ជាច្រើន (តាមលំដាប់)

```python
def add_all(*numbers):
    print(numbers)

add_all(1, 2, 3, 4) # -> (1, 2, 3, 4)

def add_all(*numbers):
    total = 0
    for n in numbers:
        total += n
    return total

print(add_all(1, 2, 3))      # 6
print(add_all(5, 10, 15))    # 30
```
👉 `*numbers` = ទទួលលេខច្រើន
👉 `numbers` = tuple

### `**kwargs` អនុញ្ញាតឲ្យ Function ទទួល Arguments ជាច្រើនជា `key=value`

```python
def show_info(**data):
    print(data)

show_info(name="Dara", age=20)
# {'name': 'Dara', 'age': 20}

def show_info(**data):
    for key, value in data.items():
        print(key, "=", value)

show_info(name="Sok", age=18)
# name = Sok
# age = 18
```

1. `*args` → tuple
2. `**kwargs` → dictionary

✅ `*args` = Arguments ច្រើន (tuple)
✅ `**kwargs` = `key=value` (dictionary)
✅ ប្រើពេលមិនដឹងចំនួន argument
✅ អាចប្រើជាមួយគ្នា
