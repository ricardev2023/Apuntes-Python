---
description: Explicación del uso de Operadores de Iteración en Python 3.
---

# Tema 5. Operadores de Iteración

## El bucle `while`

La idea del bucle `while` es: mientras la condición sea cierta, seguimos realizando las líneas del interior del bucle. Una vez la condición deja de ser verdadera, salimos del bucle.

Su estructura es la siguiente

```python
inicialización de la variable de la condición
while condición verdadera:
  instrucción 1
  instrucción 2
  .
  .
  .
  instrucción n
```

**Observación.** Vuelven a aparecer tanto los dos puntos después de la condición como la indentación previa a las instrucciones que se encuentran dentro del bucle.

**¡Cuidado!** Hay que tener en cuenta que alguna de las instrucciones que se encuentran dentro del bucle `while` tiene que modificar a la variable de la condición. De lo contrario, si la variable de la condición nunca es modificada, la condición nunca llegará a ser falsa y el bucle no acabaría nunca, con lo que pasaría a convertirse en lo que se denomina bucle infinito.

Una de las utilidades de un bucle `while` es evitar el copia y pega de algunas funciones. Por ejemplo, si queremos impirmir los primeros 10 números naturales, en vez de copiar 10 veces la función `print()`, una para cada número, lo podemos hacer todo con un bucle `while`:

Las variables i, j y k son utilizadas como estandar en los bucles como índices.

```python
i = 1 # Inicializamos la variable
while i <= 10: # Queremos que i como mucho valga 10
  print(i) # Imprimimos los números
  i += 1 # Incrementamos una unidad en cada iteración
```

```
#RESPUESTA
1
2
3
4
5
6
7
8
9
10
```

#### EJERCICIO 1:&#x20;

Con un bucle while, dado un string vamos a recorrer una frase y contar el número total de vocales.

```python
phrase = "En un lugar de la mancha de cuyo nombre no quiero acordarme."
phrase = phrase.lower()
i = 0
vocals = 0
while i < len(phrase):
    if phrase[i] == "a" or phrase[i] == "e" or phrase[i] == "i" or phrase[i] == "o" or phrase[i] == "u":
        vocals += 1 
        i += 1
    else:   # El else se puede omitir utilizando i = i + 1 a la misma altura del if, dentro de while, lo que afecta a todos los casos.
        i += 1 
print("El número de vocales es: {}".format(vocals))

#RESPUESTA
El número de vocales es: 22
```

### Comando `break`

`break` es muy útil si dada una condición queremos que se salga inmediatamente de un bucle `while`. Veámoslo con un ejemplo:

***

#### **Ejemplo 1**

La sucesión de Fibonacci es una sucesión infinita que se caracteriza porque cada término es la suma de los dos anteriores. Algunos de sus términos son 1, 1, 2, 3, 5, 8, 13...

Supongamos que queremos que se nos impriman los 20 primeros términos de esta serie. Por tanto, necesitaremos por un lado los términos de la serie y, por otro, los índices que ocupan.

**Ejercicio.** Pensad en cómo podríais resolver este problema en el cual se exige que en algún momento utilicéis el comando `break`.

```python
fibo_ant = 1 # Término anterior
fibo = 1 # Término actual
idx = 3 # Como ya tenemos los dos primeros términos, empezamos con el índice 3

print("El término {} ocupa la posición {}".format(fibo_ant, 1))
print("El término {} ocupa la posición {}".format(fibo, 2))

while fibo <= 500000: # Establecemos una cota para que el bucle no sea infinito
  temp = fibo  # Guardamos temporalmente el fibonacci actual 
  fibo = fibo + fibo_ant  # Calculamos el nuevo término de la sucesión
  fibo_ant = temp # Modicamos el valor del término anterior
  
  print("El término {} ocupa la posición {}".format(fibo, idx))
  
  if idx == 20: # Si llegamos al vigésimo índice, 
    break       # salimos del bucle
  
  idx += 1 # Incrementamos el valor del índice
```

