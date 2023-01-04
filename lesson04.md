# Урок 4. Списки, рядки та генератор списків

## Мінливі та незмінні типи даних

У Python є мінливі (mutable) та незмінні (immutable) типи даних.

Раніше розглядався тип даних int, який є незмінним. Так само незмінними є типи даних tuple (кортеж) і string (рядок).

Що значить незмінні? Значить, що вже створений рядок ми не можемо змінити. Це легко покажуть подальші приклади із рядками і кортежами. Якщо ж здається, що об'єкт одного з перерахованих даних змінився - значить, тепер ім'я об'єкта просто вказує на нову область пам'яті з новим об'єктом.

## Рядки

### Створення рядків, лапки

У python між одинарними й подвійними лапками практично немає різниці, а ще є два види потрійних. Всі типи лапок можуть бути вставлені одні в одні. Потрійні так же дозволяють перехід на новий рядок всередині рядка:

```python
S1 = 'Welcome to strings'
S2 = "Another string"
S3 = """And '''another'''
long
string"""
S4 = 'This "string" is a bit """crazy"""'
```

### Прості операції

Прості арифметичні операції складання і множення доступні і з рядками. У прикладі нижче - складання двох рядків (конкатенація), множення рядка на число та взяття конкретного елемента рядка за його індексом. Індекси у всіх послідовностях у програмуванні вважаються від нуля. По негативному індексу - відраховуємо від кінця рядка назад.

```python
S = 'abc'
print (len(S)) # 3
S = S + '12' # В S = 'abc12'
print (S[2])   # 'c'
print ('ab'*2) #  'abab'
```


### Рядки - незмінний тип

Тепер перевіримо, наскільки незмінними є рядки і як з цим боротися:


```python
S = 'asdfghj'
S[5] = 's'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
S = S[:5] + 's' + S[6:]
```

### Зрізи строк

Python дозволяє взяти частину рядка або навіть скласти з елементів рядка будь-який новий рядок, використовуючи фрагменти (зрізи). Приклади:

```python
>>> S = "Welcome to California!"
>>> S
'Welcome to California!'
>>> S[:5]
'Welco'
>>> S[5:]
'me to California!'
>>> S[:]
'Welcome to California!'
>>> S[:-3]
'Welcome to Californ'
>>> S[::-1]
'!ainrofilaC ot emocleW'
>>> S[:5:2]
'Wlo'
```

З прикладу видно, що зрізи створюються шляхом вказівки у квадратних дужках обов'язкової двокрапки. Число до двокрапки - від якого елемента показувати, після - до якого, не включаючи його. Якщо не вказано перше число - показати від початку, якщо не вказано друге - до кінця. Друга двокрапка дозволяє вказати третє число - крок, з яким потрібно йти по послідовності.

### Корисні функції роботи з рядками

```python
>>> S
'Welcome to California!'
>>> len(S) # get length of the string
22
>>> S.find('C') # get index of the first substring found
11
>>> S.replace('C', '7') # Replaces all the substrings to the new one mentioned
'Welcome to 7alifornia!'
>>> S.split() # Cuts the string using the separator provided, creates a list. By default space is used as a separator
['Welcome', 'to', 'California!']
>>> S.upper()
'WELCOME TO CALIFORNIA!'
>>> S += '\n\n'
>>> S
'Welcome to California!\n\n'
>>> S.rstrip() # removes space-like symbols at the end of string
'Welcome to California!'
```

