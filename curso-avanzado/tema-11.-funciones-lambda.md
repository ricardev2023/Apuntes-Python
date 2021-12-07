---
description: Explicación y conceptos básicos de las Funciones Lambda en Python 3.
---

# Tema 11. Funciones Lambda

## Funciones `lambda`

Son un tipo especial de funciones de `Python` que tienen la sintaxis siguiente

```python
lambda parámetros: expresión
```

* Son útiles para ejecutar funciones en una sola línea
* Pueden tomar cualquier número de argumentos
* Tienen una limitación: solamente pueden contener una expresión

Veamos algunos ejemplos

#### **Ejemplo 1**

Función que dado un número, le suma 10 puntos más:

```python
plus10 = lambda x: x + 10
plus10(5)

#RESPUESTA
15
```

#### **Ejemplo 2**

Función que calcula el producto de dos números:

```python
prod = lambda x, y: x * y
prod(5, 10)

#RESPUESTA
50
```

#### **Ejemplo 3**

Función que dados 3 números, calcula el discriminante de la ecuación de segundo grado.

Recordemos que dada una ecuación de segundo grado de la forma $$ax^2 + bx + c = 0$$

el discriminante es $$\triangle = b^2-4ac$$

y dependiendo de su signo, nos indica cuantas soluciones reales va a tener la ecuación:

* Si **Δ > 0**, entonces hay dos soluciones diferentes.
* Si **Δ = 0**, entonces hay dos soluciones que son iguales.
* Si **Δ < 0**, entonces no hay solución.

```python
discriminante = lambda a, b, c: b ** 2 - 4 * a * c
discriminante(1, 2, 1) # Se corresponde a la ecuación x^2 + 2x + 1 = 0, cuya única solución es x = -1

#RESPUESTA
0
```

#### EJERCICIO 1:&#x20;

Vamos a crear una función lambda que devuelva una tupla donde en la primera posición esté el número introducido por parámetro; en la segunda, su doble; y, en la tercera, su cuadrado.

```python
ejercicio1 = lambda a: (a, a * 2, a ** 2)
ejercicio1(2)

#RESPUESTA
(2, 4, 4)
```

### La función `filter()`

* Aplica una función a todos los elementos de un objeto iterable
* Devuelve un objeto generador, de ahí que usemos la función `list()` para convertirlo a lista
* Como output, devuelve los elementos para los cuales el aplicar la función ha devuelto `True`

Con la ayuda de las funciones `lambda`, apliquemos `filter()` para quedarnos con los números múltiplos de 7 de la siguiente lista llamada `nums`

```python
nums = [49, 57, 62, 147, 2101, 22]
list(filter(lambda x: (x % 7 == 0), nums))

#RESPUESTA
[49, 147]
```

La función proporcionada a `filter()` no tiene por qué ser `lambda`, sino que puede ser una ya existente, o bien una creada por nosotros mismos.

Con las siguientes líneas de código vamos a obtener todas las palabras cuya tercera letra sea `s` haciendo uso de `filter()` y la función creada `third_letter_is_s()`:

```python
def third_letter_is_s(word):
  return word[2] == "s"
```

```python
words = ["castaña", "astronomía", "masa", "bolígrafo", "mando", "tostada"]
list(filter(third_letter_is_s, words))

#RESPUESTA
['castaña', 'masa', 'tostada']
```

**IMPORTANTE** la función que se utilice debe tener un parámetro de entrada que sea el que se utilice para recorrer el bucle. Al utilizar filter, no damos valor a este parámetro ya que se lo dá la propia función filter con el objeto iterable que entra como segundo parámetro a filter.

#### EJERCICIO 2:&#x20;

Dada una lista numérica, vamos a filtrarla y quedarnos con los números positivos. El resultado lo mostraremos en una lista.

```python
nums = [2, -2, 5, -5, 7, -7]
list(filter(lambda x: x > 0, nums))

#RESPUESTA
[2, 5, 7]
```

### La función `reduce()`

* Aplica continuamente una misma función a los elementos de un objeto iterable
  1. Aplica la función a los primeros dos elementos
  2. Aplica la función al resultado del paso anterior y el tercer elemento
  3. Aplica la función al resultado del paso anterior y el cuarto elemento
  4. Sigue así hasta que solo queda un elemento
* Devuelve el valor resultante

Con la ayuda de las funciones `lambda`, apliquemos `reduce()` para calcular el producto de todos los elementos de una lista

```python
from functools import reduce
```

```python
nums = [1, 2, 3, 4, 5, 6]
reduce(lambda x, y: x * y, nums)

#RESPUESTA
720
```

De nuevo, la función proporcionada a `reduce()` no tiene por qué ser `lambda`, sino que puede ser una ya existente o bien, una creada por nosotros mismos.

Con las siguientes líneas de código, vamos a obtener el máximo de una lista dada, haciendo uso de `reduce()` y la función creada `bigger_than()`:

```python
def bigger_than(a, b):
  if a > b:
    return a
  return b
```

```python
bigger_than(14, 7)

#RESPUESTA
14
```

