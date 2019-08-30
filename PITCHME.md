### Python

---

### Syntax

+++

### Variables 

```python
a = 123
b = True
c = False
d = "abc"
e = [1,2,3]
f = {
    "message": "hello world"
}
```

+++

### Lists and Dicts

```python

# accessing item in array
arr = [1,2,3]
arr[0] == 1

# adding item to array
arr.append(24)
arr.insert(0, 12)

# accessing item in dict
data = {"message": "hello world"}
data["message"] == "hello world"

# merging 2 dicts
data.update({"second_message": "hello me"})

# deleting key from dict
del data["message"]
```

+++

### Functions

- based on indentation, no curly braces

```python
def sum(x,y):
    return x + y

def multiply(x,y):
    return x * y
```

+++

### Loops

```python
arr = [True, True, False]

for x in arr:
    print(x)

for idx, x in enumerate(arr):
    print(idx)
    print(x)

# for dicts

data = {"message": "hello world"}

for key, value in data.items():
    print(key)
    print(value)

# for strings

for letter in "hello":
    print(letter)
```

+++

### List Comprehensions

- processing values in arrays/dicts

```python
arr = [1,2,3]

results = [ x * 5 for x in arr]
results2 = [ x + x for x in arr]

print(results)
print(results2)
```

---

### Exercises

---

### Pig Latin

1. find the first vowel
2. shift all non-vowels behind the section starting from the first vowel and adds <span class="text-gold">ay</span>
3. if the word starts with vowel, don't change it
4. if there is no vowel in the word, add <span class="text-gold">ay</span> behind.

+++

```python
def convert(word):
    # write your code here
    pass

print(convert("art") == ("art"))
print(convert("vowel") == ("owelvay"))
print(convert("nginx") == ("inxngay"))
print(convert("hello") == ("ellohay"))
print(convert("Dr") == ("Dray"))
}
```

---

### Binary search

![image](https://www.mathwarehouse.com/programming/images/binary-vs-linear-search/binary-and-linear-search-animations.gif)

+++

```python
def bsearch(arr, target):
    # write your code here
    pass

x = [7,9,21,42,58,67,88]

print(bsearch(x, 67) == 5)
print(bsearch(x, 9) == 1)
```

---

### Tic Tac Toe

- 2 players
- display board in terminal
- player can enter board idx to place piece
- can switch to second player and vice versa
- will show who won or if its a draw

+++

```python
def play:
    # write your code here
    pass

play()

# getting input from the user
x = input("Please enter the board index to place your piece")
print(x)
```

---

### Basic Web App

---

### Web Frameworks

- flask (simple web apps)
- django (all-in-one framework)

---

### Basic Flask App

- render HTML
- render JSON
- respond to GET/POST requests

---

### Instructions

```bash
mkdir <app-name>
cd <app-name>
poetry init
poetry add flask
```

+++

### Creating the Webserver

```python
# app.py

from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return f'Hello World'
```

---

### Assignment

- build a sudoku solver web app
- it receives a json

```python
{
    "board": "105802000090076405200400819019007306762083090000061050007600030430020501600308900"
}
```

- it will solve the board and return in response

```python
{
    "board": "145892673893176425276435819519247386762583194384961752957614238438729561621358947"
}
```