```
El término 1 ocupa la posición 1
El término 1 ocupa la posición 2
El término 2 ocupa la posición 3
El término 3 ocupa la posición 4
El término 5 ocupa la posición 5
El término 8 ocupa la posición 6
El término 13 ocupa la posición 7
El término 21 ocupa la posición 8
El término 34 ocupa la posición 9
El término 55 ocupa la posición 10
El término 89 ocupa la posición 11
El término 144 ocupa la posición 12
El término 233 ocupa la posición 13
El término 377 ocupa la posición 14
El término 610 ocupa la posición 15
El término 987 ocupa la posición 16
El término 1597 ocupa la posición 17
El término 2584 ocupa la posición 18
El término 4181 ocupa la posición 19
El término 6765 ocupa la posición 20
```

```python
# EJEMPLO HECHO POR MI
#Las primeras 20 posiciones de la sucesión de Fibonacci con función break
fibo_prev = 1
fibo = 1 
count = 2

phrase = "El término {} ocupa la posición {}."
print(phrase.format(fibo_prev, count - 1))
print(phrase.format(fibo, count))

while fibo <= 5000000:
    fibo_temp = fibo
    fibo += fibo_prev
    fibo_prev = fibo_temp
    count += 1

    print(phrase.format(fibo, count))

    if count == 20:
        break
```

```
El término 1 ocupa la posición 1.
El término 1 ocupa la posición 2.
El término 2 ocupa la posición 3.
El término 3 ocupa la posición 4.
El término 5 ocupa la posición 5.
El término 8 ocupa la posición 6.
El término 13 ocupa la posición 7.
El término 21 ocupa la posición 8.
El término 34 ocupa la posición 9.
El término 55 ocupa la posición 10.
El término 89 ocupa la posición 11.
El término 144 ocupa la posición 12.
El término 233 ocupa la posición 13.
El término 377 ocupa la posición 14.
El término 610 ocupa la posición 15.
El término 987 ocupa la posición 16.
El término 1597 ocupa la posición 17.
El término 2584 ocupa la posición 18.
El término 4181 ocupa la posición 19.
El término 6765 ocupa la posición 20.
```

**Ejercicio.** El ejemplo anterior se podría haber hecho perfectamente sin necesidad de utilizar la función `break`. Pensad en cómo modificaríais el código anterior para obtener el mismo resultado únicamente haciendo uso de un bucle `while`.

***

```python
# EJEMPLO HECHO POR MI
#Las primeras 20 posiciones de la sucesión de Fibonacci SIN función break
fibo_prev = 1
fibo = 1 
count = 2

phrase = "El término {} ocupa la posición {}."
print(phrase.format(fibo_prev, count - 1))
print(phrase.format(fibo, count))

while count < 20:
    fibo_temp = fibo
    fibo += fibo_prev
    fibo_prev = fibo_temp
    count += 1

    print(phrase.format(fibo, count))
```

```
El término 1 ocupa la posición 1.
El término 1 ocupa la posición 2.
El término 2 ocupa la posición 3.
El término 3 ocupa la posición 4.
El término 5 ocupa la posición 5.
El término 8 ocupa la posición 6.
El término 13 ocupa la posición 7.
El término 21 ocupa la posición 8.
El término 34 ocupa la posición 9.
El término 55 ocupa la posición 10.
El término 89 ocupa la posición 11.
El término 144 ocupa la posición 12.
El término 233 ocupa la posición 13.
El término 377 ocupa la posición 14.
El término 610 ocupa la posición 15.
El término 987 ocupa la posición 16.
El término 1597 ocupa la posición 17.
El término 2584 ocupa la posición 18.
El término 4181 ocupa la posición 19.
El término 6765 ocupa la posición 20.
```

#### EJERCICIO 2:&#x20;

