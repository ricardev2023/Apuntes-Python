---
description: Explicación del uso de estructuras de datos tipo tuplas en Python 3.
---

# Tema 9. Estructura de Datos. Tuplas

## Tupla

La última estructura que veremos son las tuplas. Éstas son un conjunto de elementos, que pueden ser de distintos tipos, separados por comas y escritos entre paréntesis, `()`.

Las tuplas son:

* **hetereogéneas**: los elementos pueden ser de distinto tipo en una misma tupla
* **no mutables**: los elementos no pueden ser modificados una vez la tupla ha sido creado

Un ejemplo de tupla sería:

```python
t = ("Juan", 32, "profesor", True)
print(t)

#RESPUESTA
('Juan', 32, 'profesor', True)
```

Podemos declarar una tupla sin necesidad indicar sus elementos entre paréntesis

```python
t = "Juan", 32, "profesor", True
type(t)

#RESPUESTA
tuple
```

Podemos declarar tuplas con la función `tuple()`

```python
t = tuple(("Juan", 32, "profesor", True))
type(t)

#RESPUESTA
tuple
```

```python
tuple([1,2,3])

#RESPUESTA
(1, 2, 3)
```

#### EJERCICIO 1:&#x20;

Vamos a pedirle al usuario el número de números enteros que va a introducir por teclado. Para cada uno de esos números, vamos a crear una tupla donde la primera entrada sea el número entero y, la segunda, la palabra "positivo", "negativo" o "cero" según el signo del número entero. Vamos a guardar todas las tuplas en una lista y las vamos a mostrar.

```python
n = int(input("¿Cuántos números enteros vas a introducir? "))
nums = []

for _ in range(n):
  sign = ""
  num = int(input())
  if num > 0:
    sign = "positivo"
  elif num == 0:
    sign = "cero"
  else:
    sign = "negativo"
  nums.append((num, sign))

print(nums)
```

#### EJERCICIO 2:&#x20;

Vamos a pedirle al usuario números enteros del 1 al 10 hasta que introduzca el 0. Para cada uno de esos números, vamos a crear una tupla donde la primera entrada sea el número entero y, la segunda, la palabra "suspenso", "aprobado", "notable" o "excelente" según el intervalo al que pertenezca el número entero. Vamos a mostrar la tupla recién creada al usuario.

Las diferentes categorías son:

suspenso si la nota pertenece a \[1, 5) aprobado si la nota pertenece a \[5, 7) notable si la nota pertenece a \[7, 9) excelente si la nota pertenece a \[9, 10]

```python
nota = 1000

while nota != 0:
    nota = int(input("Introduzca una nota numérica: "))
    if nota < 1:
        print("Nota fuera de rango")
    elif nota >= 1 and nota < 5:
        tupla = (nota, "suspenso")
        print(tupla)
    elif nota >= 5 and nota < 7:
        tupla = (nota, "aprobado")
        print(tupla) 
    elif nota >= 7 and nota < 9:
        tupla = (nota, "notable")
        print(tupla) 
    elif nota >= 9 and nota <= 10:
        tupla = (nota, "excelente")
        print(tupla)
    else:
        print("Nota fuera de rango")
```

```
#RESPUESTA
Introduzca una nota numérica: 1
(1, 'suspenso')
Introduzca una nota numérica: 0
Nota fuera de rango
```

#### EJERCICIO 3:&#x20;

Dada una frase introducida por el usuario, vamos a crear una lista con 3 tuplas de 2 entradas. La primera tupla contendrá el número de vocales; la segunda, el número de consonantes; y la última, el número de espacios en blanco. Para cada tupla, la primera entrada será un string explicativo y, la segunda, el valor correspondiente.

```python
s = str(input("Introduzca una frase: "))
s = s.lower()

vocales = 0
consonantes = 0
espacios = 0

for i in s:
    if i == "a" or i == "e" or i == "i" or i == "o" or i == "u":
        vocales += 1
    elif i == " ":
        espacios += 1
    else:
        consonantes += 1

l = [
     ("Número de vocales", vocales), 
     ("Número de consonantes", consonantes), 
     ("Número de espacios", espacios)
     ]

print(l)
type(l[0])
```

```
#RESPUESTA
Introduzca una frase: sdfg
[('Número de vocales', 0), ('Número de consonantes', 4), ('Número de espacios', 0)]

tuple
```

### Elementos de una tupla

