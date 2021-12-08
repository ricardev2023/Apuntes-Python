---
description: >-
  Explicación de como controlar los errores y excepciones derivados del uso de
  nuestros scripts en Python 3.
---

# Tema 15. Errores y Excepciones

A lo largo de este tema vamos a aprender sobre los diferentes tipos de errores y excepciones que existen en `Python`. Tanto los errores como las excepciones saltan cuando el intérprete de `Python` encuentra algún error.

Es completamente normal cometer ciertos errores mientras se escribe un programa. Estos fallos conducen a errores cuando tratamos de ejecutar dicho programa. La ejecución termina al instante de encontrar alguno de esos fallos, que pueden ser de dos tipos:

1. **Error de sintaxis**
2. **Excepción (error de lógica)**

## Errores de sintaxis

**Error de sintaxis.** Ocurre cuando no se sigue la sintaxis correcta del lenguaje.

Un error de sintaxis ocurre cuando nos dejamos un paréntesis sin cerrar, los dos puntos tras la condición de un operador de decisión o iteración...

```python
a = 2
if (a > 3 : 
    print(a)
```

```
  File "<ipython-input-1-539906e83b82>", line 2
    if (a > 3 :
              ^
SyntaxError: invalid syntax
```

Como podemos observar, ha saltado un error de sintaxis, `SintaxError`, debido a que nos hemos olvidado del paréntesis de cierre. Además, el propio error nos indica a qué es debido y dónde tenemos que modificar el código para corregir el fallo.

## Excepciones

**Excepción.** Una vez superado el test de sintaxis, si la ejecución del programa es interrumpida, entonces estamos ante una excepción o error de lógica.

Una excepción puede deberse a intentar llamar a una variable que no ha sido declarada (`NameError`), intentar abrir un archivo que no se encuentra en la dirección indicada (`FileNotFoundError`), intentar dividir un número entre cero (`ZeroDivisionError`)... Siempre que se da alguna de estas situaciones, `Python` crea un objeto excepción. Si no es manejado correctamente, imprime un rastreo del error junto a algunos detalles sobre qué ha causado dicho error.

```python
a = 2
if (b > 3) : 
    print(b)
```

```
---------------------------------------------------------------------------

NameError                                 Traceback (most recent call last)

<ipython-input-2-85a72f55ae65> in <module>()
      1 a = 2
----> 2 if (b > 3) :
      3     print(b)


NameError: name 'b' is not defined
```

Como podemos observar, ha saltado una excepción, `NameError`, debido a que nos hemos llamado a una variable que no existe. Además, el propio error nos indica a qué es debido y dónde tenemos que modificar el código para corregir el fallo.

### Excepciones de `Python`

Existen múltiples excepciones en `Python` que se nos muestran cuando se dan los errores correspondientes. Podemos mostrar por pantalla todas las excepciones de `Python` usando la función `locals()` tal y como se muestra a continuación

```python
for i in dir(locals()['__builtins__']):
  print(i)
```

```
ArithmeticError
AssertionError
AttributeError
BaseException
BlockingIOError
BrokenPipeError
BufferError
BytesWarning
ChildProcessError
ConnectionAbortedError
ConnectionError
ConnectionRefusedError
ConnectionResetError
DeprecationWarning
EOFError
Ellipsis
EnvironmentError
Exception
False
FileExistsError
FileNotFoundError
FloatingPointError
FutureWarning
GeneratorExit
IOError
ImportError
ImportWarning
IndentationError
IndexError
InterruptedError
IsADirectoryError
KeyError
KeyboardInterrupt
LookupError
MemoryError
ModuleNotFoundError
NameError
None
NotADirectoryError
NotImplemented
NotImplementedError
OSError
OverflowError
PendingDeprecationWarning
PermissionError
ProcessLookupError
RecursionError
ReferenceError
ResourceWarning
RuntimeError
RuntimeWarning
StopAsyncIteration
StopIteration
SyntaxError
SyntaxWarning
SystemError
SystemExit
TabError
TimeoutError
True
TypeError
UnboundLocalError
UnicodeDecodeError
UnicodeEncodeError
UnicodeError
UnicodeTranslateError
UnicodeWarning
UserWarning
ValueError
Warning
ZeroDivisionError
__IPYTHON__
__build_class__
__debug__
__doc__
__import__
__loader__
__name__
__package__
__spec__
abs
all
any
ascii
bin
bool
bytearray
bytes
callable
chr
classmethod
compile
complex
copyright
credits
delattr
dict
dir
display
divmod
dreload
enumerate
eval
exec
filter
float
format
frozenset
get_ipython
getattr
globals
hasattr
hash
help
hex
id
input
int
isinstance
issubclass
iter
len
license
list
locals
map
max
memoryview
min
next
object
oct
open
ord
pow
print
property
range
repr
reversed
round
set
setattr
slice
sorted
staticmethod
str
sum
super
tuple
type
vars
zip
```