Додаткову інформацію про рядки та функції роботи з ними можна знайти за посиланням: 
[Детальніше про рядки](http://rtfm.co.ua/python_s_nulya/python-s-nulya-chast-7-stroki/)

### Форматування рядків

Існує багато засобів створення рядків. Можна створювати новий рядок, використовуючи як існуючи рядки у змінних, так і нові літерали. Найпростіший варіант - конкатенація:

```python
>>> S = 'Welcome to'
>>> C = 'Ukraine!'
>>> print(S + ' ' + C)
>>> 
Welcome to Ukraine!
```

#### Форматування з оператором %

Є найбільш застарілий варіант форматування рядків за допомогою оператора %. Цей підхід зʼявився ще у часи створення мови програмування Фортран [(Printf)](https://ru.wikipedia.org/wiki/Printf) 

Працює це так:

```python
>>> S = 'Welcome to'
>>> C = 'Ukraine!'
>>> print('%s %s' % (S, C))
>>>
Welcome to Ukraine!
```

- **`%s`** всередині рядка означає, що тут буде підставлено рядок
- **`%`** після рядку - оператор підставляння
- кортеж з двома змінними - рядками, яких буде підставлено замість **`%s`**

Окрім **`%s`** для позначення рядка, також використовуються **`%d`** для цілих чисел та **`%f`** для чисел с крапкою, що плаває:

```python
>>> C = 'Ukraine'
>>> S = 'welcomed'
>>> print('%d people are %s in %s!' % (3, S, C))
3 people are welcomed in Ukraine!
```

[Декілька варіантів використання оператора форматування %](https://pythonworld.ru/osnovy/formatirovanie-strok-operator.html)

#### Форматування за допомогою метода .format()

Метод `.format()` є свіжішим та покращує синтаксис форматування в цілому, але при обробці великих рядків все ж таки буде виникати проблема з читанням.

Використовуючи метод рядка **.format()** можна форматувати рядок різними способами:
- підставляючи змінні підряд, вказуючи позицію
- підставляючи змінні підряд без вказання позиції
- підставляючи змінні по назві
- в змішаному стилі

Наприклад, з вказанням позиції:

```python
>>> S = "Information! {0} people are {1} {2} {3}!"
>>> S.format(3, 'welcomed', 'in', 'Ukraine')
'Information! 3 people are welcomed in Ukraine!'
```
Без вказання позиції:

```python
>>> S = "Information! {} people are {} {} {}!"
>>> S.format(3, 'welcomed', 'in', 'Ukraine')
'Information! 3 people are welcomed in Ukraine!'
```

З назвою:

```python
S = "Information! Russian people are {reaction} {pretext} {country}!"
print(S.format(country = "USA", pretext = "over", reaction = 'hated'))
# Information! Russian people are hated over USA!
```

[Більше інформації за посиланням](https://pyprog.pro/python/py/str/str_format_method.html)

#### Форматування за допомогою префіксу `f`

Найсвіжіший варіант форматування рядків - за допомогою префіксу `f`. Знайомимось на прикладі:

```python
>>> name = 'Jake'
>>> f'He said his name is {name}'
# 'He said his name is Jake'
>>> f'He said his name is {name!r}'
# "He said his name is 'Jake'"
```

Цей варіант швидший або принаймні такий же швидкий, як інші варіанти форматування, але читається набагато легше.

Зверніть увагу на `!r`, це цукор для виклику метода `repr()`, що показує репрезентативний варіант обʼєкта. Є ще цікаві варіанти методів `str()` та `ascii()`, відповідно `!s` та `!a`. Перший повертає обʼєкт у вигляді рядка, другий - у презентативному вигляді, але на відміну від `repr()`, він екранує символи, які не є стандартними літерами.

А ось ще цікавий приклад мультірядкового варіанта форматування:

```python
name = "Eric"
profession = "comedian"
affiliation = "Monty Python"
message = (
    f"Hi {name}. "
    f"You are a {profession}. "
    f"You were in {affiliation}."
)
print(message)
#'Hi Eric. You are a comedian. You were in Monty Python.'
```

[Велика стаття по префіксах та форматуванню](https://pyprog.pro/python/py/str/str_lit.html)


# List (список)

### Створення списків

В python відсутні масиви в традиційному розумінні цього терміну. Натомість для зберігання однорідних (і не тільки) об'єктів використовуються списки. Вони задаються багатьма способами: 

```python
# empty list
>>>empty_list = []
# Simple listing
>>> a = [2, 2.25, "Python"]
>>> a
[2, 2.25, 'Python']

# Transforming the string to a list
>>> b = list("help")
>>> b
['h', 'e', 'l', 'p']

>>> b = 'welcome to the hell'.split()
>>> b
['welcome', 'to', 'the', 'hell']

```

### Операції зрізів та вставок зі списками

До списків застосовні всі зрізи, що застосовуються до рядків. На додаток, до списків таким чином можна ще й додавати нові елементи.

```python
L = [1, 2, 's']
>>> L
[1, 2, 's']
>>> L[1:3]
[2, 's']
>>> L[2] = '17'
>>> L
[1, 2, '17']
>>> L[1:2]
[2]
>>> L[1:2] = ['new', 'list']
>>> L
[1, 'new', 'list', '17']
```


### Деякі функції, що працюють зі списками

```python
>>> L = list(range(1, 11))
>>> L
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
>>> L.append(12) # Adds element at the end of the list
>>> L
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 12]
>>> L.extend([13, 14]) # Adds second's list elements to the end of the first list
>>> L
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 12, 13, 14]
>>> L.insert(2, 5) # Insert 5 to the second place (index)
>>> L
[1, 2, 5, 3, 4, 5, 6, 7, 8, 9, 10, 12, 13, 14]
>>> L.remove(5) # Removes the first 5 appeared
>>> L
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 12, 13, 14]
```


```python
>>> L
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
# map function applies the method given to the iterable proposed
>>> L = list(map(str, range(1, 11)))
>>> L # Here we have casted all integers to strings
['1', '2', '3', '4', '5', '6', '7', '8', '9', '10']
>>> S = ': '.join(L) # concats small strings into one big, using "glue". Starts as a method of "glue"
>>> S
'1: 2: 3: 4: 5: 6: 7: 8: 9: 10'
```

### Цикли та списки

Цикл for спеціально створений для того, щоб виконувати повторювані дії зі списками та іншими об'єктами, що ітеруються. Пара прикладів:

```python
>>> S = 'This is Sparta!!'
>>> L = S.split()
>>> L
['This', 'is', 'Sparta!!']
>>> for elem in L:
...     print('say ' + elem)
...
say This
say is
say Sparta!!

>>> for num, elem in enumerate(L):
...     print (str(num) + '. say ' + elem)
...
0. say This
1. say is
2. say Sparta!!
```

Зверніть увагу на функцію enumerate, яка видає не лише вміст списку, а і його порядковий номер.

### List comprehensions (Спискові включення)

У мовах програмування є таке поняття, як синтаксичний цукор. Це можливості мови за деяким спрощенням мовних конструкцій, які не впливають на виконання конструкцій, але спрощують життя програміста. Найпопулярніший і найпоширеніший приклад - спискові включення, list comprehensions.

Нижче наведено приклади приведення звичайного циклу до спискового включення:

```python
>>> l = []
>>> for x in range(1, 11):
...     l.append(x*x)
...
>>> l
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

# now with the list comprehension
>>> l2 = [x*x for x in range(1, 11)]
>>> l2
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

Синтаксис у list comprehensions приблизно такий:

`result_list = [actions_with_var for var in list if condition]`

Як видно з синтаксису, можна навіть додати перевірку певної умови, з виконання якої ми додаватимемо або не додаватимемо елемент до результівного списку.

## Посилання

[List comprehensions за 5 хвилин](https://medium.com/nuances-of-programming/list-comprehensions-%D0%B2-python-%D0%B7%D0%B0-5-%D0%BC%D0%B8%D0%BD%D1%83%D1%82-4e5ff3cafd62)

[Зрізи](https://habr.com/ru/post/319200/)

[Домашка](hw04.md)