```python
nums = [-10, 5, 7, -3, 16, -30, 2, 33]
reduce(bigger_than, nums)

#RESPUESTA
33
```

#### EJERCICIO 3:&#x20;

Dada una lista de palabras, vamos a quedarnos con la palabra con más "a".

```python
from functools import reduce

def a_comparer(a, b):
    if a.count("a") > b.count("a"):
        return a
    else:
        return b

words = ["albondiga", "espejo", "alama", "antimanifestaciones", "supercalifragilisticoespialidoso", "aaaa", "a"]

reduce(a_comparer, words)

#RESPUESTA
'aaaa'
```

### La función `map()`

* Aplica una misma función a todos los elementos de un objeto iterable
* Devuelve un objeto generador, de ahí que usemos la función `list()` para convertirlo a lista
* Como output, devuelve el resultado de aplicar la función a cada elemento

Con la ayuda de las funciones `lambda`, apliquemos `map()` para calcular las longitudes de las siguientes palabras

```python
words = ["zapato", "amigo", "yoyo", "barco", "xilófono", "césped"]
list(map(lambda w: len(w), words))

#RESPUESTA
[6, 5, 4, 5, 8, 6]
```

Sin embargo, para este caso en concreto no haría falta usar funciones `lambda`, pues podríamos hacer directamente

```python
list(map(len, words))

#RESPUESTA
[6, 5, 4, 5, 8, 6]
```

#### EJERCICIO 4:&#x20;

Vamos a convertir una lista de grados Celsius a grados Fahrenheit. El resultado lo mostraremos como una lista.

```python
degrees = [22.5, 35, -5.2]

list(map(lambda x: x * (9 / 5) + 32, degrees))

#RESPUESTA
[72.5, 95.0, 22.64]
```

### La función `sorted()`

* Ordena los elementos del objeto iterable que indiquemos de acuerdo a la función que pasemos por parámetro
* Como output, devuelve una permutación del objeto iterable ordenado según la función indicada

Con la ayuda de las funciones `lambda`, apliquemos `sorted()` para ordenar la lista `words` en función de las longitudes de las palabras en orden descendente.

```python
words = ["zapato", "amigo", "yoyo", "barco", "xilófono", "césped"]
sorted(words, key = lambda x: len(x), reverse = True)

#RESPUESTA
['xilófono', 'zapato', 'césped', 'amigo', 'barco', 'yoyo']
```

De nuevo, podríamos en este caso evitar el uso de las funciones `lambda` haciendo uso del siguiente código:

```python
sorted(words, key = len, reverse = True)

#RESPUESTA
['xilófono', 'zapato', 'césped', 'amigo', 'barco', 'yoyo']
```

**Observación.** Si quisiésemos ordenar en orden ascendente, simplemente tendríamos que indicar `reverse = False`, que al ser el valor por defecto, bastaría con omitir dicho parámetro.

**Observación.** Si el tipo de objeto a ser ordenado es un string y no indicamos parámetro `key`, entonces se ordenan por defecto: orden alfabético ascendente.

```python
sorted(words, key = len)

#RESPUESTA
['yoyo', 'amigo', 'barco', 'zapato', 'césped', 'xilófono']
```

```python
sorted(words)

#RESPUESTA
['amigo', 'barco', 'césped', 'xilófono', 'yoyo', 'zapato']
```

#### EJERCICIO 5:&#x20;

Vamos a ordenar una lista de palabras por el número de apariciones de la letra indicada por el usuario. El orden será descendente.

```python
words = ["zapato", "amigo", "yoyo", "barco", "xilófono", "césped"]
letter = input("Introduzca una letra: ")

sorted(words, key = lambda x: x.count(letter), reverse = True)
```

```
#RESPUESTA
Introduzca una letra: a
['zapato', 'amigo', 'barco', 'yoyo', 'xilófono', 'césped']
```

## REPASO

```python
#EJERCICIO 1: Crea una función lambda que dado un número entero multiplique por su anterior y su siguiente. Por ejemplo,
#si proporcionamos n = 3, nos tendrá que devolver 2 · 3 · 4 = 24.

ejercicio1 = lambda n: (n - 1) * n * (n + 1)
ejercicio1(3)

#RESPUESTA
24
```

```python
#EJERCICIO 2: Crea una función lambda que dados dos números devuelva si el primero es mayor.

ejercicio2 = lambda a, b: a > b
ejercicio2(3, 2)

#RESPUESTA
True
```

```python
#EJERCICIO 3: Dada una lista de palabras, quédate con filter() con las que tengan más vocales que consonantes. 
# Necesitarás una función que devuelva si una palabra tiene más vocales que consonantes

def more_vocals(word):
    """
    Función que indica si la palabra tiene 
    más vocales que consonantes.

    Args:
        word (str): palabra a comprobar.
    Return:
        True si tiene más vocales que cons.
        False si tiene más consonantes.
    """
    vowels = 0
    cons = 0

    for i in word.lower():
        if i == "a" or i == "e"  or i == "i" or i == "o" or i == "u":
            vowels += 1
        elif i == " " or i == "1" or i == "2" or i == "3" or i == "4" or i == "5" or i == "6" or i == "7" or i == "8" or i == "9" or i == "0":
            continue
        else:
            cons += 1

    if vowels > cons:
        return True
    else:
        return False

words = ["playa", "alijo", "macarron"]
list(filter(more_vocals, words))

#RESPUESTA
['alijo']
```

