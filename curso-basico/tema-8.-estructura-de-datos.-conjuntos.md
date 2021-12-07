---
description: Explicación del uso de estructuras de datos tipo conjuntos en Python 3.
---

# Tema 8. Estructura de Datos. Conjuntos

## Conjunto

Ahora, es el turno de los **conjuntos**. Éstos son una estructura sin orden que no admiten múltiples ocurrencias de un mismo elemento. Pueden ser definidos a partir de una lista con la función `set()`, o bien, los elementos del conjunto pueden ir entre llaves, `{}`, y estar separados por comas.

Los conjuntos son:

* **hetereogéneos**: los elementos pueden ser de distinto tipo en un mismo conjunto
* **no** **mutables**: los elementos no pueden ser modifcados una vez el conjunto ha sido creado

Los conjuntos pueden construirse con la función `set()` o directamente entre llaves, `{}`.

```python
set1 = set([1, 7, 4, 2, 0])
print(set1)
type(set1)

#RESPUESTA
{0, 1, 2, 4, 7}
set
```

```python
set2 = set((1, 7, 4, 2, 0))
print(set2)
type(set2)

#RESPUESTA
{0, 1, 2, 4, 7}
set
```

```python
set3 = {1, 7, 4, 2, 0}
print(set3)
type(set3)

#RESPUESTA
{0, 1, 2, 4, 7}
set
```

Como se ha dicho antes, los conjuntos no admiten elementos repetidos:

```python
set1 = {1, 2, 2, 3, 3, 3, 4, 4, 4, 4}
set1

#RESPUESTA
{1, 2, 3, 4}
```

**Observación.** Al decir que los conjuntos no tienen orden, lo que ocurre es que `Python` no mantendrá el que hemos introducido, tal y como hacía con las listas, sino que reordenará todos los elementos por orden primero numérico (yendo antes los negativos que los positivos) y luego alfabético de las claves. Con la función `print()`, el conjunto no se ordena correctamente.

```python
set1 = {1, "a", "i", "o", 2, "e", 4, 3, 5, "u"}
set1

#RESPUESTA
{1, 2, 3, 4, 5, 'a', 'e', 'i', 'o', 'u'}
```

```python
print(set1)

#RESPUESTA
{1, 2, 3, 4, 5, 'e', 'a', 'i', 'u', 'o'}
```

```python
set2 = {-1, "a", 3, "i", "o", 2, "e", 4, -3, 5, "u", 1}
set2

#RESPUESTA
{-1, -3, 1, 2, 3, 4, 5, 'a', 'e', 'i', 'o', 'u'}
```

```python
print(set2)

#RESPUESTA
{1, 2, 3, 4, 5, 'e', 'a', 'i', 'u', 'o', -3, -1}
```

Por lo que hemos visto hasta ahora, podemos decir que los conjuntos en `Python` son fieles a la definición matemática de éstos, salvo por el hecho de que en `Python` **un conjunto no puede contener como elemento a otro conjunto**:

**Conjunto.** Colección de elementos pertenecientes a la misma categoría, y cuya agrupación puede ser considerada o identificada en sí misma como un objeto. Un conjunto queda definido únicamente por sus elementos y por nada más. En particular, un conjunto puede escribirse como una lista de elementos, pero cambiar el orden de dicha lista o añadir elementos repetidos no define un conjunto nuevo.

### Subconjuntos

**Subconjunto.** Un subconjunto **B** de un conjunto **A** es un conjunto que contiene algunos de los elementos de A (o quizá todos). Se denota por **B** **⊆** **A**

**Subconjunto propio.** Un subconjunto propio **B** de un conjunto **A** es un conjunto que tiene algunos de los elementos de **A**, pero no todos. Se denota por **B ⊂ A**

Para saber si un conjunto **B** es subconjunto del conjunto **A**, podemos utilizar el método `.issubset()` o el comparador `<=`. Para saber si se trata de un subconjunto propio, tenemos el comparador `<`.