`locals["__builtins__"]` nos devuelve el módulo con las excepciones, funciones y atributos de `Python`. La función `dir()` nos permite listar todos esos elementos como strings.

Algunas de las excepciones de `Python` más comunes al programar son:

|       Excepción       | Causa                                                                                     |
| :-------------------: | ----------------------------------------------------------------------------------------- |
|   `ArithmeticError`   | Cuando falla una operación numérica                                                       |
|    `AssertionError`   | Cuando falla una declaración `assert`                                                     |
|    `AtributeError`    | Cuando falla una asignación de atributo o referencia                                      |
|       `EOFError`      | Cuando la función `input()` llega a la condición fin de archivo (end-of-file)             |
|  `FloatingPointError` | Cuando falla una operación en coma flotante                                               |
|     `ImportError`     | Cuando un módulo importando no es encontrado                                              |
|   `IndentationError`  | Cuando la indentación no es correcta                                                      |
|      `IndexError`     | Cuando el índice de una secuencia se sale del rango                                       |
|       `KeyError`      | Cuando una clave de un diccionario no es encontrada                                       |
|  `KeyboardInterrupt`  | Cuando el usuario pulsa la tecla de interrupción                                          |
|     `LookupError`     | Cuando el elemento no puede ser encontrado                                                |
|     `MemoryError`     | Cuando una operación se queda sin memoria                                                 |
|      `NameError`      | Cuando se llama a una variable que no se encuentra a nivel global ni local                |
| `NotImplementedError` | Cuando un método abstracto requiere de una clase heredada para sobreescribir el método    |
|    `OverflowError`    | Cuando el resultado de una operación aritmética es demasiado grande para ser representado |
|     `RuntimeError`    | Cuando un error no entra dentro de ninguna categoría                                      |
|       `TabError`      | Cuando la indentación consiste de tabulaciones y espacios en blanco inconsistentes        |
|      `TypeError`      | Cuando a una función u operación se le suministra un objeto de tipo incorrecto            |
|      `ValueError`     | Cuando una función obtiene un argumento del tipo correcto pero de valor incorrecto        |
|  `ZeroDivisionError`  | Cuando el divisor de una división es 0                                                    |

## Manejo de excepciones

Como programadores, necesitamos ser lo más específicos posible. Esto implica ser conscientes de los errores que podrían ocurrir. Por suerte, `Python` permite a los programadores tratar con errores de forma eficiente.

Podemos manejar excepciones usando 5 sentencias:

1. `try / except`
2. `try / finally`
3. `assert`
4. `raise`
5. `with / as`

### **1. `try / except`**

* El bloque `try` permite comprobar si hay errores de código.
* El bloque `except` permite manejar el error.

En el siguiente chunk, en caso de que ocurra el error, imprimimos un mensaje por pantalla:

```python
a, b = 5, 0

try:
  print(a / b)
except ZeroDivisionError:
  print("¡Has querido dividir entre 0!")
```

```
¡Has querido dividir entre 0!
```

En el siguiente chunk, en caso de que ocurra el error, imprimimos el mensaje de la excepción correspondiente por pantalla:

```python
a, b = 5, 0

try:
  print(a / b)
except ZeroDivisionError as message:
  print(message)
```

```
division by zero
```

Sin `try /except`, hubiéramos obtenido