```python
#EJERCICIO 4: Dada una lista de números enteros, quédate con filter() con los que tengan más de 5 divisores. 
#Necesitarás una función que devuelva el número de divisores de un número dado.

def divisors(x):
    """
    Función que cuenta cuantos divisores
    tiene un número

    Args:
        x (int): Numero entero positivo
    Return:
        counter (int): contador de divisores.
    """
    counter = 0
    for divisor in range(1, x + 1):
        if x % divisor == 0:
            counter += 1
    return counter

nums = [1994, 234, 56, 8999, 567]
list(filter(lambda num: divisors(num) > 5, nums))

#RESPUESTA
[234, 56, 567]
```

```python
#EJERCICIO 5: Dada una lista de palabras, quédate con reduce() con la palabra más larga. Necesitarás una función que
#compare dos palabras y devuelva la que tenga mayor longitud.

from functools import reduce

def larger_word(a, b):
    """
    Función que devuelve la palabra más larga.

    Args:
        a (str): palabra 1
        b (str): palabra 2
    Return:
        a o b en función de cual sea más larga.
    """

    if len(a) > len(b):
        return a
    else:
        return b #Si son iguales devuelve la nueva palabra

words = ["zapato", "amigo", "yoyo", "barco", "xilófono", "césped"]
reduce(larger_word, words)

#RESPUESTA
'xilófono'
```

```python
#EJERCICIO 6: Dada una lista de palabras, calcula el número de vocales de cada una con map().

def vowel_counter(word):
    """
    Función que cuenta vocales.

    Args:
        word (string)
    Return:
        counter (int)
    """
    counter = 0
    for i in word:
         if i == "a" or i == "e"  or i == "i" or i == "o" or i == "u":
             counter += 1
    return counter

words = ["zapato", "amigo", "yoyo", "barco", "xilófono", "césped"]
list(map(vowel_counter, words))

#RESPUESTA
[3, 3, 2, 2, 3, 1]
```

```python
#EJERCICIO 7: Dada una lista de palabras, quédate con reduce() y map() con la palabra con más consonantes. Necesitarás
# una función que cuente el número de consonantes de una palabra y otra que dados dos números, devuelva el
# mayor.

from functools import reduce

def cons_counter(word):
    """
    Función que cuenta consonantes.

    Args:
        word (string)
    Return:
        counter (int)
    """
    counter = 0
    for i in word:
        if i == "a" or i == "e"  or i == "i" or i == "o" or i == "u" or i == " " or i == "1" or i == "2" or i == "3" or i == "4" or i == "5" or i == "6" or i == "7" or i == "8" or i == "9" or i == "0":
            continue
        else:
            counter += 1
    return counter

def larger(x, y):
    """
    Función que devuelve el número más grande.

    Args:
        x (int): resultado de cons_counter
        y (int): resultado de cons_counter
    
    Return:
        x o y en función de cual es más grande.
    """
    if x > y:
        return x
    else:
        return y

words = ["zapato", "amigo", "yoyo", "barco", "xilófono", "céspedes"]
#Buscamos el elemento de words que cumple:
#en la lista de cuantas consonantes buscamos el index del elemento con más consonantes.
words[list(map(cons_counter, words)).index(reduce(larger, list(map(cons_counter, words))))]

#RESPUESTA
'céspedd'
```

```python
#EJERCICIO 8: Dada una lista de números enteros, calcula el número anterior con map().

nums = [1994, 234, 56, 8999, 567]
list(map(lambda num: num - 1, nums))

#RESPUESTA
[1993, 233, 55, 8998, 566]
```

```python
#EJERCICIO 9: Dada una lista de números reales, ordénalos con sorted() por valor absoluto de menor a mayor.

nums = [1994, 234, 56, 8999, 567, -79012, -925, -57]

sorted(nums, key = lambda num: abs(num), reverse = False)

#RESPUESTA
[56, -57, 234, 567, -925, 1994, 8999, -79012]
```

```python
#EJERCICIO 10: Dada una lista de palabras, ordénalos con sorted() por número de consonates de mayor a menor.

def cons_counter(word):
    """
    Función que cuenta consonantes.

    Args:
        word (string)
    Return:
        counter (int)
    """
    counter = 0
    for i in word:
        if i == "a" or i == "e"  or i == "i" or i == "o" or i == "u" or i == " " or i == "1" or i == "2" or i == "3" or i == "4" or i == "5" or i == "6" or i == "7" or i == "8" or i == "9" or i == "0":
            continue
        else:
            counter += 1
    return counter

words = ["zapato", "amigo", "yoyo", "barco", "xilófono", "césped"]
sorted(words, key = cons_counter, reverse = True)

#RESPUESTA
['xilófono', 'césped', 'zapato', 'barco', 'amigo', 'yoyo']
```