Podemos acceder a los elementos de una tupla mediante el índice que ocupan con la sintaxis de claudator, `[]`

```python
t = 1, "a", 2, "e", 3, "i", 4, "o", 5, "u"
print(t[0])
print(t[5])

#RESPUESTA
1
i
```

Al igual que con las listas, podemos acceder a los elementos de tuplas mediante el uso de índices negativos

```python
print(t[-1])
print(t[-4])

#RESPUESTA
u
4
```

Para acceder a múltiples entradas de una tupla a la vez, podemos utilizar la función `:` para indicar un intervalo de índices.

```python
print(t[2:6])
print(t[:5])
print(t[5:])
```

```
#RESPUESTA
(2, 'e', 3, 'i')
(1, 'a', 2, 'e', 3)
('i', 4, 'o', 5, 'u')
```

**Observación.** Recordad que

* el índice indicado tras los dos puntos, `:`, nunca es incluido.
* si no se indica índice a la izquierda de `:`, se considera desde el índice 0 hasta el inmediatamente anterior al indicado a la derecha de `:`
* si no se indica índice a la derecha de `:`, se considera desde el índice indicado a la izquierda de `:` hasta el último elemento

También podemos usar índices negativos con la función `:`

```python
print(t[-5:-1])

#RESPUESTA
('i', 4, 'o', 5)
```

Para saber si un elemento pertenece a una tupla, podemos usar la palabra clave `in`

```python
print(6 in t)
print("i" in t)

#RESPUESTA
False
True
```

Hemos dicho que las tuplas son inmutables. Esto es, una vez creada la tupla, sus elementos no pueden ser modificados

```python
t = "Cereza", "Manzana", "Pera"
t[1] = "Kiwi"

#RESPUESTA
TypeError: 'tuple' object does not support item assignment
```

**Una alternativa sería convertir a lista, realizar la modificación y reconvertir a tupla**

```python
t = "Cereza", "Manzana", "Pera"
t = list(t)
t[1] = "Kiwi"
t = tuple(t)

print(t)
print(type(t))

#RESPUESTA
('Cereza', 'Kiwi', 'Pera')
<class 'tuple'>
```

#### EJERCICIO 4:&#x20;

Vamos a pedirle al usuario una asignatura ("Mates", "Lengua", "Historia", "Informática" o "Música") y la nota en dicha asignatura hasta que introduzca una asignatura diferente a las indicadas. El usuario puede repetir una asignatura tantas veces como quiera. La nota tendrá que ser del 1 al 10. Guardaremos la información (asignatura, nota) en una tupla. Las tuplas serán guardadas en una lista. Finalmente, para cada asignatura, vamos a mostrar la nota media.

```python
asignaturas = ["Mates", "Lengua", "Historia", "Informática" o "Música"]
l = []

n = str(input("Introduzca una asignatura de las siguientes (Mates, Lengua, Historia, Informática o Música): "))
while n in asignaturas:
    nota = int(input("Introduzca la nota del 1 al 10: "))
    l.append((n, nota))
    n = str(input("Introduzca una asignatura de las siguientes (Mates, Lengua, Historia, Informática o Música): "))

means = {"Mates": [],
         "Lengua": [],
         "Historia": [],
         "Informática": [],
         "Música": []}

for item in grades:
  means[item[0]].append(item[1])

print("\n=== NOTAS MEDIAS ===")
for key, val in means.items():
  print("La nota media de {} es {}".format(key, "desconocida" if len(val) == 0 else sum(val) / len(val)))
```

### El método de unpacking

Podemos extraer los valores de una tupla en variables. Este proceso es conocido como **unpacking.**

```python
fruits = "Cereza", "Kiwi", "Pera", "Naranja"
print(type(fruits))

# Con paréntesis
(fruit1, fruit2, fruit3, fruit4) = fruits

print(fruit1)
print(fruit2)
print(fruit3)
print(fruit4)
```

```
#RESPUESTA
<class 'tuple'>
Cereza
Kiwi
Pera
Naranja
```

Funciona igual si no declaramos las variables entre paréntesis.

```python
fruits = "Cereza", "Kiwi", "Pera", "Naranja"
print(type(fruits))

# Sin paréntesis
fruit1, fruit2, fruit3, fruit4 = fruits

print(fruit1)
print(fruit2)
print(fruit3)
print(fruit4)
```