```python
A, B = {0, 3, 7, 2, 5}, {2, 3, 0}
B.issubset(A)

#RESPUESTA
True
```

```python
B <= A

#RESPUESTA
True
```

```python
B < A

#RESPUESTA
True
```

**Superconjunto.** Un superconjunto **A** de un conjunto **B** es un conjunto que contiene a **B**. Se denota por **A ⊇ B**

**Superconjunto propio.** Un superconjunto propio **A** de un conjunto $ es un conjunto que contiene a **B** y consta de al menos un elemento más. Se denota por **A ⊃ B**

Para saber si un conjunto **A** es superconjunto del conjunto **B**, podemos utilizar el método `.issuperset()` o el comparador `>=`. Para saber si se trata de un superconjunto propio, tenemos el comparador `>`.

```python
A, B = {0, 3, 7, 2, 5}, {2, 3, 0}
A.issuperset(B)

#RESPUESTA
True
```

```python
A >= B

#RESPUESTA
True
```

```python
A > B

#RESPUESTA
True
```

**Ojo:** ¡Pero no todos los conjuntos son siempre subconjunto o superconjunto unos de otros!

```python
X = {1,2,3}
Y = {'a', 'b', 'c'}
```

```python
X <= Y

#RESPUESTA
False
```

```python
X >= Y

#RESPUESTA
False
```

### Operaciones con conjuntos

Dados los conjuntos **A** y **B**, vamos a ver una serie de operaciones que podemos hacer con ellos.

**Unión.** La unión de dos conjuntos **A** y **B** es un nuevo conjunto **A ∪ B** que contiene todos los elementos de **A** y/o todos los de **B**. En `Python`, la unión de dos conjuntos se consigue con la función `|` o bien, con el método `.union()`

```python
A, B = {1, 3, 5, 7, 9}, {0, 2, 4, 6, 8}
A | B

#RESPUESTA
{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
```

```python
A.union(B)

#RESPUESTA
{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
```

```python
B.union(A)

#RESPUESTA
{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
```

**Intersección.** La intersección entre dos conjuntos **A** y **B** es un nuevo conjunto **A ∩ B** que contiene todos los elementos comunes de **A** y **B**.

En `Python`, la intersección de dos conjuntos se consigue con la función `&` o bien, con el método `.intersection()`

```python
A, B = {0, 1, 3, 5, 8, 13}, {0, 2, 4, 6, 8}
A & B

#RESPUESTA
{0, 8}
```

```python
A.intersection(B)

#RESPUESTA
{0, 8}
```

```python
B.intersection(A)

#RESPUESTA
{0, 8}
```

**Diferencia.** La diferencia entre dos conjuntos **A** y **B** es un nuevo conjunto **A** - **B** que contiene todos los elementos de **A** que no están en **B**

En `Python`, la diferencia de dos conjuntos se consigue con la función `-` o bien, con el método `.difference()`

```python
A, B = {0, 1, 4, 5, 8, 13}, {0, 3, 4, 7, 8}
A - B

#RESPUESTA
{1, 5, 13}
```

```python
A.difference(B)

#RESPUESTA
{1, 5, 13}
```

```python
B.difference(A)

#RESPUESTA
{3, 7}
```

**Diferencia simétrica.** La diferencia entre dos conjuntos **A** y **B** es un nuevo conjunto **A Δ B** que contiene todos los elementos de **A ∪ B** no están en **A ∩ B**

$$A\vartriangle B = (A\cup B) - (A\cap B) = (A - B)\cup (B - A)$$

En `Python`, la diferencia simétrica de dos conjuntos se consigue con el método `.symmetric_difference()`

```python
A, B = {0, 1, 4, 5, 8, 13}, {0, 3, 4, 7, 8}
A.symmetric_difference(B)

#RESPUESTA
{1, 3, 5, 7, 13}
```

```python
(A-B) | (B-A)

#RESPUESTA
{1, 3, 5, 7, 13}
```

```python
(A | B) - (A & B)

#RESPUESTA
{1, 3, 5, 7, 13}
```

### Elementos de un conjunto