Con un bucle while, dados dos números enteros proporcionados por el usuario, vamos a encontrar el primer número divisible entre 2, 3 y 5, siempre que sea posible, que se encuentre dentro del intervalo formado por los dos números dados por el usuario (ambos extremos también incluidos).

```python
print("Escriba dos números que limiten un intervalo y la aplicación le enseñará el primero que sea divisible entre 2, 3 y 5.")
ni = int(input("Escriba el inicio del intervalo: "))
nf = int(input("Escriba el final del intervalo: "))
if nf < ni:
    print("El final no puede ser anterior al principio.")
else:
    n = ni
    while  n <= nf:
        if n % 2 == 0 and n % 3 == 0 and n % 5 == 0:
            print("El numero {} es el primero del intervalo [{},{}] en ser dividible entre 2, 3 y 5".format(n, ni, nf))
            break
        else:
            n += 1
    else:
        print("Ningun numero cumple las limitaciones.")
```

```
#RESPUESTA
Escriba dos números que limiten un intervalo y la aplicación le enseñará el primero que sea divisible entre 2, 3 y 5.
Escriba el inicio del intervalo: 1
Escriba el final del intervalo: 20000
El numero 30 es el primero del intervalo [1,20000] en ser dividible entre 2, 3 y 5
```

### Combinación `while ... else`

Podemos combinar un bucle `while` con el operador `else` para ejecutar un bloque de código una vez la condición del `while` haya dejado de ser verdadera.

```python
i = 10
print("Preparados para despegue. Empieza la cuenta atrás.")
while i >= 0:
  print(i)
  i -= 1
else:
  print("La cuenta atrás ha finalizado.")
```

```
#RESPUESTA
Preparados para despegue. Empieza la cuenta atrás.
10
9
8
7
6
5
4
3
2
1
0
La cuenta atrás ha finalizado.
```

#### EJERCICIO 3:&#x20;

Vamos a hacer que el usuario introduzca números por teclado e ir sumándolos. Cuando el usuario introduzca 0 saldremos del bucle while. Al salir del bucle, con un else mostraremos la suma.

```python
print("Introduzca numeros para que se vayan sumando, en caso de querer terminar, introduzca 0.")
suma = int(input("+ Introduzca el primer número: "))
ns = 1

while ns != 0:
    ns = int(input("+ Introduza el siguiente número: "))
    suma += ns
    print("+ Resultado: {}".format(suma))
else:
    print("+ Saliendo del programa")
```

```
#RESPUESTA
Introduzca numeros para que se vayan sumando, en caso de querer terminar, introduzca 0.
+ Introduzca el primer número: 0
+ Introduza el siguiente número: 0
+ Resultado: 0
+ Saliendo del programa
```

#### EJERCICIO 4:&#x20;

Imaginemos las letras del abecedario ordenadas y dispuestas en círculo. Es decir, a la derecha de la A está la B, luego la C, y así sucesivamente hasta la Z. A la derecha de la Z, se encuentra de nuevo la letra A.

Vamos a hacer que el usuario introduzca un valor entero n, que se corresponderá con la rotación que llevará a una determinada letra n posiciones a su derecha. Por ejemplo, si la rotación es 4, entonces la A pasará a la E, la B a la F, ..., la Y a la C y la Z a la D.

Con un bucle while, vamos a construir el programa que desplazará las letras n posiciones a la derecha.

**PISTA**: Investiga las funciones chr() y ord() para pasar del valor ASCII de un caracter al caracter y viceversa.

```python
n = int(input("Introduce una rotación: "))
i = 65

while i <= 90:
  if i + n <= 90:
    print(chr(i) + ": " + chr(i + n))
  else:
    print(chr(i) + ": " + chr((i - 26) + n))
  i += 1
```

```
#RESPUESTA
Introduce una rotación: 10
A: K
B: L
C: M
D: N
E: O
F: P
G: Q
H: R
I: S
J: T
K: U
L: V
M: W
N: X
O: Y
P: Z
Q: A
R: B
S: C
T: D
U: E
V: F
W: G
X: H
Y: I
Z: J
```