```
#RESPUESTA
<class 'tuple'>
Cereza
Kiwi
Pera
Naranja
```

**¡Cuidado!** El número de variables debe coincidir con el número de elementos de la tupla. De lo contrario, debe usarse un asterisco para guardar los elementos restantes en una lista.

```python
fruits = "Cereza", "Kiwi", "Pera", "Naranja"

(fruit1, fruit2, *restFruits) = fruits

print(fruit1)
print(fruit2)
print(restFruits)
print(type(restFruits))
```

```
#RESPUESTA
Cereza
Kiwi
['Pera', 'Naranja']
<class 'list'>
```

**Observación.** Si el asterisco es añadido en alguna variable que no sea la última, `Python` almacenará tantos elementos en la lista como sea necesario para que el número de elementos restantes coincida con el número de variables restantes.

```python
fruits = "Cereza", "Kiwi", "Pera", "Naranja", "Melocotón", "Sandía", "Melón"

(fruit1, *restFruits, fruit2, fruit3) = fruits

print(fruit1)
print(restFruits)
print(fruit2)
print(fruit3)
```

```
#RESPUESTA
Cereza
['Kiwi', 'Pera', 'Naranja', 'Melocotón']
Sandía
Melón
```

**Podemos utilizar una barra baja en el caso de que no queramos que nos devuelva un dato.**

```python
punto = (1, 2, 3)
x, _, z = punto
print(x + z)

#RESPUESTA
4
```

```python
fruits = "Cereza", "Kiwi", "Pera", "Naranja", "Melocotón", "Sandía", "Melón"

(fruit1, *_, fruit2, fruit3) = fruits

print(fruit1)
print(fruit2)
print(fruit3)
```

```
#RESPUESTA
Cereza
Sandía
Melón
```

#### EJERCICIO 5:

&#x20;Vamos a pedirle al usuario el número de puntos de un plano que quiere introducir. Para cada punto, vamos a solicitarle las coordenadas x e y. Guardaremos las coordenadas (x, y) en tuplas de tamaño 3, donde la última entrada se corresponde con el cuadrante al que pertenece dicho punto. Todas las tuplas de tamaño 3 serán guardadas en una lista. Finalmente, mostraremos todas las tuplas de tamaño 3 creadas, con el formato "El punto ({x}, {y}) pertenece al cuadrante {cuadrante}"

```python
num = int(input("Introduzca el número de puntos que quiere introducir: "))

l = []

for i in range(num):
    x = int(input("Introduzca la coordenada X del punto {}: ".format(i + 1)))
    y = int(input("Introduzca la coordenada Y del punto {}: ".format(i + 1)))
    if x > 0 and y > 0:
        cuadrante = "cuadrante 1"
    elif x < 0 and y > 0:
        cuadrante = "cuadrante 2"
    elif x < 0 and y < 0:
        cuadrante = "cuadrante 3"
    elif x > 0 and y < 0:
        cuadrante = "cuadrante 4"
    else:
        cuadrante = "cero"
    
    l.append((x, y, cuadrante))

for item in l:
    print("El punto ({}, {}) pertenece al {}".format(item[0], item[1], item[2]))
```

```
#RESPUESTA
Introduzca el número de puntos que quiere introducir: 5
Introduzca la coordenada X del punto 1: 0
Introduzca la coordenada Y del punto 1: 0
Introduzca la coordenada X del punto 2: 1
Introduzca la coordenada Y del punto 2: 1
Introduzca la coordenada X del punto 3: -1
Introduzca la coordenada Y del punto 3: 1
Introduzca la coordenada X del punto 4: -1
Introduzca la coordenada Y del punto 4: -1
Introduzca la coordenada X del punto 5: 1
Introduzca la coordenada Y del punto 5: -1
El punto (0, 0) pertenece al cero
El punto (1, 1) pertenece al cuadrante 1
El punto (-1, 1) pertenece al cuadrante 2
El punto (-1, -1) pertenece al cuadrante 3
El punto (1, -1) pertenece al cuadrante 4
```

### Concatenación de tuplas

Podemos concatenar tuplas con la función `+`, aunque el resultado será una nueva tupla, ya que recordemos éstas no pueden ser modificadas

```python
t1 = 1, 3
t2 = 2, 4

t1 + t2

#RESPUESTA
(1, 3, 2, 4)
```

### Repetición de tuplas