Podemos añadir un elemento a un conjunto con el método `.add()`

```python
set1 = {1, 2, 3, 4, 5}
set1.add(-1)
print(set1)

set1.add(0)
print(set1)

#RESPUESTA
{1, 2, 3, 4, 5, -1}
{0, 1, 2, 3, 4, 5, -1}
```

Para añadir elementos de otro conjunto en el conjunto actual, podemos usar el método `.update()`

```python
set1 = {1, 2, 3, 4, 5}
set2 = {-1, -2, -3, -4, -5}

print(set1)

set1.update(set2)
print(set1)

#RESPUESTA
{1, 2, 3, 4, 5}
{1, 2, 3, 4, 5, -1, -5, -4, -3, -2}
```

**Observación.** El método `.update()` nos permite añadir los elementos de un iterable al conjunto actual

```python
set1 = {1, 2, 3, 4, 5}
l = [-1, -2, -3, -4, -5]

set1.update(l)
print(set1)

#RESPUESTA
{1, 2, 3, 4, 5, -2, -5, -4, -3, -1}
```

Podemos averiguar si un elemento pertenece a un conjunto con el operador `in`

```python
set1 = {1, -1, 2, -2, 3, -3}
print(3 in set1)
print(0 in set1)

#RESPUESTA
True
False
```

También podemos eliminar elementos de un conjunto con los métodos `.remove()` o `.discard()`

```python
set1 = {"a",  "e", "i", "o", "u"}
set1.remove("a")
set1.discard("o")

print("a" in set1)
print("o" in set1)
print(set1)
```

```
#RESPUESTA
False
False
{'e', 'u', 'i'}
```

**Observación.** Si intentamos eliminar un elemento que no existe ya de por sí en el conjunto con el método `.remove()`, `Python` nos devolverá error, mientras que con el método `.discard()` no devolverá ningún error.

### Tamaño de un conjunto

Para saber cuántos elementos contiene un conjunto, podemos usar la función `len()`del siguiente modo:

```python
set1 = {1, "a", "i", "o", 2, "e", 4, 3, 5, "u"}
print(len(set1))

#RESPUESTA
10
```

## Bucles y conjuntos

Podemos acceder a todos los elementos de un conjunto mediante un bucle `for`

```python
set1 = {"manzana", "pera", "melón"}
for item in set1:
  print(item)
```

```
#RESPUESTA
melón
manzana
pera
```

## Más métodos de conjuntos

El método `.pop()` nos devuelve un objeto del conjunto (como no hay orden, no sabemos cuál es) y lo elimina de éste.

```python
set1 = {"u", 5, -3, "a", "b"}
set1

#RESPUESTA
{-3, 5, 'a', 'b', 'u'}
```

```python
set1.pop()

#RESPUESTA
'b'
```

```python
set1

#RESPUESTA
{-3, 5, 'a', 'u'}
```

El método `.clear()` vacía el conjunto.

```python
set1 = {"a", "e", "i", "o", "u"}
set1.clear()
print(set1)

#RESPUESTA
set()
```

#### EJERCICIO 1:&#x20;

Vamos a pedirle al usuario una frase y vamos a guardar en un conjunto las letras que aparecen en dicha frase.

```python
print("+ A continuación debe escribir una frase")
s = str(input("+ Su frase: "))
set1 = set()
for i in s.lower():
    if i != " ":
        set1.add(i)

print(set1)
```

```
#RESPUESTA
+ A continuación debe escribir una frase
+ Su frase: a hierro muere
{'h', 'm', 'u', 'r', 'o', 'a', 'i', 'e'}
```

#### EJERCICIO 2:&#x20;

Vamos a pedirle al usuario dos palabras y vamos a calcular la intersección de las letras de cada palabra. Para ello habrá que crear dos conjuntos que contendrán, respectivamente, las letras que forman cada palabra.

```python
print("+ Escriba dos palabras: ")
word1 = str(input("+ Palabra 1: "))
set1 = set()
for c in word1:
    if c != " ":
        set1.add(c)
word2 = str(input("+ Palabra 2: "))
set2 = set()
for i in word2:
    if i != " ":
        set2.add(i)
print(set1.intersection(set2))
```