## Bucle `for`

La idea del bucle `for` es: para todos los elementos de la clave, seguimos realizando las líneas del bucle. Una vez nos quedemos sin elementos, salimos del bucle.

Su estructura es la siguiente

```python
for clave:
  instrucción 1
  instrucción 2
  .
  .
  .
  instrucción n
```

**Observación.** Vuelven a aparecer tanto los dos puntos después de la clave como la indentación previa a las instrucciones que se encuentran dentro del bucle.

Un ejemplo del uso de un bucle `for` es el de recorrer todos los caracteres de un string:

```python
s = "Me gustan las matemáticas"

for c in s:
  print(c)
```

```
#RESPUESTA
M
e
 
g
u
s
t
a
n
 
l
a
s
 
m
a
t
e
m
á
t
i
c
a
s
```

Lo que hace el anterior chunk de código es imprimir todos y cada uno de los caracteres, a los que identificamos por `c`, que se encuentran en el string `s`.

#### EJERCICIO 5:&#x20;

Vamos a recorrer un string dado con un bucle for y lo vamos a devolver impreso del revés.

```python
print("Escriba una frase y la devolveré del revés.")
s = input("Escriba aquí su frase: ")
s_inv = ""

for c in s:
    s_inv = c + s_inv
print(s_inv)
```

```
Escriba una frase y la devolveré del revés.
Escriba aquí su frase: pintor
rotnip
```

### Función `range()`

La función `range()` tiene 3 posibles argumentos:

* `start`
* `stop`
* `step`

Veremos el uso de la función `range()` con un ejemplo. Recuperemos el ejemplo en que queríamos imprimir los 10 primeros números naturales:

```python
for i in range(1, 11, 1):
  print(i)
```

```
#RESPUESTA
1
2
3
4
5
6
7
8
9
10
```

```python
for x in range(5):
    print(x)
```

```
#RESPUESTA
0
1
2
3
4
```

**Observación.** Cosas a tener en cuenta cuando usamos la función `range()`:

* El elemento indicado en el argumento `stop` nunca se incluye.
* Si no indicamos ningún elemento en el argumento `start`, por defecto éste vale 0.
* El valor por defecto del argumento `step` es 1.

Por lo tanto, obtendríamos el mismo resultado que en el ejemplo anterior ejecutando las siguientes líneas de código:

```python
for i in range(1, 11):
  print(i)
```

```
#RESPUESTA
1
2
3
4
5
6
7
8
9
10
```

¿Y si quisiéramos imprimir los 10 primeros números naturales invirtiendo el orden? Pues, con un bucle `for`, lo haríamos del siguiente modo:

```python
for i in range(10, 0, -1):
  print(i)
```

```
#RESPUESTA
10
9
8
7
6
5
4
3
2
1
```

#### EJERCICIO 6:&#x20;

Con un bucle for, dada una progresión aritmética de números enteros indicada por el usuario (nos dará el primer término, la diferencia y la cota), vamos a calcular la suma de los elementos incluyendo la cota.

Un ejemplo de progresión aritmética es: 0, 2, 4, 6, 8, ... donde el primer término es 0 y la diferencia entre sus términos es 2.

```python
print("Proporcione al programa el número inicial de la progresión aritmética, la diferencia y la cota máxima.")
ni = int(input("Introduzca el inicio: "))
d = int(input("Introduzca la diferencia: "))
c = int(input("Introduzca la cota: ")) + 1
count = 0 

for idx in range(ni, c, d):
    count += idx
print ("La suma de todos los terminos es {}".format(count))
```

```
#RESPUESTA
Proporcione al programa el número inicial de la progresión aritmética, la diferencia y la cota máxima.
Introduzca el inicio: 1
Introduzca la diferencia: 1
Introduzca la cota: 10
La suma de todos los terminos es 55
```