Podemos repetir tuplas un número $n$ de veces con la función `*`

```python
t = ("a", "b", "c")
t * 5

#RESPUESTA
('a', 'b', 'c', 'a', 'b', 'c', 'a', 'b', 'c', 'a', 'b', 'c', 'a', 'b', 'c')
```

### Tamaño de una tupla

Podemos calcular el número de elementos de una tupla con la función `len()`

```python
t = "Juan", 32, "profesor", True
len(t)

#RESPUESTA
4
```

**¡Cuidado!** Si quisiésemos crear una tupla de un solo elemento, tendríamos que hacer lo siguiente

```python
t1 = ("manzana", )
print(type(t1))

# Lo siguiente no es una tupla
t2 = ("manzana")
print(type(t2))

#RESPUESTA
<class 'tuple'>
<class 'str'>
```

## Bucles y tuplas

Podemos iterar una tupla utilizando un bucle `for`

```python
fruits = "Cereza", "Kiwi", "Pera", "Naranja", "Melocotón", "Sandía", "Melón"

for fruit in fruits:
  print(fruit)
```

```
#RESPUESTA
Cereza
Kiwi
Pera
Naranja
Melocotón
Sandía
Melón
```

También podemos usar la técnica de unpacking en los bucles

```python
t = ("cereza", "roja"), ("kiwi", "amarillo"), ("pera", "verde"), ("naranja", "naranja")

for fruit, color in t:
  if fruit == "kiwi":
    print("El color del", fruit, "es", color)
  else:
    print("La {} es {}".format(fruit, color))
  
```

```
#RESPUESTA
La cereza es roja
El color del kiwi es amarillo
La pera es verde
La naranja es naranja
```

## Tuplas y el resto de estructuras de datos

Una tupla puede contener listas, diccionarios, conjuntos y tuplas

```python
t = [4, 5, 6], {"vowels": ("a", "e", "i", "o", "u")}, {1, 2, 3}, ("x", "y")
type(t)

#RESPUESTA
tuple
```

Asimismo,

* las listas pueden contener diccionarios, conjuntos, tuplas y otras listas
* los diccionarios pueden contener listas, conjuntos, tuplas y otros diccionarios
* los conjuntos no pueden contener ni listas, ni diccionarios, ni tuplas, ni siquiera otros conjuntos

```python
l = [{"vowels": ("a", "e", "i", "o", "u")}, {1, 2, 3}, ("x", "y"), [4, 5, 6]]
type(l)

#RESPUESTA
list
```

```python
dicc = {"list": [4, 5, 6], "set": {1, 2, 3}, "tuple": ("x", "y"), "dict": {"vowels": ("a", "e", "i", "o", "u")}}
type(dicc)

#RESPUESTA
dict
```

```python
set1 = {[4, 5, 6], {"vowels": ("a", "e", "i", "o", "u")}, ("x", "y"), {1, 2, 3}}

#RESPUESTA
TypeError: unhashable type: 'list'
```

Dado cualquier objeto iterable en `Python`, lo podemos convertir a tupla con la función `tuple()`

```python
print(tuple(l)) # A partir de una lista
print(type(tuple(l)))

print(tuple(dicc)) # A partir de un diccionario solo se guardan las claves en la tupla
print(type(tuple(dicc)))

print(tuple({1, 2, 3, 4, 5})) # A partir de un conjunto
print(type(tuple({1, 2, 3, 4, 5})))
```

```
#RESPUESTA
({'vowels': ('a', 'e', 'i', 'o', 'u')}, {1, 2, 3}, ('x', 'y'), [4, 5, 6])
<class 'tuple'>
('list', 'set', 'tuple', 'dict')
<class 'tuple'>
(1, 2, 3, 4, 5)
<class 'tuple'>
```

### La función `zip()`

La función `zip()` sirve para juntar listas en tuplas

```python
objects = ["libreta", "pluma", "portaminas", "pack_minas"]
price = [5.00, 3.30, 1.29, 0.50]
items = zip(objects, price)
print(items)

#RESPUESTA
<zip object at 0x7f3782cff6c8>
```

Podemos convertir el resultado de una función `zip()` a una lista

```python
items = zip(objects, price)
list(items)

#RESPUESTA
[('libreta', 5.0), ('pluma', 3.3), ('portaminas', 1.29), ('pack_minas', 0.5)]
```

Podemos convertir el resultado de una función `zip()` a un diccionario

