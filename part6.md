## Содержание 
 - [34.Кортежи(tuple) и их методы](#34кортежиtuple-и-их-методы) 
 - [35.Тип данных NoneType](#35тип-данных-nonetype)
 - [36.Множества (set) и их методы](#36множества-set-и-их-методы)
 - [37.Операции над множествами. Сравнение множеств](#37операции-над-множествами-сравнение-множеств)
 - [38.Генераторы множеств, frozenset](#38генераторы-множеств-frozenset)

## 34.Кортежи(tuple) и их методы

**Кортеж** - это упорядоченная, но неизменяемая последовательность произвольных данных.

<h3 align="center">Кортежи</h3>

Кортежи по своей природе (задумке) – неизменяемые аналоги списков. Поэтому программный код:

```python
my_tuple = (1, 2, 3, 4, 5)
my_tuple[0] = 9
my_tuple[4] = 7
print(my_tuple)
```

приводит к ошибке

```python
TypeError: 'tuple' object does not support item assignment
```
<h3 align="center">Кортеж с одним элементом</h3>

Для создания кортежа с единственным элементом после значения элемента ставят замыкающую запятую:

```python
my_tuple = (1,)
print(type(my_tuple))     # <class 'tuple'>
```

Если запятую пропустить, то кортеж создан не будет. Например, приведенный ниже код просто присваивает переменной my_tuple целочисленное значение 1:

```python
my_tuple = (1)
print(type(my_tuple))     # <class 'int'>
```

<h3 align="center">Зачем использовать кортеж вместо списка?</h3>

**Неизменяемость кортежей** обеспечивает им особые свойства:

- **скорость** – кортежи быстрее работают, так как из-за неизменяемости хранятся в памяти иначе, и операции с их элементами выполняются заведомо быстрее, чем с
компонентами списка. Обработка кортежа выполняется быстрее, чем обработка списка, поэтому кортежи удобны для обработки большого объема неизменных данных.

- **безопасность** – неизменяемость превращает их в идеальные константы. Заданные кортежами константы делают код более читаемым и безопасным. Кроме того, в кортеже
можно безопасно хранить данные, не опасаясь, что они будут случайно или преднамеренно изменены в программе.

> Списки предназначены для объединения неопределенного количества однородных сущностей. Кортежи, как правило, объединяют под одним именем несколько разнородных
>  объектов, имеющих различный смысл.

<h3 align="center">Функция tuple()</h3>

Функция `tuple` принимает на вход итерируемый объект и превращает его в кортеж.

```python
str_list = ['один', 'два', 'три']
str_tuple = tuple(str_list)
print(str_tuple)  # ('один', 'два', 'три')
text = 'hello python'
str_tuple = tuple(text)
print(str_tuple)  # ('h', 'e', 'l', 'l', 'o', ' ', 'p', 'y', 't', 'h', 'o', 'n')
```

С помощью функции `tuple` можно создать пустой кортеж

```python
t = tuple()
print(type(t))  # <class 'tuple'>
```

> Кортежи поддерживают те же операции, что и списки, за исключением изменяющих содержимое.

<h4 align="center">Функция len()</h4>

**Длиной кортежа** называется количество его элементов. Для того, чтобы посчитать длину кортежа мы используем встроенную функцию `len()`.

```python
numbers = (2, 4, 6, 8, 10)
languages = ('Python', 'C#', 'C++', 'Java')

print(len(numbers))      # 5
print(len(languages))    # 4
```

<h4 align="center">Оператор принадлежности in</h4>

Оператор `in` позволяет проверить, содержит ли кортеж некоторый элемент.

```python
numbers = (2, 4, 6, 8, 10)
print(2 in numbers)  # True
print(8 not in numbers)  # False
```

<h4 align="center">Индексация</h4>

Для индексации кортежей в Python используются квадратные скобки `[]`, в которых указывается индекс нужного элемента в кортеже.

Пусть `numbers = (2, 4, 6, 8, 10)`

| Выражение | Выражение | Результат |
| --------- | --------- | --------- |
| `numbers[0]` | `numbers[-5]` | 2 |
| `numbers[1]` | `numbers[-4]` | 4 |
| `numbers[2]` | `numbers[-3]` | 6 |
| `numbers[3]` | `numbers[-2]` | 8 |
| `numbers[4]` | `numbers[-1]` | 10 |

Обращение по несуществующему индексу приводит к ошибке:

```python
numbers[34]  # IndexError: tuple index out of range
```

<h4 align="center">Срезы</h4>

Пусть `numbers = (2, 4, 6, 8, 10)`

С помощью среза мы можем получить несколько элементов кортежа, создав диапазон индексов разделенных двоеточием `numbers[x:y]`.

```python
print(numbers[1:3])  # (4, 6)
print(numbers[2:5])  # (6, 8, 10)
```
При использовании срезов с кортежами мы также можем опускать второй параметр в срезе `numbers[x:]`, тогда срез берется до конца кортежа. Аналогично если опустить
первый параметр `numbers[:y]`, то можно взять срез от начала кортежа. Как и в списках, можно использовать отрицательные индексы в срезах кортежей.

>  В отличии от списков срез `numbers[:]` не возвращает копию исходного кортежа, а возвращает ссылку на тот же кортеж:
> ```python
> tp1 = (1, 2, 3)
> tp2 = tp1[:]
> print(id(tp1), id(tp2))  # 2307512686208 2307512686208
> ```

<h4 align="center">Операция конкатенации + и умножения на число *</h4>

Операторы `+` и `*` применяют для кортежей:

```python
print((1, 2, 3, 4) + (5, 6, 7, 8))  # (1, 2, 3, 4, 5, 6, 7, 8)
print((7, 8) * 3)  # (7, 8, 7, 8, 7, 8)
print((0,) * 10)  # (0, 0, 0, 0, 0, 0, 0, 0, 0, 0)
``` 

Расширенные операторы `+=` и `*=` также можно использовать при работе с кортежами:

```python
a = (1, 2, 3, 4)
b = (7, 8)
a += b   # добавляем к кортежу a кортеж b
b *= 5   # повторяем кортеж b 5 раз 

print(a)  # (1, 2, 3, 4, 7, 8)
print(b)  # (7, 8, 7, 8, 7, 8, 7, 8, 7, 8)
```

> В действительности измененение кортежа при таких операциях не происходит, создается новый кортеж и присваивается в переменную.

<h4 align="center">Встроенные функции sum(), min(), max()</h4>

Встроенная функция `sum()` может принимать кортеж чисел и вычисляет сумму его элементов.

```python
numbers = (1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
print(sum(numbers))  # 55
```

Встроенные функции `min()` и `max()` могут принимать в качестве параметра кортеж и находят минимальный и максимальный элементы соответственно.

```python
numbers = (3, 4, 10, 3333, 12, -7, -5, 4)
print(min(numbers))  # -7
print(max(numbers))  # 3333
```

<h4 align="center">Метод index()</h4>

Метод `index()` возвращает индекс первого элемента, значение которого равняется переданному в метод значению. В метод передается три параметра(1 обязательный и
2 необязательных(`start` и `stop`)):

 1. `value`: значение, индекс которого требуется найти.
 2. `start`: индекс с которого начинаем поиск
 3. `stop`: индекс на котором закончиваем поиск, не включая его
 
Если элемент в кортеже не найден, то во время выполнения происходит ошибка.

```python
names = ('Gvido', 'Roman' , 'Timur')
position = names.index('Timur')
print(position)  # 2
position = names.index('Anders')
print(position)  # ValueError: tuple.index(x): x not in tuple
```
Чтобы избежать таких ошибок, можно использовать метод `index()` вместе с оператором принадлежности `in`.

<h4 align="center">Метод count()</h4>

Метод `count()` возвращает количество элементов в кортеже, значения которых равны переданному в метод значению. 

Таким образом, в метод передается один параметр:

- `value`: значение, количество элементов, равных которому,  нужно посчитать.

Если значение в кортеже не найдено, то метод возвращает 0.

Следующий программный код:

```python
names = ('Timur', 'Gvido', 'Roman', 'Timur', 'Anders', 'Timur')
cnt1 = names.count('Timur')
cnt2 = names.count('Josef')

print(cnt1)  # 3
print(cnt2)  # 0
```

<h3 align="center">Вложенные кортежи</h3>

Подобно спискам, мы можем создавать вложенные кортежи.

```python
colors = ('red', ('green', 'blue'), 'yellow')
numbers = (1, 2, (4, (6, 7, 8, 9)), 10, 11)
print(colors[1][1])  # blue
print(numbers[2][1][3])  # 9
```

<h3 align="center">Перебор кортежей</h3>

Для вывода каждого из элементов кортежа:

**Вариант 1**. Если нужны индексы элементов:

```python
numbers = (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

for i in range(len(numbers)):
    print(numbers[i])
```    
    
**Вариант 2**. Если индексы не нужны:

```python
numbers = (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

for num in numbers:
    print(num)
```    
    
Можно также использовать операцию распаковки кортежа:

```python
numbers = (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
languages = ('Python', 'C++', 'Java')

print(*numbers)
print(*languages, sep='\n')
```

выводит:

```
0 1 2 3 4 5 6 7 8 9 10
Python
C++
Java
```

<h3 align="center">Сравнение кортежей</h3>

Приведенный ниже код:

```python
print((1, 8) == (1, 8))  # True
print((1, 8) != (1, 10))  # True
print((1, 9) < (1, 2))  # False
print((2, 5) < (6,))  # True
print(('a', 'bc') > ('a', 'de'))  # False
```

> Операции `==` и `!=` применимы к любым кортежам, независимо от типов элементов. А вот операции `<`, `>`, `<=`, `>=` применимы только в том случае, когда
>  соответствующие элементы кортежей имеют один тип.

Приведенный ниже код:

```python
print((7, 5) < ('java', 'python'))
```

выводит:

```python
TypeError: '<' not supported between instances of 'int' and 'str'
```

<h3 align="center">Сортировка кортежей</h3>

```python
not_sorted_tuple = (34, 1, 8, 67, 5, 9, 0, 23)
print(not_sorted_tuple)  # (34, 1, 8, 67, 5, 9, 0, 23)

sorted_tuple = tuple(sorted(not_sorted_tuple))
print(sorted_tuple)  # (0, 1, 5, 8, 9, 23, 34, 67)
```

<h3 align="center">Упаковка кортежей</h3>

Упаковкой кортежа называют присваивание его какой-либо переменной(выполняется всегда, когда справа от знака равенства стоит больше одного значения).

Приведенный ниже код автоматически запакует `1`, `2`, `3` и `'b'`, в кортежи `(1, 2, 3)` и `('b', )` и присвоит их значения переменным `tuple1` и `tuple2`:

```python
tuple1 = 1, 2, 3
tuple2 = 'b',

print(type(tuple1))  # <class 'tuple'>
print(type(tuple2))  # <class 'tuple'>
```

<h3 align="center">Распаковка кортежей</h3>

Обратная операция, смысл которой в том, чтобы присвоить значения элементов кортежа отдельным переменным называется распаковкой кортежа:

```python
colors = ('red', 'green', 'blue', 'cyan')

a, b, c, d = colors

print(a)  # red
print(b)  # green
print(c)  # blue
print(d)  # cyan
```

Количество переменных должно совпадать с числом элементов в кортеже.

Приведенный ниже код:

```python
colors = ('red', 'green', 'blue', 'cyan')
a, b = colors
```

приводит к ошибке:

```python
ValueError: too many values to unpack
```
> Если необходимо получить лишь какие-то отдельные значения, то в качестве "ненужных" переменных позволено использовать символ нижнего подчеркивания `_`.

<h3 align="center">* при распаковке кортежей</h3>

Есть способ собрать сразу несколько значений в одну переменную. Это делается при помощи звездочки перед именем переменной:

```python
a, b, *tail = 1, 2, 3, 4, 5, 6
```

В переменной `a` будет записана 1, в переменной `b` — 2, а в переменной `tail` — список, состоящий из всех аргументов, которые не попали в
предыдущие переменные. В данном случае `tail` будет равен `[3, 4, 5, 6]`.

 > Звездочка может быть только у одного аргумента.


## Задания

1. В переменную city_name вводится название города (например, Москва), а в переменную city_year – год его основания (например, 
1147). Заполните пропущенную строку таким образом, чтобы в переменной city оказался кортеж из значений этих двух переменных
(сначала название города, затем год основания).

```python
city_name = input()
city_year = int(input())
city = city_name, city_year
print(city)
```

2. Дополните приведенный код, так чтобы получить список, содержащий только непустые кортежи исходного списка tuples, не меняя 
порядка их следования.

```python
tuples = [(), (), ('',), ('a', 'b'), (), ('a', 'b', 'c'), (1,), (), (), ('d',), ('', ''), ()]
non_empty_tuples = [el for el in tuples if el]

print(non_empty_tuples)
```

3. Вводятся имена студентов в одну строчку через пробел. На их основе формируется кортеж. Отобразите на экране все имена из 
этого кортежа, которые содержат фрагмент "ва" (без учета регистра). Имена выводятся в одну строчку через пробел в нижнем 
регистре (малыми буквами).

```python
lst = [c.lower() for c in input().split()]
names = tuple([name for name in lst if "ва" in name])
print(*names)
```

4. Дополните приведенный код так, чтобы переменная new_tuples, содержала список кортежей на основе списка tuples с последним
элементом каждого кортежа, замененным на численное значение 100.

```python
tuples = [(10, 20, 40), (40, 50, 60), (70, 80, 90), (10, 90), (1, 2, 3, 4), (5, 6, 10, 2, 1, 77)]
new_tuples = [_tuple[:-1] + (100, ) for _tuple in tuples]
print(new_tuples)
```

5. Вводятся целые числа в одну строку через пробел. На их основе формируется кортеж. Необходимо создать еще один кортеж с 
уникальными (не повторяющимися) значениями из первого кортежа. Результат отобразите в виде списка чисел через пробел.

```python
a = tuple([int(i) for i in input().split()])
t = ()
for el in a:
    if el not in t:
        t = t + (el,)
print(*t)
```

6. Напишите программу, которая выводит список хорошистов и отличников в классе.

**Формат входных данных**

На вход программе подается натуральное число n, далее следует n строк с фамилией школьника и его оценкой на каждой из них.

**Формат выходных данных**
Программа должна вывести сначала все введённые строки с фамилиями и оценками учеников в том же порядке. Затем следует пустая 
строка, а затем выводятся строки с фамилиями и оценками хорошистов и отличников (в том же порядке).

```python
excellent_students = []
count = int(input())
for _ in range(count):
    student, estimation = input().split()
    if int(estimation) >= 4:
        excellent_students.append((student, int(estimation)))
    print(student, int(estimation))
print()
for row in excellent_students:
    print(*row)
```

## 35.Тип данных NoneType

<h3 align="center">Литерал None</h3>

Литерал `None` в `Python` представляет переменную, которая не содержит какого-либо значения. `None` – это объект специального типа данных `NoneType`.

```python
var = None
print(type(var))  # <class 'NoneType'>
```

Мы можем присвоить значение `None` любой переменной, однако мы не можем самостоятельно создать другой `NoneType` объект.

<h3 align="center">Проверка на None</h3>

Для того, чтобы проверить значение переменной на `None`, используется оператор `is`, либо оператор проверки на равенство `==`.

```python
var = None
print(var is None)  # True
print(var == None)  # True
```
> Рекомендуется для сравнения с `None` использовать оператор `is`.

> is сравнивает id объектов, а == сами объекты на равенство.
>Следующий код демонстрирует работу is и ==:
>```python
>lst1 = [1, 2, 3]
>lst2 = [1, 2, 3]
>print(lst1 is lst2, lst1 == lst2)  # False True
>```

<h3 align="center">Сравнение None с другими типами данных</h3>

Сравнение `None` с любым объектом, отличным от `None` дает значение `False`.

```python
print(None == 0)      # False
print(None == "")     # False
print(None == ())     # False
print(None == [])     # False
print(None == False)  # False
```

> Сравнивать `None` с другими типами данных можно только на равенство/неравенство.

```python
print(None > 0)
print(None <= False)
```

приводит к ошибке:

```python
TypeError: '>' not supported between instances of 'NoneType' and 'int' ('bool')
```

## 36.Множества (set) и их методы

**Множество** – структура данных, неупорядоченная коллекция уникальных элементов.

<h4 align="center">Создание множества</h4>

Чтобы создать множество, нужно перечислить его элементы через запятую в фигурных скобках:

```python
info = {'Timur', 1992, 61.5}
```

Элементы множества должны быть хешируемыми объектами, например числами, строками. Элементы изменяемых (нехешируемых) объектов не могут входить в
множества. Требование хешируемости элементов множества накладывается особенностями представления множеств в `Python`:

```python
myset1 = {1, 2, [5, 6], 7}    # множество не может содержать список
myset2 = {1, 2, {5, 6}, 7}    # множество не может содержать множество
```

приводит к ошибке:

```python
TypeError: unhashable type: 'list'
TypeError: unhashable type: 'set'
```

Однако приведенный ниже код:

```python
myset = {1, 2, (5, 6), 7}    # множество может содержать кортеж
```

работает как полагается.

> Однако, если кортеж внутри себя будет содержать изменяемые(нехешируемые) типы данных, то он не может быть элементом множества:
>```python
>myset = {1, 2, (2, [3, 4])}
>```
>```python
>TypeError: unhashable type: 'list'
>```

<h4 align="center">Пустое множество</h4>

Создать пустое множество можно с помощью встроенной функции, которая называется `set()`:

```python
st = set()
```

Cоздать пустое множество с помощью пустых фигурных скобок нельзя:

```python
dct = {}
```

С помощью пустых фигурных скобок создаются словари.

<h4 align="center">Вывод множества</h4>

Для вывода всего множества можно использовать функцию `print()`:

```python
st = {1, 4, "d", False, 4.5}
print(st)  # {False, 1, 4.5, 4, 'd'}
```

> При выводе функцией `print` вывод может отличаться, так как множества неупорядоченные коллекции.

<h4 align="center">Встроенная функция set()</h4>

В функцию `set()` можно передать один аргумент. Передаваемый аргумент должен быть итерируемым объектом, например список, кортеж или строковое значение.
Отдельные элементы объекта, передаваемого в качестве аргумента, становятся элементами множества:

```python
myset1 = set(range(10))          # множество из элементов последовательности
myset2 = set([1, 2, 3, 4, 5])    # множество из элементов списка
myset3 = set('abcd')             # множество из элементов строки
myset4 = set((10, 20, 30, 40))   # множество из элементов кортежа
```

Пустое множество также можно создать передав функции `set()` в качестве аргумента пустой список, строку или кортеж:

```python
emptyset1 = set([])         # пустое множество из пустого списка
emptyset2 = set('')         # пустое множество из пустой строки
emptyset3 = set(())         # пустое множество из пустого кортежа
```

<h4 align="center">Дубликаты при создании множеств</h4>

Множества не могут содержать повторяющиеся элементы. Если в функцию `set()` передать аргумент, содержащий повторяющиеся элементы, то в множестве появится только
один из этих повторяющихся элементов:

```python
myset1 = {2, 2, 4, 6, 6}
myset2 = set([1, 2, 2, 3, 3])
myset3 = set('aaaaabbbbccccddd')

print(myset1)  # {2, 4, 6}
print(myset2)  # {1, 2, 3}
print(myset3)  # {'b', 'c', 'd', 'a'}
```

<h4 align="center">Функция len()</h4>

Длиной множества называется количество его элементов. Чтобы посчитать длину множества используют встроенную функцию `len()`:

```python
myset1 = {2, 2, 4, 6, 6}
myset2 = set([1, 2, 2, 3, 3, 4, 4, 5, 5])
myset3 = set('aaaaabbbbccccddd')

print(len(myset1))  # 3
print(len(myset2))  # 5
print(len(myset3))  # 4
```

<h4 align="center">Оператор принадлежности in</h4>

Оператор `in` позволяет проверить, содержит ли множество некоторый элемент:

```python
st = {1, 4, 5, 7, 2}
print(2 in st)  # True
print(7 not in st)  # False
```

> Оператор принадлежности `in` работает очень быстро на множествах. 

<h4 align="center">Встроенные функции sum(), min(), max()</h4>

Встроенная функция `sum()` может принимать в качестве аргумента множество чисел и вычисляет сумму его элементов:

```python
numbers = {2, 2, 4, 6, 6}
print(sum(numbers))  # 12
```

Встроенные функции `min()` и `max()` могут принимать в качестве аргумента множество и находят минимальный и максимальный элементы соответственно:

```python
numbers = {2, 2, 4, 6, 6}
print(min(numbers))  # 2
print(max(numbers))  # 6
```

> Индексация и срезы недоступны для множеств.

> Операция конкатенации `+` и умножения на число `*` недоступны для множеств.

<h3 align="center">Перебор элементов множества</h3>

Для вывода элементов множества каждого на отдельной строке можно использовать следующий код:

```python
numbers = {0, 1, 1, 2, 3, 3, 3, 5, 6, 7, 7}

for num in numbers:
    print(num)
```    
    
Такой код выведет (порядок элементов может отличаться):

```
0
1
2
3
5
6
7
```

Можно использовать операцию **распаковки множества**:

```python
numbers = {0, 1, 1, 2, 3, 3, 3, 5, 6, 7, 7}

print(*numbers, sep='\n')
```

выводит (порядок элементов может отличаться):

```
0
1
2
3
5
6
7
```

Если нужно гарантировать порядок вывода элементов (по возрастанию / убыванию), то необходимо воспользоваться встроенной функцией `sorted()`:

```python
numbers = {0, 1, 1, 2, 3, 3, 3, 5, 6, 7, 7}

sorted_numbers = sorted(numbers)
print(*sorted_numbers, sep='\n')
```

будет гарантированно выводить элементы множества в порядке возрастания.

<h3 align="center">Сравнение множеств</h3>

Множества можно сравнивать между собой. Равные множества имеют одинаковую длину и содержат равные элементы. Для сравнения множеств используются операторы `==` и `!=`:

```python
myset1 = {1, 2, 3, 3, 3, 3}
myset2 = {2, 1, 3}
myset3 = {1, 2, 3, 4}

print(myset1 == myset2)  # True
print(myset1 == myset3)  # False
print(myset1 != myset3)  # True
```

<h3 align="center">Добавление элементов</h3>

<h4 align="center">Метод add()</h4>

Для добавления нового элемента в множество используется метод `add()`.

Следующий программный код:

```python
numbers = {1, 1, 2, 3, 5, 8, 3}  # создаем множество

numbers.add(21)  # добавляем число 21 в множество
numbers.add(34)  # добавляем число 34 в множество

print(numbers)
```

выводит (порядок элементов может отличаться):

```
{1, 2, 3, 34, 5, 8, 21}
```

Если требуется внести несколько значений в множество, то можно воспользоваться циклом `for`:

```python
numbers = set()  # создаем пустое множество

for i in range(10):
    numbers.add(i*i + 1)

print(numbers)
```

выводит (порядок элементов может отличаться):

```
{1, 2, 65, 5, 37, 10, 17, 50, 82, 26}
```

<h3 align="center">Удаление элемента</h3>

Для удаления элементов из множества используются методы:

 - `remove()`;
 - `discard()`;
 - `pop()`.
 
<h4 align="center">Метод remove()</h4>

Метод `remove()` — удаляет элемент из множества с генерацией исключения (ошибки) в случае, если такого элемента нет.

```python
numbers = {1, 2, 3, 4, 5}

numbers.remove(3)
print(numbers)
```

выводит (порядок элементов может отличаться):

```
{1, 2, 4, 5}
```

Следующий программный код:

```python
numbers = {1, 2, 3, 4, 5}

numbers.remove(10)
print(numbers)
```

приводит к возникновению ошибки `KeyError`, так как элемент 10 отсутствует в множестве.

<h4 align="center">Метод discard()</h4>

Метод `discard()` — удаляет элемент из множества без генерации исключения (ошибки), если элемент отсутствует.

```python
numbers = {1, 2, 3, 4, 5}

numbers.discard(3)
print(numbers)
```

выводит (порядок элементов может отличаться):

```
{1, 2, 4, 5}
```

Следующий программный код:

```python
numbers = {1, 2, 3, 4, 5}

numbers.discard(10)
print(numbers)
```

не приводит к возникновению ошибки и выводит (порядок элементов может отличаться):

```
{1, 2, 3, 4, 5}
```

<h4 align="center">Метод pop()</h4>

Метод `pop()` — удаляет и возвращает случайный элемент из множества с генерацией исключения (ошибки) при попытке удаления из пустого множества.

```python
numbers = {1, 2, 3, 4, 5}

print('до удаления:', numbers)
num = numbers.pop()                 # удаляет случайный элемент множества, возвращая его
print('удалённый элемент:', num)
print('после удаления:', numbers)
```

Результат работы такого кода случаен, например, такой код может вывести:

```python
до удаления: {1, 2, 3, 4, 5}
удалённый элемент: 1
после удаления: {2, 3, 4, 5}
```

<h4 align="center">Метод clear()</h4>

Метод `clear()` удаляет все элементы из множества:

```python
numbers = {1, 2, 3, 4, 5}
numbers.clear()

print(numbers)  # set()
```

## Задания

1. Напишите программу, которая выводит все цифры, встречающиеся в символьной строке больше одного раза.

```python
lst_numbers = [int(c) for c in input() if c.isdigit()]
repeats_set = set()
st = set()
for el in lst_numbers:
    if el not in st:
        st.add(el)
    else:
        repeats_set.add(el)
print(*sorted(repeats_set) or ["NO"])
```
2. Напишите программу, которая удаляет из строки все повторяющиеся символы, при этом регистр букв необходимо учитывать.

```python
a = input()
s = set()
for i in range(len(a)):
    if a[i] in s:
        a = " " + a[:i] + a[i + 1:]
    s.add(a[i])
print(a.lstrip())
```

```python
# 2 способ
a = input()
b = set(a)
for i in a:
    if i in b:
        print(i, end='')
        b.remove(i)
```

3. Пользователь с клавиатуры вводит названия городов, пока не введет букву q. Определить общее уникальное число городов, 
которые вводил пользователь. На экран вывести это число. Из коллекций при реализации программы использовать только 
множества.

```python
s = set()
city = input()
while city != "q":
    s.add(city)
    city = input()
print(len(s))
```

## 37.Операции над множествами. Сравнение множеств

Основные операции над множествами:
 
- объединение множеств;
- пересечение множеств;
- разность множеств;
- симметрическая разность множеств.

<h4 align="center">Объединение множеств: метод union()</h4>

**Объединение множеств** - это множество, состоящее из элементов, принадлежащих хотя бы одному из объединяемых множеств. 

Для этой операции существует метод `union()`.

![image](https://user-images.githubusercontent.com/124737857/231516141-8ed4e7db-5951-425b-858d-bf14001f6df4.png)

Приведенный ниже код:

```python
myset1 = {1, 2, 3, 4, 5}
myset2 = {3, 4, 6, 7, 8}

myset3 = myset1.union(myset2)
print(myset3)
```

выводит (порядок элементов может отличаться):

```
{1, 2, 3, 4, 5, 6, 7, 8}
```

Для объединения двух множеств можно также использовать оператор `|`.

Результат выполнения приведенного ниже кода:

```python
myset1 = {1, 2, 3, 4, 5}
myset2 = {3, 4, 6, 7, 8}

myset3 = myset1 | myset2
print(myset3)
```

аналогичен предыдущему.

> Метод `union()` возвращает новое множество в которое входят все элементы множеств `myset1` и `myset2`

<h4 align="center">Пересечение множеств: метод intersection()</h4>

**Пересечение** множеств - это множество, состоящее из элементов, принадлежащих одновременно каждому из пересекающихся множеств. 

Для этой операции существует метод `intersection()`.

![image](https://user-images.githubusercontent.com/124737857/231517238-902a8fe2-a33c-4e12-bbdc-aa7d8382ddb4.png)

```python
myset1 = {1, 2, 3, 4, 5}
myset2 = {3, 4, 6, 7, 8}

myset3 = myset1.intersection(myset2)
print(myset3)
```

выводит (порядок элементов может отличаться):

```
{3, 4}
```

Для пересечения двух множеств можно также использовать оператор `&`.

Результат выполнения приведенного ниже кода:

```python
myset1 = {1, 2, 3, 4, 5}
myset2 = {3, 4, 6, 7, 8}

myset3 = myset1 & myset2
print(myset3)
```

аналогичен предыдущему.

> Метод `intersection()` возвращает новое множество в которое входят общие элементы множеств `myset1` и `myset2`.

<h4 align="center">Разность множеств: метод difference()</h4>

**Разность** множеств это множество, в которое входят все элементы первого множества, не входящие во второе множество. 

Для этой операции существует метод `difference()`.

![image](https://user-images.githubusercontent.com/124737857/231517316-482b2f2f-f595-4d98-864f-02967cb60b5d.png)

```python
myset1 = {1, 2, 3, 4, 5}
myset2 = {3, 4, 6, 7, 8}

myset3 = myset1.difference(myset2)
print(myset3)
```

выводит (порядок элементов может отличаться):

```
{1, 2, 5}
```

Для разности двух множеств можно также использовать оператор `-`.

Результат выполнения приведенного ниже кода:

```python
myset1 = {1, 2, 3, 4, 5}
myset2 = {3, 4, 6, 7, 8}

myset3 = myset1 - myset2
print(myset3)
```

аналогичен предыдущему.

> Для операции разности множеств важен порядок, в котором указаны множества.


<h4 align="center">Симметрическая разность: метод symmetric_difference()</h4>

**Симметрическая разность** множеств - это множество, включающее все элементы исходных множеств, не принадлежащие одновременно обоим исходным множествам.

Для этой операции существует метод `symmetric_difference()`.

![image](https://user-images.githubusercontent.com/124737857/231517700-33ce2820-6d11-4f6d-af88-56c6af89ff33.png)

```python
myset1 = {1, 2, 3, 4, 5}
myset2 = {3, 4, 6, 7, 8}

myset3 = myset1.symmetric_difference(myset2)
print(myset3)
```

выводит (порядок элементов может отличаться):

```
{1, 2, 5, 6, 7, 8}
```

Для симметрической разности двух множеств можно также использовать оператор `^`.

Результат выполнения приведенного ниже кода:

```python
myset1 = {1, 2, 3, 4, 5}
myset2 = {3, 4, 6, 7, 8}

myset3 = myset1 ^ myset2
print(myset3)
```

аналогичен предыдущему.

<h3 align="center">Методы множеств, изменяющие текущие множества</h3>

Для таких целей используются парные методы `update()`, `intersection_update()`, `difference_update()`, `symmetric_difference_update()`.

Метод `update()` изменяет исходное множество **по объединению**. Аналогичный результат получается, если использовать оператор `|=`.

Метод `intersection_update()` изменяет исходное множество **по пересечению**. Аналогичный результат получается, если использовать оператор `&=`.

Метод `difference_update()` изменяет исходное множество **по разности**. Аналогичный результат получается, если использовать оператор `-=`.

Метод `symmetric_difference_update()` изменяет исходное множество по **симметрической разности**. Аналогичный результат получается, если использовать оператор `^=`.

> Все основные операции над множествами выполнятся двумя способами: при помощи метода или соответствующего ему оператора. Различие в том, что метод может принимать
>  в качестве аргумента не только множество (тип данных set), но и любой итерируемый объект (например, список, строку, кортеж).
>```python
>mylist = [2021, 2020, 2019, 2018, 2017, 2016]
>mytuple = (2021, 2020, 2016)
>mystr = 'abcd'
>myset = {2009, 2010, 2016}
>print(myset.union(mystr))              # объединяем со строкой
>print(myset.intersection(mylist))      # пересекаем со списком
>print(myset.difference(mytuple))       # находим разность с кортежем
>```
>выводит (порядок элементов может отличаться):
>```
>{2016, 'c', 'b', 'a', 'd', 2009, 2010}
>{2016}
>{2009, 2010}
>```

Приоритет операторов в порядке убывания имеет вид:

![image](https://user-images.githubusercontent.com/124737857/231519161-94cfcc75-2a45-4754-bb85-5e5f4e2525b0.png)

<h3 align="center">Подмножества и надмножества</h3>

Множество `set1` является подмножеством множества `set2`, если все элементы первого входят во второе. При этом множество `set2` – надмножество множества `set1`.

> Любое множество – подмножество самого себя, про такое подмножество говорят `"нестрогое подмножество"`.

<h4 align="center">Метод issubset()</h4>

Для определения, является ли одно из множеств подмножеством другого, используется метод `issubset()`. Данный метод возвращает значение `True`, если одно множество
является подмножеством другого, и `False`, если не является:

```python
set1 = {2, 3}
set2 = {1, 2, 3, 4, 5, 6}

print(set1.issubset(set2))  # True
```

Для определения, является ли одно из множеств подмножеством другого, также применяются операторы `<=` (нестрогое подмножество) и `<` (строгое подмножество).

```python
set1 = {2, 3}
set2 = {1, 2, 3, 4, 5, 6}

print(set1 <= set2)  # True
```

<h4 align="center">Метод issuperset()</h4>

Для определения, является ли одно из множеств надмножеством другого, используется метод `issuperset()`. Данный метод возвращает значение `True`, если одно множество
является надмножеством другого, в противном случае он возвращает `False`:

```python
set1 = {'a', 'b', 'c', 'd', 'e'}
set2 = {'c', 'e'}

print(set1.issuperset(set2))  # True
```

Для определения, является ли одно из множеств надмножеством другого, также применяются операторы `>=` (нестрогое надмножество) и `>` (строгое надмножество).

```python
set1 = {'a', 'b', 'c', 'd', 'e'}
set2 = {'c', 'e'}

print(set1 >= set2)  # True
```

<h4 align="center">Метод isdisjoint()</h4>

Для определения отсутствия общих элементов в множествах используется метод `isdisjoint()`. Данный метод возвращает значение `True`, если множества не имеют общих
элементов, и  `False`, когда множества имеют общие элементы:

```python
set1 = {1, 2, 3, 4, 5}
set2 = {5, 6, 7}
set3 = {7, 8, 9}

print(set1.isdisjoint(set2))  # False
print(set1.isdisjoint(set3))  # True
print(set2.isdisjoint(set3))  # False
```

> Методы `issuperset()`, `issubset()`, `isdisjoint()` могут принимать в качестве аргумента любой итерируемый объект.

## Задания

1. Каждый ученик, обучающийся в онлайн-школе BEEGEEK изучает либо математику, либо информатику, либо оба этих предмета. У 
руководителя школы есть списки учеников, изучающих каждый предмет. Случайно списки всех учеников перемешались. Напишите программу, которая позволит
руководителю выяснить, сколько учеников изучает только один предмет.

**Формат входных данных**

На вход программе в первых двух строках подаются числа m и n – количества учеников, изучающих математику и информатику 
соответственно. Далее идут m+n строк — фамилии учеников, изучающих математику и информатику, в произвольном порядке.

**Формат выходных данных**

Программа должна вывести количество учеников, которые изучают только один предмет. Если таких учеников не окажется, то 
необходимо вывести NO.

Примечание. Гарантируется, что среди учеников школы BEEGEEK нет однофамильцев.

```python
n, m = int(input()), int(input())
st = set()
st2 = set()
for _ in range(n + m):
    student = input()
    if student in st:
        st2.add(student)
    st.add(student)
print(len(st - st2) or "NO")
```

2. Руководителю онлайн-школы BEEGEEK захотелось узнать, кто из его учеников присутствовал на всех уроках с начала учебного года.
Для каждого урока есть листок со списком присутствовавших учеников. Напишите программу, определяющую фамилии учеников, которые присутствовали на всех уроках.

**Формат входных данных**

На вход программе в первой строке дается число m – количество уроков, проведенных с начала учебного года. Далее идёт m блоков
строк, описывающих листки с фамилиями. На первой строке каждого блока указано количество фамилий n_i, затем идёт n_i строчек с
фамилиями тех, кто был на i-ом уроке.

**Формат выходных данных**

Программа должна вывести фамилии учеников, которые были на всех уроках, отсортированных в лексикографическом порядке. Каждая 
фамилия должна быть записана на отдельной строке.

Примечание 1. Гарантируется, что среди учеников школы BEEGEEK нет однофамильцев.

Примечание 2. Гарантируется, что хотя бы один ученик был на всех уроках.

```python
m = int(input())
s = {input() for _ in range(int(input()))}
for _ in range(m - 1):
    s &= {input() for i in range(int(input()))}
print(*sorted(s), sep="\n")
```

3. Урок информатики
Даны по 10-балльной шкале оценки по информатике трех учеников. Напишите программу, которая выводит множество оценок, которые 
есть и у первого и у второго учеников, но которых нет у третьего ученика.

```python
a = set(input().split())
b = set(input().split())
c = set(input().split())
print(*sorted(map(int, (a & b) - c), reverse=True))
```

## 38.Генераторы множеств, frozenset

Пусть требуется создать множество, содержащее цифры введенного числа.

Для создания требуемого множества, содержащего уникальные цифры введенного числа, придется написать код:

```python
digits = set()

for c in input():
    digits.add(int(c))
```

Такой код хоть и не сложен, однако достаточно громоздок.

Для создания множеств в `Python` можно использовать специальный синтаксис, как при создании списка.

Приведенный выше код можно переписать с использованием генератора множеств:

```python
digits = {int(c) for c in input()}
```

Общий вид генератора множеств следующий:

```python
{выражение for переменная in последовательность}
```

где  `выражение` — некоторое выражение, как правило, зависящее от использованной в списочном выражении переменной, `переменная` — имя некоторой переменной,
`последовательность` — последовательность значений, которые она принимает (любой итерируемый объект).

<h4 align="center">Условия в генераторе множеств</h4>

В генераторах множеств можно использовать условный оператор. Например, если требуется создать множество, заполненное только цифрами некоторой строки:

```python
digits = {int(d) for d in 'abcd12ef78ghj90' if d.isdigit()}
```

> По аналогигии с вложенными генераторами списков можно использовать условные тернарные операторы, а также вложенные циклы в генераторах множеств, или другие
> генераторы множеств(получая вложенные конструкции). Так же при необходимости можно комбинировать генераторы списков и множеств(при этом нужно помнить, что
> элементами множеств могут быть только хешируемые объекты)

<h3 align="center">Frozenset</h3>

Замороженное множество (`frozenset`) также является встроенной коллекцией в Python. Обладая характеристиками обычного множества, замороженное множество не может быть
изменено после создания.

Для создания замороженного множества используется встроенная функция `frozenset()`, которая принимает в качестве аргумента любой итерируемый объект:

```python
myset1 = frozenset({1, 2, 3})                         # на основе множества
myset2 = frozenset([1, 1, 2, 3, 4, 4, 4, 5, 6, 6])    # на основе списка
myset3 = frozenset('aabcccddee')                      # на основе строки

print(myset1)  # frozenset({1, 2, 3})
print(myset2)  # frozenset({1, 2, 3, 4, 5, 6})
print(myset3)  # frozenset({'e', 'd', 'c', 'b', 'a'})
```

<h4 align="center">Операции над замороженными множествами</h4>

Над замороженными множествами можно производить операции, которые не изменяют само множество а создают копию:

 - объединение множеств: метод `union()` или оператор `|`;
 - пересечение множеств: метод `intersection()` или оператор `&`;
 - разность множеств: метод `difference()` или оператор `-`;
 - симметрическая разность множеств: метод `symmetric_difference()` или оператор `^`.
 
> Замороженные множества являются неизменяемыми, а значит могут быть элементами других множеств.

Можно сравнивать простые (тип `set`) и замороженные множества (тип `frozenset`):

```python
myset1 = set('qwerty')
myset2 = frozenset('qwerty')

print(myset1 == myset2)  # True
```

## Задания

1. Используя генератор множеств, дополните приведенный код так, чтобы он выбрал из списка files уникальные имена файлов c 
расширением .png, независимо от регистра имен и расширений. Имена файлов вывести вместе с расширением, все на одной строке, 
в нижнем регистре, в алфавитном порядке через пробел.

Примечание. Если бы список files содержал следующие имена файлов:

files = ['python.png', 'qwerty.py', 'Python.PNg', 'apple.pnG', 'zebra.PNG',  'solution.Py', 'stepik.org', 'kotlin.ko', 
'github.git', 'ZeBrA.PnG']
то ответом был бы:

apple.png python.png zebra.png

```python
files = ['python.png', 'qwerty.py', 'stepik.png', 'beegeek.org', 'windows.pnp', 'pen.txt', 'phone.py', 'book.txT', 
         'board.pNg', 'keyBoard.jpg', 'Python.PNg', 'apple.jpeg', 'png.png', 'input.tXt', 'split.pop', 'solution.Py', 
         'stepik.org', 'kotlin.ko', 'github.git']

unique_files = {file.lower() for file in files if file.lower().endswith(".png")}
print(*sorted(unique_files))
```