### Comando `continue`

El comando `continue` es similar a `break`, pero en vez de salir del bucle, lo que hace es interrumpir la iteración en la que se encuentra y empezar la siguiente iteración.

***

#### **Ejemplo 2**

Supongamos que queremos que se nos impriman todos los números entre 0 y 100 que no son ni divisibles entre 2 ni entre 5.

**Ejercicio.** Pensad cómo podríais resolver este problema en el cual se exige que en algún momento utilicéis el comando `continue`.

```python
for i in range(101):
  if i % 2 == 0 or i % 5 == 0:
    continue
  print(i)
```

```
#RESPUESTA
1
3
7
9
11
13
17
19
21
23
27
29
31
33
37
39
41
43
47
49
51
53
57
59
61
63
67
69
71
73
77
79
81
83
87
89
91
93
97
99
```

***

#### EJERCICIO 7:&#x20;

Con un bucle for, vamos a recorrer un string dado y vamos a imprimir todas las letras salvo por la letra indicada por el usuario.

```python
print("introduzca un string y la letra que quiere eliminar del string, el programa lo hará.")
s = input("Introduzca su string: ").lower()
w = ord(input("Introduzca su letra: ").lower())
s_new = ""

for c in s:
    if ord(c) == w:
        continue
    else:
    s_new = s_new + c
print(s_new)
```

```
#RESPUESTA
introduzca un string y la letra que quiere eliminar del string, el programa lo hará.
Introduzca su string: A MI ME GUSTA MAS MI MARICONERA MARRON
Introduzca su letra: m
a i e gusta as i ariconera arron
```

#### EJERCICIO 8:&#x20;

Dado un string, con un bucle for vamos a imprimirlo sin vocales y vamos a salir del bucle si la letra que indique el usuario aparece más de n veces, número que también nos proporcionará el usuario.

```python
print("Escriba una frase, una letra y un número. El string se imprimirá sin vocales y si la letra aparece el numero de veces que ha marcado, se parará.")
s = input("Su frase: "). lower()
l = input("La letra a controlar: ").lower()
n = int(input("Numero de veces que aparecerá: "))
count = 0
s_new = ""

for c in s:

    if count == n:
        break
    elif c == l:
        count += 1
    elif c == "a" or c == "e" or c == "i" or c == "o" or c == "u":
        continue
    else:
        s_new += c
    
print(s_new)
```

```
#RESPUESTA
Escriba una frase, una letra y un número. El string se imprimirá sin vocales y si la letra aparece el numero de veces que ha marcado, se parará.
Su frase: a mi me gusta el pipiribipipi de la bota de vino.
La letra a controlar: i
Numero de veces que aparecerá: 3
 m m gst l pp
3
```

## Bucles anidados

Se trata de bucles dentro de bucles

***

#### **Ejemplo 3**

Vamos a calcular las tablas de multiplicar de los números del 1 al 10 anidando dos bucles `for`:

```python
for i in range(1, 11):
  print("\nTabla de multiplicar del {}".format(i))
  for j in range(1, 21):
    print("{} x {} = {}".format(i, j, i * j))
```