```python
items = zip(objects, price)
dict(items)

#RESPUESTA
{'libreta': 5.0, 'pack_minas': 0.5, 'pluma': 3.3, 'portaminas': 1.29}
```

**¡Cuidado!** Hay que crear de nuevo el objeto `zip()`, pues el resultado de esta función es un iterador y, una vez ha sido convertido a lista, diccionario o tupla, se considera una iteración completa y no será capaz de generar más valores.

Podemos convertir el resultado de una función `zip()` a una tupla:

```python
items = zip(objects, price)
tuple(items)

#RESPUESTA
(('libreta', 5.0), ('pluma', 3.3), ('portaminas', 1.29), ('pack_minas', 0.5))
```

```python
for obj, pr in zip(objects, price):
    print("El objeto {} cuesta {} €.".format(obj, pr))
```

```
#RESPUESTA
El objeto libreta cuesta 5.0 €.
El objeto pluma cuesta 3.3 €.
El objeto portaminas cuesta 1.29 €.
El objeto pack_minas cuesta 0.5 €.
```

#### EJERCICIO 6:&#x20;

Dada una lista de palabras, vamos a crear otra lista del mismo tamaño que guarde la primera letra de cada palabra en la posición correspondiente. Por último, con la función zip() crearemos una tupla de tuplas con la palabra en la primera entrada y la letra con la que empieza, en la segunda.

```python
words = ["ola", "caracola", "piña", "playa", "barbacoa", "ventana", "mosca"]
first_letter = []

for item in words:
    first_letter.append(item[0])

print(tuple(zip(words, first_letter)))
```

```
(('ola', 'o'), ('caracola', 'c'), ('piña', 'p'), ('playa', 'p'), ('barbacoa', 'b'), ('ventana', 'v'), ('mosca', 'm'))
```

## REPASO

```python
#EJERCICIO 1:Pide al usuario el número de números enteros que va a introducir por teclado. Para cada uno de esos
#números, crea una tupla donde la primera entrada sea el número entero y, la segunda, la palabra “par” o
#“impar” según la paridad del número entero. Muestra la tupla recién creada al usuario.

num = int(input("Introduzca la cantidad de números enteros que va a analizar: "))
if num < 0:
    print("El número no puede ser negativo") 
else:
    for _ in range(num):
        n = int(input("Introduzca el número: "))
        if n % 2 == 0:
            par = "par"
        else:
            par = "impar"
        print((n, par))
```

```
#RESPUESTA
Introduzca la cantidad de números enteros que va a analizar: 3
Introduzca el número: 1
(1, 'impar')
Introduzca el número: 2
(2, 'par')
Introduzca el número: 5
(5, 'impar')
```

```python
#EJERCICIO 2: Dado un año proporcionado por el usuario, crea una tupla de dos elementos cuya primera entrada sea el año
#y, la segunda entrada, el horóscopo chino correspondiente.

year = int(input("Introduzca un año: "))


if year % 12 == 0:
    animal = "Mono"
elif year % 12 == 1:
    animal = "Pollo"
elif year % 12 == 2:
    animal = "Perro"
elif year % 12 == 3:
    animal = "Cerdo"
elif year % 12 == 4:
    animal = "Rata"
elif year % 12 == 5:
    animal = "Buey"
elif year % 12 == 6:
    animal = "Tigre"
elif year % 12 == 7:
    animal = "Conejo"
elif year % 12 == 8:
    animal = "Dragón"
elif year % 12 == 9:
    animal = "Serpiente"
elif year % 12 == 10:
    animal = "Caballo"
else:
    animal = "Oveja"

mitupla = (year, animal)
print("El año {}, es según el horoscopo chino, el año del {}.".format(mitupla[0], mitupla[1]))
```

```
#RESPUESTA
Introduzca un año: 1925
El año 1925, es según el horoscopo chino, el año del Buey.
```

```python
#EJERCICIO 3: Dada una frase proporcionada por el usuario, crea una lista de tuplas indicando palabra, longitud de cada
#palabra, letra inicial y posición que ocupan dentro de la frase

s = str(input("Introduzca una frase: "))

l = []
s = s.split()

for word in s:
    info = (word, len(word), word[0], s.index(word) + 1)
    l.append(info)

print(l)
```

```
#RESPUESTA
Introduzca una frase: Hola que ase
[('Hola', 4, 'H', 1), ('ase', 3, 'a', 2)]
```

