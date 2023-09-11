# Mython
## Описание языка
`Mython` - интерпретатор Python-подобного программирования.
Язык является динамически типизированным, поддерживает классы, наследование, условные операторы, операции с целыми числами, печать в поток вывода.
Все методы в классах по умолчанию виртуальные.

## Работа с интерпретатором
Подготовьте файл с корректным кодом на языке `Mython`. 
Запустите исполняемый файл `Mython` (`Mython`.exe в Windows) с двумя параметрами :
<имя входного файла с кодом> , <имя выходного файла для вывода результата>
Если программа синтаксически корректна - в выходной файл будет выведен результат работы программы.
Если в программе есть ошибки - в консоль будет выведена информация об ошибках.

## Классы

```python
class Rect:
  def __init__(w, h):
    self.w = w
    self.h = h

  def area():
    return self.w * self.h
```

## Типизация

Каждая переменная определяется во время исполнения программы и может меняться в ходе её работы. Поэтому вместо «присваивания значения переменной» лучше говорить о «связывании значения с некоторым именем». Как следствие при первом использовании переменной не надо указывать её тип.

```python
x = 4           # переменная x связывается с целочисленным значением 4
x = 'hello'     # следующей командой переменная x связывается со строковым значением 'hello'
y = True
x = y  
```

## Операции
В языке `Mython` определены:

*	арифметические операции для целых чисел (деление выполняется нацело),
*	операция конкатенации строк,
*	операции сравнения строк и целых чисел на «равно/не равно», «больше/меньше», «больше или равно/меньше или равно»; при этом сравнение строк выполняется лексикографически.

## Функция str

Функция str преобразует переданный ей аргумент в строку. Если аргумент является объектом класса, она вызывает у него специальный метод `__str__` и возвращает его результат. Если метода `__str__` в классе нет, она возвращает строковое представление адреса объекта в памяти. Примеры:

*	str('Hello') вернёт строку Hello
*	str(100500) вернёт строку 100500
*	str(False) вернёт строку False
*	str(Rect(3, 4)) вернёт адрес объекта в памяти, например '0x2056fd0'

Теперь добавим в класс Rect метод `__str__`: 

```python
class Rect(Shape):
  def __init__(w, h):
    self.w = w
    self.h = h

  def __str__():
    return "Rect(" + str(self.w) + 'x' + str(self.h) + ')'
    # str(Rect(3, 4)) вернёт строку Rect(3x4). 
```

## Команда print

Специальная команда print принимает набор аргументов, разделённых запятой, печатает их в стандартный вывод и дополнительно выводит перевод строки.
```pyton
x = 4
w = 'world'
print x, x + 6, 'Hello, ' + w
# выведет 4 10 Hello, world
``` 

Обратите внимание, что команда print вставляет пробел между выводимыми значениями. Если в команду print не передать аргументов, она просто выведет перевод строки.
Для преобразования каждого своего аргумента в строку команда print вызывает для него функцию str. Таким образом команда print Rect(20, 15) выведет в stdout строку Rect(20x15).

## Условный оператор

В языке `Mython` есть условный оператор, он имеет следующий синтаксис:
```python
if <условие>:
  <действие 1>
  <действие 2>
  ...
  <действие N>
else:
  <действие 1>
  <действие 2>
  ...
 <действие M>
 ```
<условие> — это произвольное выражение, за которым следует символ двоеточия. Если условие истинно, то выполняются действия под веткой if, если ложно — действия под веткой else. Ветка else может отсутствовать. <условие> может содержать сравнения, а также логические операции and, or и not. Истинность условия определяется в зависимости от типа значения, являющегося результатом его вычисления:

*	если результатом вычисления условия является значение логического типа, то для проверки истинности условия используется именно оно,
*	если результатом вычисления условия является число, то условие истинно тогда и только тогда, когда это число не равно нулю, например,
*	если результатом вычисления условия является строка, то условие истинно тогда и только тогда, когда эта строка имеет ненулевую длину,
*	если результатом вычисления условия является объект класса, то условие истинно,
*	если результатом вычисления условия является None, то условие ложно.

Обратите внимание, что действия в ветках if и else набраны с отступом в два пробела. В языке `Mython` команды объединяются в блоки с помощью отступов. Один отступ равен двум пробелам. Сравните: 
```python
if x > 0:
  x = x + 1
print x

if x > 0:
  x = x + 1
  print x
```
Первая команда print x будет выполняться всегда, вторая — только если x > 0.

## Наследование

В языке `Mython` у класса может быть один родительский класс. Если он есть, он указывается в скобках после имени класса и до символа двоеточия. В примере ниже класс Rect наследуется от класса Shape
```python
class Shape:
  def __str__():
    return "Shape"

  def area():
    return 'Not implemented'

class Rect(Shape):
  def __init__(w, h):
    self.w = w
    self.h = h

  def __str__():
    return "Rect(" + str(self.w) + 'x' + str(self.h) + ')'

  def area():
    return self.w * self.h
```
Наследование в `Mython` все методы родительского класса становятся доступны классу-потомку. При этом все методы являются публичными и виртуальными. Например, код ниже выведет ```Hello, John```: 
```python
class Greeting:
  def greet():
    return "Hello, " + self.name()

  def name():
    return 'Noname'

class HelloJohn(Greeting):
  def name():
    return 'John'

greet_john = HelloJohn()
print greet_john.greet()
```

## Методы
Как вы могли видеть выше, методы в `Mython` имеют синтаксис:
```python
def <имя метода>(<список параметров>):
  <действие 1>
  <действие 2>
  ...
  <действие N>
```
Команда ``` return ``` завершает выполнение метода из возвращает из него результат вычисления своего аргумента. Если исполнение метода не достигает команды ``` return ```, метод возращает None.

Семантика присваивания

Как было сказано выше, `Mython` — это язык с динамической типизацией, поэтому операция присваивания имеет семантику не копирования значения в область памяти, а связывания имени переменной со значением. Как следствие, переменные только ссылаются на значения, а не содержат их копии. Говоря терминологией С++, можно сказать, что все переменные в `Mython являются указателями (аналогом ```nullptr``` является значение ```None```).
```python
class Counter:
  def __init__():
    self.value = 0

  def add():
    self.value = self.value + 1

x = Counter()
y = x
x.add()
y.add()
print x.value
#  Выведет 2, так как переменные x и y ссылаются на один и тот же объект. 
```