```
#RESPUESTA
+ Escriba dos palabras: 
+ Palabra 1: albondiga
+ Palabra 2: bonachon
{'o', 'n', 'a', 'b'}
```

#### EJERCICIO 3:&#x20;

Vamos a pedirle 4 números enteros al usuario. Se corresponderán con los extremos de los intervalos \[a,b] y \[c,d] . Vamos a generar dos conjuntos que guarden, respectivamente, los enteros contenidos en cada uno de los intervalos (incluyendo los extremos) y, finalmente, calcularemos la diferencia simétrica.

```python
print("+ Introduzca 4 números enteros: ")
n1 = int(input("Número 1: "))
n2 = int(input("Número 2: "))
n3 = int(input("Número 3: "))
n4 = int(input("Número 4: "))

if n2 < n1 or n4 < n3:
  print("No has proporcionado dos intevalos")
else:   
    set1 = set(range(n1, n2 + 1))
    set2 = set(range(n3, n4 + 1))

    print(set1.symmetric_difference(set2))
```

```
#RESPUESTA
+ Introduzca 4 números enteros: 
Número 1: 1
Número 2: 3
Número 3: 2
Número 4: 4
{1, 4}
```

#### EJERCICIO 4:&#x20;

Vamos a guardar en un conjunto los números primos comprendidos entre 2 y el número n que nos indique el usuario mediante la criba de Eratóstenes.

```python
n = int(input("Introduce un número entero mayor que 2: "))
primes = set(range(2, n + 1))
numbers = list(range(2, n + 1))
multiples = [True for x in range(len(numbers))]

for i in range(len(numbers)):
  if multiples[i] == False:
    continue
  for j in range(i + 1, len(numbers)):
    if numbers[j] % numbers[i] == 0:
      multiples[j] = False
      primes.discard(numbers[j])

print(primes)
```

#### EJERCICIO 5:&#x20;

Vamos a crear un programa que nos devuelva el elemento máximo de un conjunto sin utilizar la función max().

```python
myset = {20, 3, 5, 10, 9, 30, -5, 30}
max = -99999

for i in myset:
    if i > max:
        max = i
        
print(max)

#RESPUESTA
30
```

## REPASO

```python
#EJERCICIO 1: Dado un número entero introducido por teclado, guarda sus divisores en un conjunto y muéstralo

n = int(input("Introduzca un número: "))

divisores = set()
for i in range(1, n + 1):
    if n % i == 0:
        divisores.add(i)

print(divisores)
```

```
#RESPUESTA
Introduzca un número: 10
{1, 2, 10, 5}
```

```python
#EJERCICIO 2: Crea un programa que dado un conjunto, nos devuelva su mínimo. Debes hacerlo sin recurrir a la función min().

myset = {20, 3, 5, 10, 9, 30, -5, 30}
min = 9999

for i in myset:
    if i < min:
        min = i

print(min)

#RESPUESTA
-5
```

```python
#EJERCICIO 3:Dada una frase introducida por teclado, guarda en un conjunto todas las palabras que empiecen por la letra indicada por el usuario.

print("Dada una frase introducida por teclado, guarda en un conjunto todas las palabras que empiecen por la letra indicada por el usuario.")
s = str(input("Introduce una frase: "))
l = str(input("Introduce una letra: "))

s = s.lower()
palabras = set()

for word in s.split():
    if word[0] == l.lower():
        palabras.add(word)

print(palabras)
```

```
#RESPUESTA
Dada una frase introducida por teclado, guarda en un conjunto todas las palabras que empiecen por la letra indicada por el usuario.
Introduce una frase: Hola me llamo hector
Introduce una letra: h
{'hector', 'hola'}
```

```python
#EJERCICIO 4: Dado un conjunto, crea un programa que nos devuelva el caracter con mayor valor ASCII. Debes hacerlo sin recurrir a la función max().

myset = {"a", "e", "i", "o", "u"}
max = -9999

for i in myset:
    if ord(i) > max:
        max = ord(i)
print(chr(max))

#RESPUESTA
u
```