```python
#EJERCICIO 4: Haz que el usuario introduzca palabras hasta que introduzca una palabra vacía. Guarda todas las palabras
#en una tupla y muestra la primera y la última introducidas haciendo uso del método unpacking.
#PISTA: Para guardar los elementos de uno en uno vas a tener que utilizar un tipo de dato que no es tupla y luego transformarlo a tupla.

item = "a"
l = []

while item != "":
    item = str(input("Introduzca una palabra. Para terminar, pulse enter: "))
    l.append(item)

palabras = tuple(l)
inicio, *_, final, en_blancom = palabras

print(inicio, final)
```

```
#RESPUESTA
Introduzca una palabra. Para terminar, pulse enter: Hola
Introduzca una palabra. Para terminar, pulse enter: caracola
Introduzca una palabra. Para terminar, pulse enter: eres
Introduzca una palabra. Para terminar, pulse enter: una
Introduzca una palabra. Para terminar, pulse enter: maricona
Introduzca una palabra. Para terminar, pulse enter: 
Hola maricona
```

```python
#EJERCICIO 5: Dada una lista de palabras, crea otra lista del mismo tamaño que guarde la longitud de cada palabra. Usa
#la función zip() para crear un diccionario con claves las palabras y valores, su longitud.

words = ["Hola", "caracola", "como", "te", "encuentras"]
lon = []

for item in words:
    lon.append(len(item))

completo = dict(zip(words, lon))
```

```
#RESPUESTA
{'Hola': 4, 'caracola': 8, 'como': 4, 'te': 2, 'encuentras': 10}
```

```python
#EJERCICIO 6: Haz que el usuario introduzca palabras hasta que introduzca una palabra vacía. Guarda todas las palabras
#en una tupla y muestra la tupla y el número total de caracteres que ha introducido.
#PISTA: Para guardar los elementos de uno en uno vas a tener que utilizar un tipo de dato que no es tupla y luego transformarlo a tupla.

item = "a"
l = []
char = 0

while item != "":
    item = str(input("Introduzca una palabra. Para terminar, pulse enter: "))
    if item != "":
        l.append(item)

for word in l:
    char += len(word)

print(tuple(l), char)
```

```
#RESPUESTA
Introduzca una palabra. Para terminar, pulse enter: ok
Introduzca una palabra. Para terminar, pulse enter: ok
Introduzca una palabra. Para terminar, pulse enter: ok
Introduzca una palabra. Para terminar, pulse enter: ok
Introduzca una palabra. Para terminar, pulse enter: k
Introduzca una palabra. Para terminar, pulse enter: 
('ok', 'ok', 'ok', 'ok', 'k') 9
```

```python
#EJERCICIO 7: Crea una lista de 20 tuplas de tamaño 2. La primera entrada será un número entero entre 1 y 20 y la segunda
#entrada contendrá una lista con los 10 primeros múltiplos del número entero correspondiente. Por último,
#muestra las tablas de multiplicar del 1 al 20 con el formato “1 x 1 = 1”

l = []
for i in range(1, 21):
    mult = []
    for c in range(11):
        mult.append(i * c)
    l.append((i, mult))

print(l)
for x, y in dict(l).items():
    print("+++TABLA DEL {}+++".format(x))
    for z in range(11):
        print("{} x {} = {}".format(x, z, y[z]))
```