```
#RESPUESTA
Tabla de multiplicar del 1
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
1 x 11 = 11
1 x 12 = 12
1 x 13 = 13
1 x 14 = 14
1 x 15 = 15
1 x 16 = 16
1 x 17 = 17
1 x 18 = 18
1 x 19 = 19
1 x 20 = 20

Tabla de multiplicar del 2
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
2 x 11 = 22
2 x 12 = 24
2 x 13 = 26
2 x 14 = 28
2 x 15 = 30
2 x 16 = 32
2 x 17 = 34
2 x 18 = 36
2 x 19 = 38
2 x 20 = 40

Tabla de multiplicar del 3
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
3 x 11 = 33
3 x 12 = 36
3 x 13 = 39
3 x 14 = 42
3 x 15 = 45
3 x 16 = 48
3 x 17 = 51
3 x 18 = 54
3 x 19 = 57
3 x 20 = 60

Tabla de multiplicar del 4
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
4 x 11 = 44
4 x 12 = 48
4 x 13 = 52
4 x 14 = 56
4 x 15 = 60
4 x 16 = 64
4 x 17 = 68
4 x 18 = 72
4 x 19 = 76
4 x 20 = 80

Tabla de multiplicar del 5
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
5 x 11 = 55
5 x 12 = 60
5 x 13 = 65
5 x 14 = 70
5 x 15 = 75
5 x 16 = 80
5 x 17 = 85
5 x 18 = 90
5 x 19 = 95
5 x 20 = 100

Tabla de multiplicar del 6
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
6 x 11 = 66
6 x 12 = 72
6 x 13 = 78
6 x 14 = 84
6 x 15 = 90
6 x 16 = 96
6 x 17 = 102
6 x 18 = 108
6 x 19 = 114
6 x 20 = 120

Tabla de multiplicar del 7
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
7 x 11 = 77
7 x 12 = 84
7 x 13 = 91
7 x 14 = 98
7 x 15 = 105
7 x 16 = 112
7 x 17 = 119
7 x 18 = 126
7 x 19 = 133
7 x 20 = 140

Tabla de multiplicar del 8
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
8 x 11 = 88
8 x 12 = 96
8 x 13 = 104
8 x 14 = 112
8 x 15 = 120
8 x 16 = 128
8 x 17 = 136
8 x 18 = 144
8 x 19 = 152
8 x 20 = 160

Tabla de multiplicar del 9
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
9 x 11 = 99
9 x 12 = 108
9 x 13 = 117
9 x 14 = 126
9 x 15 = 135
9 x 16 = 144
9 x 17 = 153
9 x 18 = 162
9 x 19 = 171
9 x 20 = 180

Tabla de multiplicar del 10
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
10 x 11 = 110
10 x 12 = 120
10 x 13 = 130
10 x 14 = 140
10 x 15 = 150
10 x 16 = 160
10 x 17 = 170
10 x 18 = 180
10 x 19 = 190
10 x 20 = 200
```

***

## REPASO:

```python
#Ejercicio 1
#Haz que el usuario introduzca números enteros por teclado. Mientras el usuario no introduzca el 0, muestra
#si el número introducido es par o impar.

print("+ Introduzca numeros y el programa le dirá si son pares o impares. Para salir introduzca el 0.")
n = 1

while n != 0:
    n = int(input("+Introduzca un número: "))
    if n % 2 == 0:
        print("+ El número {} es par".format(n))
    else:
        print("+ El número {} es impar".format(n))
else:
    print("- Saliendo!")
```

```
#RESPUESTA
+ Introduzca numeros y el programa le dirá si son pares o impares. Para salir introduzca el 0.
+Introduzca un número: 0
+ El número 0 es par
- Saliendo!
```

```python
#Ejercicio 2
#Haz que el usuario introduzca una palabra y una letra por teclado. Comprueba si la palabra contiene la
#letra o no e indícaselo al usuario por pantalla.

print("Introduzca una palabra y una letra. El programa le dirá si la frase la contiene.")
w = input("Escriba su frase: ").lower()
l = input("Escriba su letra: ").lower()

for c in w:
    if c == l:
        print("La letra {} aparece en la palabra {}".format(l,w))
        break
else:
    print("La letra {} NO aparece en la palabra {}".format(l,w))
```

```
#RESPUESTA
Introduzca una palabra y una letra. El programa le dirá si la frase la contiene.
Escriba su frase: HOLA
Escriba su letra: A
La letra a aparece en la palabra hola
```