```python
a, b = 5, 0
print(a / b)
```

```
---------------------------------------------------------------------------

ZeroDivisionError                         Traceback (most recent call last)

<ipython-input-11-ed3c7da87ae8> in <module>()
      1 a, b = 5, 0
----> 2 print(a / b)


ZeroDivisionError: division by zero
```

Podríamos poner más de un bloque `except`

```python
a, b = "a", 0

try:
  print(a / b)
except ZeroDivisionError:
  print("¡Has querido dividir entre 0!")
except:
  print("Algo más ha salido mal")
```

```
Algo más ha salido mal
```

En el chunk anterior hemos intentado dividir un string entre 0. Por tanto, la execpción ya no se debe a intentar dividir entre 0, sino a otro motivo: que un string no puede ser el dividendo de la división.

También podemos combinar `try / except` con `else`:

```python
a, b = 5, 2

try:
  print(a / b)
except ZeroDivisionError:
  print("¡Has querido dividir entre 0!")
else:
  print("Nada ha salido mal")
```

```
2.5
Nada ha salido mal
```

El bloque `else` se ejecutará siempre y cuando no haya excepciones, junto al bloque `try`, tal cual ocurre en el ejemplo anterior.

### **2. `try / finally`**

* El bloque `try` permite comprobar si hay errores de código.
* El bloque `finally` permite ejecutar el código a pesar del resultado de los bloques `try` y `except`.

```python
a, b = 5, 0

try:
  print(a / b)
except:
  print("Algo ha salido mal")
finally:
  print("El proceso try / except ha finalizado")
```

```
Algo ha salido mal
El proceso try / except ha finalizado
```

```python
a, b = 5, 2

try:
  print(a / b)
except:
  print("Algo ha salido mal")
finally:
  print("El proceso try / except ha finalizado")
```

```
2.5
El proceso try / except ha finalizado
```

Sea cual sea el caso, el bloque `finally` siempre se ejecuta.

El bloque `finally` puede ser útil para cerrar objetos y limpiar recursos.

### **3. `assert`**

La palabra reservada `assert` se utiliza para debuguear el código. Nos permite comprobar si una condición en nuestro código devuelve `True`. De lo contrario, el programa nos devolverá un `AssertionError`

```python
x = "Hola"

# Si la condición devuelve True, no ocurre nada
assert x == "Hola"
```

```python
# Si la condición devuelve False, salta un AssertionError
assert x == "Adiós"
```

```
---------------------------------------------------------------------------

AssertionError                            Traceback (most recent call last)

<ipython-input-19-7c43999c077d> in <module>()
      1 # Si la condición devuelve False, salta un AssertionError
----> 2 assert x == "Adiós"


AssertionError: 
```

En el caso de que la condición devuelva `False`, podríamos indicar un mensaje del siguiente modo:

```python
# Si la condición devuelve False, salta un AssertionError
assert x == "Adiós", "x debería de contener 'Hola'"
```

```
---------------------------------------------------------------------------

AssertionError                            Traceback (most recent call last)

<ipython-input-20-c080a268a731> in <module>()
      1 # Si la condición devuelve False, salta un AssertionError
----> 2 assert x == "Adiós", "x debería de contener 'Hola'"


AssertionError: x debería de contener 'Hola'
```

```python
import math
x = 7.5
assert x > 0, "El valor de x debe ser positivo para calcular un logaritmo"
math.log(x)
```

```
2.0149030205422647
```

### **4. `raise`**

Como programadores, podemos elegir cuando mostrar una excepción dada una condición. Para mostrar excepciones, usamos la palabra reservada `raise`

```python
radius = -7
if radius < 0:
  raise Exception("El radio no puede tomar valores menores a 0")
```

```
---------------------------------------------------------------------------

Exception                                 Traceback (most recent call last)

<ipython-input-26-cc0e3501a0d7> in <module>()
      1 radius = -7
      2 if radius < 0:
----> 3   raise Exception("El radio no puede tomar valores menores a 0")


Exception: El radio no puede tomar valores menores a 0
```