```
#RESPUESTA
[(1, [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]), (2, [0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20]), (3, [0, 3, 6, 9, 12, 15, 18, 21, 24, 27, 30]), (4, [0, 4, 8, 12, 16, 20, 24, 28, 32, 36, 40]), (5, [0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50]), (6, [0, 6, 12, 18, 24, 30, 36, 42, 48, 54, 60]), (7, [0, 7, 14, 21, 28, 35, 42, 49, 56, 63, 70]), (8, [0, 8, 16, 24, 32, 40, 48, 56, 64, 72, 80]), (9, [0, 9, 18, 27, 36, 45, 54, 63, 72, 81, 90]), (10, [0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100]), (11, [0, 11, 22, 33, 44, 55, 66, 77, 88, 99, 110]), (12, [0, 12, 24, 36, 48, 60, 72, 84, 96, 108, 120]), (13, [0, 13, 26, 39, 52, 65, 78, 91, 104, 117, 130]), (14, [0, 14, 28, 42, 56, 70, 84, 98, 112, 126, 140]), (15, [0, 15, 30, 45, 60, 75, 90, 105, 120, 135, 150]), (16, [0, 16, 32, 48, 64, 80, 96, 112, 128, 144, 160]), (17, [0, 17, 34, 51, 68, 85, 102, 119, 136, 153, 170]), (18, [0, 18, 36, 54, 72, 90, 108, 126, 144, 162, 180]), (19, [0, 19, 38, 57, 76, 95, 114, 133, 152, 171, 190]), (20, [0, 20, 40, 60, 80, 100, 120, 140, 160, 180, 200])]
+++TABLA DEL 1+++
1 x 0 = 0
1 x 1 = 1
1 x 2 = 2
1 x 3 = 3
1 x 4 = 4
1 x 5 = 5
1 x 6 = 6
1 x 7 = 7
1 x 8 = 8
1 x 9 = 9
1 x 10 = 10
+++TABLA DEL 2+++
2 x 0 = 0
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6
2 x 4 = 8
2 x 5 = 10
2 x 6 = 12
2 x 7 = 14
2 x 8 = 16
2 x 9 = 18
2 x 10 = 20
+++TABLA DEL 3+++
3 x 0 = 0
3 x 1 = 3
3 x 2 = 6
3 x 3 = 9
3 x 4 = 12
3 x 5 = 15
3 x 6 = 18
3 x 7 = 21
3 x 8 = 24
3 x 9 = 27
3 x 10 = 30
+++TABLA DEL 4+++
4 x 0 = 0
4 x 1 = 4
4 x 2 = 8
4 x 3 = 12
4 x 4 = 16
4 x 5 = 20
4 x 6 = 24
4 x 7 = 28
4 x 8 = 32
4 x 9 = 36
4 x 10 = 40
+++TABLA DEL 5+++
5 x 0 = 0
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
5 x 4 = 20
5 x 5 = 25
5 x 6 = 30
5 x 7 = 35
5 x 8 = 40
5 x 9 = 45
5 x 10 = 50
+++TABLA DEL 6+++
6 x 0 = 0
6 x 1 = 6
6 x 2 = 12
6 x 3 = 18
6 x 4 = 24
6 x 5 = 30
6 x 6 = 36
6 x 7 = 42
6 x 8 = 48
6 x 9 = 54
6 x 10 = 60
+++TABLA DEL 7+++
7 x 0 = 0
7 x 1 = 7
7 x 2 = 14
7 x 3 = 21
7 x 4 = 28
7 x 5 = 35
7 x 6 = 42
7 x 7 = 49
7 x 8 = 56
7 x 9 = 63
7 x 10 = 70
+++TABLA DEL 8+++
8 x 0 = 0
8 x 1 = 8
8 x 2 = 16
8 x 3 = 24
8 x 4 = 32
8 x 5 = 40
8 x 6 = 48
8 x 7 = 56
8 x 8 = 64
8 x 9 = 72
8 x 10 = 80
+++TABLA DEL 9+++
9 x 0 = 0
9 x 1 = 9
9 x 2 = 18
9 x 3 = 27
9 x 4 = 36
9 x 5 = 45
9 x 6 = 54
9 x 7 = 63
9 x 8 = 72
9 x 9 = 81
9 x 10 = 90
+++TABLA DEL 10+++
10 x 0 = 0
10 x 1 = 10
10 x 2 = 20
10 x 3 = 30
10 x 4 = 40
10 x 5 = 50
10 x 6 = 60
10 x 7 = 70
10 x 8 = 80
10 x 9 = 90
10 x 10 = 100
+++TABLA DEL 11+++
11 x 0 = 0
11 x 1 = 11
11 x 2 = 22
11 x 3 = 33
11 x 4 = 44
11 x 5 = 55
11 x 6 = 66
11 x 7 = 77
11 x 8 = 88
11 x 9 = 99
11 x 10 = 110
+++TABLA DEL 12+++
12 x 0 = 0
12 x 1 = 12
12 x 2 = 24
12 x 3 = 36
12 x 4 = 48
12 x 5 = 60
12 x 6 = 72
12 x 7 = 84
12 x 8 = 96
12 x 9 = 108
12 x 10 = 120
+++TABLA DEL 13+++
13 x 0 = 0
13 x 1 = 13
13 x 2 = 26
13 x 3 = 39
13 x 4 = 52
13 x 5 = 65
13 x 6 = 78
13 x 7 = 91
13 x 8 = 104
13 x 9 = 117
13 x 10 = 130
+++TABLA DEL 14+++
14 x 0 = 0
14 x 1 = 14
14 x 2 = 28
14 x 3 = 42
14 x 4 = 56
14 x 5 = 70
14 x 6 = 84
14 x 7 = 98
14 x 8 = 112
14 x 9 = 126
14 x 10 = 140
+++TABLA DEL 15+++
15 x 0 = 0
15 x 1 = 15
15 x 2 = 30
15 x 3 = 45
15 x 4 = 60
15 x 5 = 75
15 x 6 = 90
15 x 7 = 105
15 x 8 = 120
15 x 9 = 135
15 x 10 = 150
+++TABLA DEL 16+++
16 x 0 = 0
16 x 1 = 16
16 x 2 = 32
16 x 3 = 48
16 x 4 = 64
16 x 5 = 80
16 x 6 = 96
16 x 7 = 112
16 x 8 = 128
16 x 9 = 144
16 x 10 = 160
+++TABLA DEL 17+++
17 x 0 = 0
17 x 1 = 17
17 x 2 = 34
17 x 3 = 51
17 x 4 = 68
17 x 5 = 85
17 x 6 = 102
17 x 7 = 119
17 x 8 = 136
17 x 9 = 153
17 x 10 = 170
+++TABLA DEL 18+++
18 x 0 = 0
18 x 1 = 18
18 x 2 = 36
18 x 3 = 54
18 x 4 = 72
18 x 5 = 90
18 x 6 = 108
18 x 7 = 126
18 x 8 = 144
18 x 9 = 162
18 x 10 = 180
+++TABLA DEL 19+++
19 x 0 = 0
19 x 1 = 19
19 x 2 = 38
19 x 3 = 57
19 x 4 = 76
19 x 5 = 95
19 x 6 = 114
19 x 7 = 133
19 x 8 = 152
19 x 9 = 171
19 x 10 = 190
+++TABLA DEL 20+++
20 x 0 = 0
20 x 1 = 20
20 x 2 = 40
20 x 3 = 60
20 x 4 = 80
20 x 5 = 100
20 x 6 = 120
20 x 7 = 140
20 x 8 = 160
20 x 9 = 180
20 x 10 = 200
```