```python
#EJERCICIO 5: Dado un conjunto, crea un programa que nos devuelva el caracter con menor valor ASCII. Debes hacerlo sin recurrir a la función min().

myset = {"a", "e", "i", "o", "u"}
min = 9999

for i in myset:
    if ord(i) < min:
        min = ord(i)
print(chr(min))

#RESPUESTA
a
```

```python
#EJERCICIO 6: Dada una frase introducida por teclado, guarda en un conjunto todas las palabras que contengan la letra indicada por el usuario.

print("Dada una frase introducida por teclado, guarda en un conjunto todas las palabras que contengan la letra indicada por el usuario.")
s = str(input("Introduce una frase: "))
l = str(input("Introduce una letra: "))

s = s.lower()
palabras = set()

for word in s.split():
    for c in word:
        if c == l.lower():
            palabras.add(word)

print(palabras)
```

```
#RESPUESTA
Dada una frase introducida por teclado, guarda en un conjunto todas las palabras que contengan la letra indicada por el usuario.
Introduce una frase: supercalifragilistico
Introduce una letra: a
{'supercalifragilistico'}
```

```python
#EJERCICIO 7: Dada una frase introducida por teclado, guarda en un conjunto la primera letra de cada palabra sin hacer uso del método .split().

print("Dada una frase introducida por teclado, guarda en un conjunto la primera letra de cada palabra sin hacer uso del método .split().")
s = str(input("Introduce una frase: "))
s = s.strip()
letras = set(s[0])

for c in range(len(s)):
    if s[c] == " ":
        letras.add(s[c + 1])

print(letras)
```

```
#RESPUESTA
Dada una frase introducida por teclado, guarda en un conjunto la primera letra de cada palabra sin hacer uso del método .split().
Introduce una frase: Hola me llamo enrique
{'H', 'm', 'e', 'l'}
```

```python
#EJERCICIO 8: Dada una frase introducida por teclado, guarda en un conjunto todas las palabras con longitud par.

print("Dada una frase introducida por teclado, guarda en un conjunto todas las palabras con longitud par.")
s = str(input("Introduce una frase: "))
s = s.lower()

pares = set()

for word in s.split():
    if len(word) % 2 == 0:
        pares.add(word)

print(pares)
```

```
#RESPUESTA
Dada una frase introducida por teclado, guarda en un conjunto todas las palabras con longitud par.
Introduce una frase: Hola me llamo enrique
{'me', 'hola'}
```

```python
#EJERCICIO 9: Dada una frase introducida por teclado, guarda en un conjunto todas las palabras que acaben por la letra indicada por el usuario.

print("Dada una frase introducida por teclado, guarda en un conjunto todas las palabras que acaben por la letra indicada por el usuario.")
s = str(input("Introduce una frase: "))
l = str(input("Introduce una letra: "))

s = s.lower()
palabras = set()

for word in s.split():
    if word[-1] == l:
        palabras.add(word)

print(palabras)
```

```
#RESPUESTA
Dada una frase introducida por teclado, guarda en un conjunto todas las palabras que acaben por la letra indicada por el usuario.
Introduce una frase: Hola me llamo enriqueta
Introduce una letra: a
{'enriqueta', 'hola'}
```

```python
#EJERCICIO 10: Dada una frase introducida por teclado, guarda en un conjunto todas las palabras palíndromas.

print("Dada una frase introducida por teclado, guarda en un conjunto todas las palabras palíndromas")
s = str(input("Introduce una frase: "))

s = s.lower()
palindromas = set()

for word in s.split():
    if word == word[::-1]:
        palindromas.add(word)
print(palindromas)
```

```
#RESPUESTA
Dada una frase introducida por teclado, guarda en un conjunto todas las palabras palíndromas
Introduce una frase: Aba hecho Anana arañara peso
{'anana', 'arañara', 'aba'}
```
