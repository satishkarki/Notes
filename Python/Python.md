## 100 days of Python Coding

### Python as a language

Developed by Guido van Rossum

It is easier for you to learn python than it is for computer to learn english.

### All 33 reserved words in Python 3

| and      | except  | lambda   | with  |
| -------- | ------- | -------- | ----- |
| as       | finally | nonlocal | while |
| assert   | false   | None     | yield |
| break    | for     | not      |       |
| class    | from    | or       |       |
| continue | global  | pass     |       |
| def      | if      | raise    |       |
| del      | import  | return   |       |
| elif     | in      | True     |       |
| else     | is      | try      |       |

- Integer divison produces a floating point result in python 3.x but it was different in Python 2.x

- type()

- int()

- input(): it gives back us a string

- try/except concept

  ```python
  rawstr=input('Enter a number:')
  try:
  	ival=int(rawstr)
  except:
  	ival=-1
  if ival>0:
  	print('Nice Work')
  else:
  	print('Not a number')
      
  #Output 
  Enter a number:1
  Nice Work
  Enter a number:satish
  Not a number
  ```

- def 

  ```python
  def thing():
  	print('Hello')
  	print('World')
  thing()
  print('Zip')
  
  #Output
  Hello
  World
  Zip
  ```

  Bulit-in Functions

  | **A** [`abs()`](https://docs.python.org/3/library/functions.html#abs) [`aiter()`](https://docs.python.org/3/library/functions.html#aiter) [`all()`](https://docs.python.org/3/library/functions.html#all) [`any()`](https://docs.python.org/3/library/functions.html#any) [`anext()`](https://docs.python.org/3/library/functions.html#anext) [`ascii()`](https://docs.python.org/3/library/functions.html#ascii)   **B** [`bin()`](https://docs.python.org/3/library/functions.html#bin) [`bool()`](https://docs.python.org/3/library/functions.html#bool) [`breakpoint()`](https://docs.python.org/3/library/functions.html#breakpoint) [`bytearray()`](https://docs.python.org/3/library/functions.html#func-bytearray) [`bytes()`](https://docs.python.org/3/library/functions.html#func-bytes)   **C** [`callable()`](https://docs.python.org/3/library/functions.html#callable) [`chr()`](https://docs.python.org/3/library/functions.html#chr) [`classmethod()`](https://docs.python.org/3/library/functions.html#classmethod) [`compile()`](https://docs.python.org/3/library/functions.html#compile) [`complex()`](https://docs.python.org/3/library/functions.html#complex)   **D** [`delattr()`](https://docs.python.org/3/library/functions.html#delattr) [`dict()`](https://docs.python.org/3/library/functions.html#func-dict) [`dir()`](https://docs.python.org/3/library/functions.html#dir) [`divmod()`](https://docs.python.org/3/library/functions.html#divmod) | **E** [`enumerate()`](https://docs.python.org/3/library/functions.html#enumerate) [`eval()`](https://docs.python.org/3/library/functions.html#eval) [`exec()`](https://docs.python.org/3/library/functions.html#exec)   **F** [`filter()`](https://docs.python.org/3/library/functions.html#filter) [`float()`](https://docs.python.org/3/library/functions.html#float) [`format()`](https://docs.python.org/3/library/functions.html#format) [`frozenset()`](https://docs.python.org/3/library/functions.html#func-frozenset)   **G** [`getattr()`](https://docs.python.org/3/library/functions.html#getattr) [`globals()`](https://docs.python.org/3/library/functions.html#globals)   **H** [`hasattr()`](https://docs.python.org/3/library/functions.html#hasattr) [`hash()`](https://docs.python.org/3/library/functions.html#hash) [`help()`](https://docs.python.org/3/library/functions.html#help) [`hex()`](https://docs.python.org/3/library/functions.html#hex)   **I** [`id()`](https://docs.python.org/3/library/functions.html#id) [`input()`](https://docs.python.org/3/library/functions.html#input) [`int()`](https://docs.python.org/3/library/functions.html#int) [`isinstance()`](https://docs.python.org/3/library/functions.html#isinstance) [`issubclass()`](https://docs.python.org/3/library/functions.html#issubclass) [`iter()`](https://docs.python.org/3/library/functions.html#iter) | **L** [`len()`](https://docs.python.org/3/library/functions.html#len) [`list()`](https://docs.python.org/3/library/functions.html#func-list) [`locals()`](https://docs.python.org/3/library/functions.html#locals)   **M** [`map()`](https://docs.python.org/3/library/functions.html#map) [`max()`](https://docs.python.org/3/library/functions.html#max) [`memoryview()`](https://docs.python.org/3/library/functions.html#func-memoryview) [`min()`](https://docs.python.org/3/library/functions.html#min)   **N** [`next()`](https://docs.python.org/3/library/functions.html#next)   **O** [`object()`](https://docs.python.org/3/library/functions.html#object) [`oct()`](https://docs.python.org/3/library/functions.html#oct) [`open()`](https://docs.python.org/3/library/functions.html#open) [`ord()`](https://docs.python.org/3/library/functions.html#ord)   **P** [`pow()`](https://docs.python.org/3/library/functions.html#pow) [`print()`](https://docs.python.org/3/library/functions.html#print) [`property()`](https://docs.python.org/3/library/functions.html#property) | **R** [`range()`](https://docs.python.org/3/library/functions.html#func-range) [`repr()`](https://docs.python.org/3/library/functions.html#repr) [`reversed()`](https://docs.python.org/3/library/functions.html#reversed) [`round()`](https://docs.python.org/3/library/functions.html#round)   **S** [`set()`](https://docs.python.org/3/library/functions.html#func-set) [`setattr()`](https://docs.python.org/3/library/functions.html#setattr) [`slice()`](https://docs.python.org/3/library/functions.html#slice) [`sorted()`](https://docs.python.org/3/library/functions.html#sorted) [`staticmethod()`](https://docs.python.org/3/library/functions.html#staticmethod) [`str()`](https://docs.python.org/3/library/functions.html#func-str) [`sum()`](https://docs.python.org/3/library/functions.html#sum) [`super()`](https://docs.python.org/3/library/functions.html#super)   **T** [`tuple()`](https://docs.python.org/3/library/functions.html#func-tuple) [`type()`](https://docs.python.org/3/library/functions.html#type)   **V** [`vars()`](https://docs.python.org/3/library/functions.html#vars)   **Z** [`zip()`](https://docs.python.org/3/library/functions.html#zip)   **_** [`__import__()`](https://docs.python.org/3/library/functions.html#import__) |
  | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |

  ```python
  print("Hello"[0])
  > H
  ```

  ```python
  print(123456789)
  print(123_456_789)
  # Both gives same output
  ```

- Division gives float value in Python

  ```python
  print(round(9/4, 2))
  print(9/4)
  print(type(9/4))
  print(9//4)
  print(type(9//4))
  #Output
  2.25
  2.25
  <class 'float'>
  2
  <class 'int'>
  ```

- ### f-string

  ```python
  name="Satish"
  age=27
  weight=70.5
  student=True
  print(f"Your name is {name}, age is {age}, weight is {70.5}, and your student status is {student}")
  
  #Output
  Your name is Satish, age is 27, weight is 70.5, and your student status is True
  ```

- ### Rounding up Errors

  ```python
  print(5/2)
  print(round(5/2, 2))
  print("{:.2f}".format(5/2))
  #Output
  2.5
  2.5
  2.50
  ```

- love calculator

  ```python
  print("Welcome to the Love Calculator!")
  name1 = input("What is your name? \n")
  name2 = input("What is their name? \n")
  
  count1=0
  count2=0
  i=0
  j=0
  Name1=name1.upper()
  Name2=name2.upper()
  while i< (len(Name1)):
    if Name1[i]=="T" or Name1[i]=="R" or Name1[i]=="U" or Name1[i]=="E":
      count1+=1
    if Name1[i]=="L" or Name1[i]=="O" or Name1[i]=="V" or Name1[i]=="E":
      count2+=1
    i+=1
  while j< (len(Name2)):
    if Name2[j]=="T" or Name2[j]=="R" or Name2[j]=="U" or Name2[j]=="E":
      count1+=1
    if Name2[j]=="L" or Name2[j]=="O" or Name2[j]=="V" or Name2[j]=="E":
      count2+=1
    j+=1
  print(f"The first digit is {count1}")
  print(f"The second digit is {count2}")
  print(f"Your love percentage is: {str(count1)+str(count2)}%")
  ```

  ### Random Number
  
  ```python
  import random
  #Generates a random number between 0 and 10, both inclusive
  random_integer=random.randint(0,10)
  ```
  
  ### List
  
  ```python
  alist=["Apple","Banana","Orange"]
  alist.append("Watermelon")
  alist.extend("Pineapple","Guava")
  ```
  
  ```python
  #Nested List
  fruit=["Apple","Ornage"]
  vegetable=["Potato","Tomamto"]
  mix=[fruit,vegetable]
  print(mix)
  
  #Output
  [['Apple', 'Ornage'], ['Potato', 'Tomamto']]
  ```
  
  More on List [here](https://docs.python.org/3/tutorial/datastructures.html)

### map()

```python
# Python program to demonstrate working of map. 
# Return double of n
def addition(n):
    return n + n
 
# We double all numbers using map()
numbers = (1, 2, 3, 4)
result = map(addition, numbers)
print(result)
print(type(result))
print(list(result))

#Output
<map object at 0x7fc5705f8160>
<class 'map'>
[2, 4, 6, 8]
```

Crossword Example

```python
# 🚨 Don't change the code below 👇
row1 = ["⬜️","⬜️","⬜️"]
row2 = ["⬜️","⬜️","⬜️"]
row3 = ["⬜️","⬜️","⬜️"]
layout = [row1, row2, row3]
print(f"{row1}\n{row2}\n{row3}")
position = input("Where do you want to put the treasure? ")
# 🚨 Don't change the code above 👆

#Write your code below this row 👇
numbers=list(position)
print(numbers)
test=list(map(int,numbers))
print(test)
layout[test[0]-1][test[1]-1]="X"

#Write your code above this row 👆
# 🚨 Don't change the code below 👇
print(f"{row1}\n{row2}\n{row3}")
```

```python
#Output

['⬜️', '⬜️', '⬜️']
['⬜️', '⬜️', '⬜️']
['⬜️', '⬜️', '⬜️']
Where do you want to put the treasure? 12
['1', '2']
[1, 2]
['⬜️', 'X', '⬜️']
['⬜️', '⬜️', '⬜️']
['⬜️', '⬜️', '⬜️']
```

### Loop

```python
# for with list
students=[1,2,3,4,5]
for student in students:
    print student

# for with range
total=0
for number in range(1, 101) # 101 is not included
	total+=number
print(total)    
    
```

FizzBuzz

```python
for number in range(1,101):
  if number%3==0 and number%5==0:
    print("fizzbuzz")
  elif number% 3==0:
    print("fizz")
  elif number%5==0:
    print("buzz")
  else:
    print(number)
```

Random Password Generator

```python
# How I did and messed up
#Password Generator Project
import random
letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
numbers = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']
symbols = ['!', '#', '$', '%', '&', '(', ')', '*', '+']

print("Welcome to the PyPassword Generator!")
nr_letters= int(input("How many letters would you like in your password?\n")) 
nr_symbols = int(input(f"How many symbols would you like?\n"))
nr_numbers = int(input(f"How many numbers would you like?\n"))

letter_pass=random.choices(letters, k=nr_letters)
letter_string=''.join(map(str,letter_pass))
print(letter_string)

number_pass=random.choices(numbers, k=nr_numbers)
number_string=''.join(map(str,number_pass))
print(number_string)

symbol_pass=random.choices(symbols, k=nr_symbols)
symbol_string=''.join(map(str,symbol_pass))
print(symbol_string)

simple_password=letter_string+number_string+symbol_string
print(f"Your password is {simple_password}")

pass_list=list(simple_password)
print(pass_list)

random_pass=random.choices(simple_password,k=len(simple_password))
your_random_pass=''.join(map(str,random_pass))
print(f"your password is {your_random_pass}")
```

```python
# How Instructor did 
#Password Generator Project
import random
letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
numbers = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']
symbols = ['!', '#', '$', '%', '&', '(', ')', '*', '+']

print("Welcome to the PyPassword Generator!")
nr_letters = int(input("How many letters would you like in your password?\n")) 
nr_symbols = int(input(f"How many symbols would you like?\n"))
nr_numbers = int(input(f"How many numbers would you like?\n"))

#Eazy Level
# password = ""

# for char in range(1, nr_letters + 1):
#   password += random.choice(letters)

# for char in range(1, nr_symbols + 1):
#   password += random.choice(symbols)

# for char in range(1, nr_numbers + 1):
#   password += random.choice(numbers)

# print(password)

#Hard Level
password_list = []

for char in range(1, nr_letters + 1):
  password_list.append(random.choice(letters))

for char in range(1, nr_symbols + 1):
  password_list += random.choice(symbols)

for char in range(1, nr_numbers + 1):
  password_list += random.choice(numbers)

print(password_list)
random.shuffle(password_list)
print(password_list)

password = ""
for char in password_list:
  password += char

print(f"Your password is: {password}")
```