```python
#Ejercicio 3
#Haz que el usuario introduzca precios por teclado (si introduce 0, entonces es que ha finalizado). Si el usuario
#pasa de 200€, entonces ya no debe poder introducir más precios pues se ha pasado de presupuesto. Sea cual
#sea el resultado (o bien el precio final o bien que no tiene más presupuesto), indícaselo por pantalla al usuario.

print("Introduzca precios para comprobar si se pasa de presupuesto (200€). Para finalizar introduzca 0")
count = 0

while count < 200:
    n = int(input("Introduzca un valor: "))
    if n == 0:
        print(count, "\n- Saliendo!")
        break
    else:
        count += n
else:
    print("Se ha pasado del presupuesto.")

print("Se ha gastado: {}".format(count))
```

```
#RESPUESTA
Introduzca precios para comprobar si se pasa de presupuesto (200€). Para finalizar introduzca 0
Introduzca un valor: 5
Introduzca un valor: 6
Introduzca un valor: 200
Se ha pasado del presupuesto.
Se ha gastado: 211
```

```python
#Ejercicio 4
#Haz que el usuario introduzca números enteros por teclado. Mientras el usuario no introduzca el 0, calcula
#cuántos números positivos y cuántos negativos ha introducido y muéstraselo al final.

print("Introduzca numeros enteros y el programa le dirá cuantos número positivos y cuantos negativos ha introducido. 0 para salir.")
count_pos = 0
count_neg = 0
n = 1

while n != 0:
    n = int(input("Introduzca un número entero: "))
    if n > 0:
        count_pos += 1
    elif n < 0:
        count_neg += 1
print("Ha introducido un total de {} numeros positivos".format(count_pos))
print("Ha introducido un total de {} numeros negativos".format(count_neg))
```

```
#RESPUESTA
Introduzca numeros enteros y el programa le dirá cuantos número positivos y cuantos negativos ha introducido. 0 para salir.
Introduzca un número entero: 1
Introduzca un número entero: 2
Introduzca un número entero: 3
Introduzca un número entero: 5
Introduzca un número entero: -1
Introduzca un número entero: -2
Introduzca un número entero: -3
Introduzca un número entero: 0
Ha introducido un total de 4 numeros positivos
Ha introducido un total de 3 numeros negativos
```

```python
#Ejercicio 5
#Haz que el usuario introduzca números por teclado. Mientras el usuario no introduzca el 0, pídele otro
#número. Cuando el usuario introduzca el 0, muéstrale la media aritmética de los números que ha introducido.

print("Introduzca numeros enteros y el programa le dirá la media aritmética de los números que ha introducido. 0 para salir.")
n = 1
count = 0
suma = 0

while n != 0:
    n = float(input("Introduzca un número: "))
    if n == 0:
        continue
    else:
        count += 1
        suma += n
print("La media aritmética de los números introducidos es: {}".format(suma / count))
```

```
#RESPUESTA
Introduzca numeros enteros y el programa le dirá la media aritmética de los números que ha introducido. 0 para salir.
Introduzca un número: 5
Introduzca un número: 5
Introduzca un número: 5
Introduzca un número: 5
Introduzca un número: 5
Introduzca un número: 5
Introduzca un número: 0
La media aritmética de los números introducidos es: 5.0
30.0
6
```

```python
#Ejercicio 6
#Haz que el usuario introduzca dos números enteros por teclado. El primero será el extremo izquierdo del
#intervalo y, el segundo, el extremo derecho. Imprime todos los números que se encuentren entre los dos
#números introducidos por el usuario (los extremos incluidos).

print("Introduzca dos números que formarán un intervalo. Se imprimirán todos los números del intervalo")
a = int(input("Introduzca el número a del intervalo [a, b]: "))
b = int(input("Introduzca el número b del intervalo [a, b]: "))

for c in range(a, b + 1):
    print(c)
```

```
#RESPUESTA
Introduzca dos números que formarán un intervalo. Se imprimirán todos los números del intervalo
Introduzca el número a del intervalo [a, b]: 5
Introduzca el número b del intervalo [a, b]: 6
5
6
```