En el chunk anterior hemos usado `raise` para mostrar una excepción. No obstante, podemos elegir qué tipo de excepción mostrar y el texto que imprimir al usuario:

```python
radius = "-5"

if not type(radius) is int and not type(radius) is float:
  raise TypeError("El radio debe ser de tipo numérico (int o float)")
elif radius < 0:
  raise Exception("El radio no puede tomar valores menores a 0")
```

```
---------------------------------------------------------------------------

TypeError                                 Traceback (most recent call last)

<ipython-input-48-98967b628ed7> in <module>()
      2 
      3 if not type(radius) is int and not type(radius) is float:
----> 4   raise TypeError("El radio debe ser de tipo numérico (int o float)")
      5 elif radius < 0:
      6   raise Exception("El radio no puede tomar valores menores a 0")


TypeError: El radio debe ser de tipo numérico (int o float)
```

### **5. `with / as`**

La palabra reservada `with` se utiliza para manejar excepciones y conseguir así un código más limpio y legible. Simplifica el manejo de recursos comunes tales como flujos de archivos.

En el siguiente chunk no utilizamos la palabra reservada `with`

```python
file = open("path_del_archivo", "w")
try: 
    file.write("¡Hola, caracola!") 
finally: 
    file.close() 
```

Mientras que en el siguiente sí que utilizamos `with / as` y observamos que el código queda mucho más limpio y legible.

```python
with open("path_del_archivo", "w") as file: 
    file.write("¡Hola, caracola!") 
```

Ambos chunks de código darían el mismo resultado. No obstante, el segundo tiene menos líneas de código, pues entre otras cosas no le hace falta la línea `file.close()`, tal cual vimos en el tema anterior.

La palabra reservada `with` se asegura la adquisición y liberación adecuadas de recursos.

## REPASO

#### Ejercicio 1

Dada la función divisors(), asegura con assert que el parámetro n se trata de un número entero positivo. De lo contrario, muestra como mensaje que "n debe ser de tipo int y debe ser mayor que 0"

```python
def divisors(n):
    """
    Calcula los divisores de un número entero positivo.
    Args:
    n: Número entero positivo
    Returns:
    divisors: Lista de divisores de n
    """
    assert type(n) == int and n > 0, "n debe ser de tipo int y debe ser mayor que 0" 
    divisors = []
    for i in range(1, n + 1):
        if n % i == 0: divisors.append(i)
    return divisors
```

#### Ejercicio 2

Dada la función divisors(), muestra TypeError con el mensaje correspondiente si el parámetro n no se trata de un número entero y muestra ValueError con el mensaje correspondiente si n no se trata de un número positivo.

```python
def divisors(n):
    """
    Calcula los divisores de un número entero positivo.
    Args:
    n: Número entero positivo
    Returns:
    divisors: Lista de divisores de n
    """
    if type(n) != int:
        raise TypeError("n debe ser de tipo int")
    if n <= 0:
        raise ValueError("n debe ser mayor que 0")
    divisors = []
    for i in range(1, n + 1):
        if n % i == 0: divisors.append(i)
    return divisors
```

#### Ejercicio 3

Dada la función is\_palindrome(), asegura con assert que el parámetro word se trata de una variable de tipo string. De lo contrario, muestra como mensaje que "word debe ser de tipo string".

```python
def is_palindrome(word):
    """
    Devuelve si la palabra word es palíndroma.
    Args:
        word: Palabra
    Returns:
        isPalindrome: Booleano
    """
    assert type(word) == str, "word debe ser de tipo string"
    word = word.lower()
    l = []
    isPalindrome = True
    for c in word:
        l.append(c)
    n = len(l)
    for i in range(int(n / 2)):
        if l[i] != l[n - (i + 1)]: isPalindrome = False
    return isPalindrome
```

#### Ejercicio 4

Dada la función is\_palindrome(), muestra TypeError con el mensaje correspondiente si word no se trata de una variable de tipo string.

```python
def is_palindrome(word):
    """
    Devuelve si la palabra word es palíndroma.
    Args:
        word: Palabra
    Returns:
        isPalindrome: Booleano
    """
    if type(word) != str:
        raise TypeError("word debe ser de tipo string")
    word = word.lower()
    l = []
    isPalindrome = True
    for c in word:
        l.append(c)
    n = len(l)
    for i in range(int(n / 2)):
        if l[i] != l[n - (i + 1)]: isPalindrome = False
    return isPalindrome
```