```python
#EJERCICIO 8: Pide al usuario dos números enteros por teclado. Asegúrate de que el primero es mayor o igual al segundo.
#Realiza la división entera y guarda en una tupla el dividendo, el divisor, el cociente y el resto de la divisón
#entera realizada y muéstrale al usuario el resultado por pantalla

x = float(input("Introduzca el dividendo: "))
y = float(input("Introduzca el divisor: "))

if y > x:
    print("El divisor no puede ser más grande que el dividendo.")
else:
    resultado = (x, y, x // y, x % y)

    print(resultado)
```

```
#RESPUESTA
Introduzca el dividendo: 5
Introduzca el divisor: 2
(5.0, 2.0, 2.0, 1.0)
```

```python
#EJERCICIO 9: Pide al usuario números entre 0 y 360. Para cada número, crea una tupla donde la primera entrada sea
#dicho número y, la segunda, la medida angular correspondiente en radianes. Recuerda, 360◦ = 2πrad. En
#este caso, utiliza π = 3.141592653589793

pi = 3.141592653589793
num = float(input("Introduzca un ángulo en grados (entre 0 y 360): "))

if num < 0 or num > 360:
    print("El ángulo no es adecuado")
else:
    conversion = (num, (num * 2 * pi) / 360)
print(conversion)
```

```
#RESPUESTA
Introduzca un ángulo en grados (entre 0 y 360): 180
(180.0, 3.141592653589793)
```

```python
#EJERCICIO 10: Pide al usuario números complejos. Para cada número, crea una tupla donde la primera entrada sea dicho número complejo, la segunda, su opuesto y, la tercera, su conjugado

a = int(input("Introduzca la parte real del número complejo: "))
j = int(input("Introduzca la parte compleja del número complejo: "))

z = complex(a, j)

resultado = (z, -z, z.conjugate())
print(resultado)
```

```
#RESPUESTA
Introduzca la parte real del número complejo: 1
Introduzca la parte compleja del número complejo: 5
((1+5j), (-1-5j), (1-5j))
```