```python
#Ejercicio 7
#Haz que el usuario introduzca dos números enteros por teclado. El primero será el extremo izquierdo del
#intervalo y, el segundo, el extremo derecho. Imprime la suma de todos los múltiplos de 3 que se encuentren
#entre los dos números introducidos por el usuario (los extremos incluidos). Finalmente, muestra por pantalla
#el resultado de la suma.

print("Introduzca dos números que formarán un intervalo. Se imprimirán la suma de todos los numeros multiplos de tres en el intervalo.")
suma = 0
a = int(input("Introduzca el número a del intervalo [a, b]: "))
b = int(input("Introduzca el número b del intervalo [a, b]: "))

for c in range(a, b + 1):
    if c % 3 == 0:
        suma += c
print("La suma de todos los numeros múltiplos de 3 es: {}".format(suma))
```

```
#RESPUESTA
Introduzca dos números que formarán un intervalo. Se imprimirán la suma de todos los numeros multiplos de tres en el intervalo.
Introduzca el número a del intervalo [a, b]: 0
Introduzca el número b del intervalo [a, b]: 30
La suma de todos los numeros múltiplos de 3 es: 165
```

```python
#Ejercicio 8
#Pídele al usuario cuántos números va a introducir. Con un bucle for, solicítale esa cantidad de números y
#calcula su producto.

print("Introduzca la cantidad de numeros que quiere multiplicar y luego el programa se los pedirá uno a uno.")
n = int(input("Escriba la cantidad de numeros a multiplicar: "))
mul = 1

for c in range(n):
    n2 = int(input("numero a multiplicar: "))
    mul *= n2
print("La multiplicación de ellos es: {}".format(mul))
```

```
#RESPUESTA
Introduzca la cantidad de numeros que quiere multiplicar y luego el programa se los pedirá uno a uno.
Escriba la cantidad de numeros a multiplicar: 2
numero a multiplicar: 2
numero a multiplicar: 3
La multiplicación de ellos es: 6
```

```python
#Ejercicio 9
#Haz que el usuario introduzca su edad y el año actual. Imprime todos los años que han pasado desde su año
#de nacimiento hasta el año actual (ambos incluidos).

print("Introduzca su edad y el año actual y el programa imprimirá todos los años que ha vivido.")
edad = int(input("Su edad: "))
act = int(input("Año actual: "))

for c in range(act, act - edad - 1, -1):
    print(c)
```

```
#RESPUESTA
Introduzca su edad y el año actual y el programa imprimirá todos los años que ha vivido.
Su edad: 27
Año actual: 2021
2021
2020
2019
2018
2017
2016
2015
2014
2013
2012
2011
2010
2009
2008
2007
2006
2005
2004
2003
2002
2001
2000
1999
1998
1997
1996
1995
1994
```

```python
#Ejercicio 10
#Haz que el usuario introduzca un número entero. Muestra un cuadrado y luego un triángulo rectángulo de
#lado y altura, respectivamente, el número entero introducido. Por ejemplo, si el usuario introduce como
#número 5, se deberá mostrar:

print("Introduzca un número y el programa representará un triangulo rectángulo y un cuadrado con esa medida.")
n = int(input("Lado: "))
for c in range(n):
    print((c + 1) * "*")
print("\n")
for c in range(n):
    print(n * "*")
```

```
#RESPUESTA
Introduzca un número y el programa representará un triangulo rectángulo y un cuadrado con esa medida.
Lado: 5
*
**
***
****
*****


*****
*****
*****
*****
*****
```

```python
#Ejemplo de otra alumna que lo hace mejor que yo.
n = int(input("Ingresé número a graficar: "))

for i in range(1, n + 1):
    print(("* " * i) + " " + ((" " * len("* " * (n - i))) + ("* " * n)))
```

```
#RESPUESTA
Ingresé número a graficar: 5
*          * * * * * 
* *        * * * * * 
* * *      * * * * * 
* * * *    * * * * * 
* * * * *  * * * * * 
```