#### Ejercicio 5

Dada la función is\_palindrome(), muestra ValueError con el mensaje correspondiente si word no se trata de una palabra. Es decir, si una vez ha pasado la comprobación de ser una variable de tipo string, comprueba que no tiene espacios.

```python
def is_palindrome(word):
    """
    Devuelve si la palabra word es palíndroma.
    Args:
        word: Palabra
    Returns:
        isPalindrome: Booleano
    """
    if type(word) != str:
        raise TypeError("word debe ser de tipo string")
    for i in word:
        if i == " ":
            raise ValueError("word no puede tener espacios.")
    word = word.lower()
    l = []
    isPalindrome = True
    for c in word:
        l.append(c)
    n = len(l)
    for i in range(int(n / 2)):
        if l[i] != l[n - (i + 1)]: isPalindrome = False
    return isPalindrome
```

#### Ejercicio 6

Dada la función is\_palindrome() del resultado del ejercicio anterior, modifícala de modo que acepte no solo palabras sino también frases y devuelva si el string introducido es palíndromo o no. Recuerda tener en cuenta la excepción TypeError junto al mensaje correspondiente.

```python
def is_palindrome(sentence):
    """
    Devuelve si la palabra word es palíndroma.
    Args:
        word: Palabra
    Returns:
        isPalindrome: Booleano
    """
    if type(word) != str:
        raise TypeError("word debe ser de tipo string")
        
    sentence = sentence.lower()
    if sentence == sentence[::-1]:
        return True
    else:
        return False
```

#### Ejercicio 7

Utiliza try / except para dado un objeto de Python guardado en la variable x, aplicarle el método .index() y localizar el elemento "c". En el bloque try, guarda el resultado en la variable result. En el bloque except, en la variable result, si el objeto x es una lista, guarda el mensaje "La lista no tiene el elemento "c". En caso contario, guarda el mensaje "El objeto {tipo del objeto que sea x} no tiene el método .index()". Finalmente, imprime por pantalla el resultado.

```python
def search_list(x, c):

    try:
        result = x[x.index(c)]
    except:
        if type(x) == list:
           print("La lista no tiene el elemento 'c'")
        
        else:
            print("El objeto {} no tiene método .index()".format(type(x)))
```

#### Ejercicio 8

Crea una función que calcule el área de un cuadrado. Como parámetro se recibirá un número real, correspondiente a la longitud de la base. Lanza las excepciones pertinentes siempre que el parámetro no se trate de un número real o entero positivo.

```python
def square_area(l):
    if type(l) != int and type(l) != float:
        raise TypeError("El lado debe ser un número entero o real.")
    if l <= 0:
        raise ValueError("El lado no puede ser negativo o cero.")
    
    return l * l
```

#### Ejercicio 9

Crea una función que solicite al usuario la edad. Lanza una excepción en caso de que no se trate de una edad válida. Se considera edad no válida una edad negativa o mayor a 150. En cada caso, lanza el mensaje correspondiente.

```python
def correct_age():
    age = 0
    try:
        age = int(input("Introduzca su edad: "))
    except ValueError:
        raise ValueError("Su edad debe ser un número entero")
    if age <= 0 or age > 150:
        raise ValueError("Su edad no está comprendida entre las edades permitidas.")  
```

#### Ejercicio 10

Crea una función que solicite al usuario una letra en mayúscula. Lanza una excepción en caso de que el usuario no haya introducido nada, no haya introducido una letra, no haya introducido una letra mayúscula o no haya introducido solamente un caracter.

```python
def mayus_1():
    a = input("Introduzca una letra mayuscula: ")
    if a == "" or a in [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] or len(a) > 1 or a.isupper() == False:
        raise ValueError("Lo que ha introducido no es una letra mayuscula, vuelva a intenarlo.")
```

```python
mayus_1()
```

```
Introduzca una letra mayuscula: A
```
