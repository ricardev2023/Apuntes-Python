---
description: Explicación de las operaciones básicas en Python.
---

# Tema 2. Números en Python

## Tipos de números

* `int`: número entero
* `float`: número en coma flotante

Para saber el tipo de dato de un número podemos utilizar la función `type()`

```python
type(5)

#RESPUESTA
int
```

```python
type(5.0)

#RESPUESTA
float
```

**Observación.** En `Python`, para referirnos a números de tipo `float` con todo 0's en la parte decimal como `3.0`, basta que indiquemos `3.`. Es decir, `Python` entiende que los números `3.0` y `3.` son el mismo, incluyendo que son del mismo tipo: `float`.

```python
type(3.0)

#RESPUESTA
float
```

```python
type(3.)

#RESPUESTA
float
```

**Casting**: Podemos indicar el tipo de número que deseamos utilizar con las funciones `int()` y `float()`.

```python
type(int(7.0))

#RESPUESTA
int
```

```python
type(int(9.))

#RESPUESTA
int
```

```python
type(float(3))

#RESPUESTA
float
```

**¡Cuidado!** Es sencillo pasar de enteros a números en coma flotante, ya que siempre es posible, pero no siempre podemos pasar de números en coma flotante a números enteros, pues se pierde la parte decimal.

```python
int(3.5)

#RESPUESTA
3
```

## Operaciones aritméticas

### Suma

Para sumar dos números, utilizamos la función `+`

```python
2 + 1

#RESPUESTA
3
```

```python
2.0 + 1.

#RESPUESTA
3.0
```

```python
2 + 1.0

#RESPUESTA
3.0
```

**Observación.** Fijémonos que al combinar un número entero (int) y un número en coma flotante (float), el resultado es un número float. Esto ocurre para todas las operaciones aritméticas en `Python`.

### Resta

Para restar dos números, utilizamos la función `-`

```python
7 - 3

#RESPUESTA
4
```

```python
7.0 - 3.

#RESPUESTA
4.0
```

```python
7 - 3.0

#RESPUESTA
4.0
```

### Producto

Para multiplicar dos números, utilizamos la función `*`

```python
8 * 6

#RESPUESTA
48
```

```python
8. * 6.

#RESPUESTA
48.0
```

```python
8.0 * 6

#RESPUESTA
48.0
```

### División

Para dividir dos números, utilizamos la función `/`

```python
6 / 5

#RESPUESTA
1.2
```

```python
6. / 5.0

#RESPUESTA
1.2
```

```python
6 / 5.0

#RESPUESTA
1.2
```

**¡Cuidado!** Hay que tener en cuenta el tipo de número (int o float) cuando vayamos a dividir en `Python`, porque en algunas versiones (por debajo de la 3.6), si dividimos dos números enteros, se lleva a cabo la **división entera** automáticamente.

**CONSEJO:** Es una buena costumbre utilizar siempre un numero FLOAT si queremos asegurarnos que no se realiza la división entera.

#### División entera o Euclídea

Dados dos números naturales $a$ y $b$, con $b \ne 0$, la división Euclídea de $a$ entre $b$ asocia un cociente $q$ y un resto $r$, ambos números naturales, que satisfacen

* $a = b \cdot q + r$
* $r < b$

***

#### **Ejemplo 1**

Si queremos la división entera de $a = 7$ entre $b = 5$, tendremos que el cociente es $q = 1$ y el resto es $r = 2$, ya que

$$7 = 5\cdot 1 + 2$$

y el resto $r$ es menor al divisor $b$. Es decir, $2 < 5$.

***

Para obtener el **cociente** de la división entera, utilizamos la función `//`

```python
10 // 3

#RESPUESTA
3
```

Para obtener el **resto** de la división entera, utilizamos la función `%`

```python
10 % 3

#RESPUESTA
1
```

### Potencia

Para calcular la potencia $n$-ésima de un número, usamos la función `**`

```python
5 ** 3

#RESPUESTA
125
```

```python
5.0 ** 3.0

#RESPUESTA
125.0
```

```python
5.0 ** 3

#RESPUESTA
125.0
```

Para calcular la potencia $n$-ésima de un número, también podemos usar la función `pow()`

```python
pow(5, 3)

#RESPUESTA
125
```

```python
pow(5., 3.0)

#RESPUESTA
125.0
```

```python
pow(5, 3.)

#RESPUESTA
125.0
```

## Orden de las operaciones aritméticas

El orden en que se llevan a cabo las operaciones aritméticas en `Python` es el siguiente:

* Primero se calcula lo que se halla entre paréntesis.
* A continuación, las potencias.
* Después, productos y divisiones. En caso de haber varias, el orden que se sigue es de izquierda a derecha.
* Finalmente, sumas y restas. En caso de haber varias, el orden que se sigue es de izquierda a derecha.

```python
6 + 2 * 8 / 4 - 2 ** 3

#RESPUESTA
2.0
```

```python
(6 + 2) * (8 / (4 - 2)) ** 3

#RESPUESTA
512.0
```

```python
(6 + 2) * 8 / (4 - 2) ** 3

#RESPUESTA
8.0
```

**Observación.** El uso de los paréntesis puede cambiar completamente el resultado. No conviene abusar de ellos, aunque es mejor que sobren, ya que ayudan a entender el orden en que se van a llevar a cabo las operaciones.

## Números complejos

### Definiciones

* **Número complejo.** Es un par ordenado de números reales $z = (a, b)$, con $a,b\in\mathbb{R}$.
* **Parte real.** Es el primer elemento del par ordenado, $\text{Re}(z) = a$.
* **Parte imaginaria.** Es el segundo elemento del par ordenado, $\text{Im}(z) = b$.
* **Complejo real.** $z = (a, 0)$.
* **Imaginario puro.** $z = (0, b)$.
* **Unidad imaginaria.** $i = (0, 1)$.
* **Conjunto de números complejos.** $\mathbb{C} = {z = (a,b)\ :\ a,b\in\mathbb{R}}$.

### Operaciones

* Suma: $(a, b) + (c, d) = (a + c, b + d)$
* Resta: $(a, b) - (c, d) = (a - c, b - d)$
* Producto: $(a, b) \cdot (c, d) = (a \cdot c - b \cdot d, a\cdot d + b\cdot c)$
* División: $(a, b) \div (c, d) = \frac{(a \cdot c + b \cdot d, b \cdot c - a \cdot d)}{c^2 + d^2} = \left(\frac{a \cdot c + b \cdot d}{c^2 + d^2},\frac{b \cdot c - a \cdot d}{c^2 + d^2}\right)$

### Conjugado, Módulo y Argumento

Dado un complejo $z = (a,b)$,

* **Conjugado.** $\bar{z} = (a, -b)$.
* **Módulo.** $\text{Mod}(z) = |z| = \sqrt{\text{Re}(z)^2 + \text{Im}(z)^2} = \sqrt{a^2 + b^2}$.
* **Argumento.** $\text{Arg}(z) = \arctan\left(\frac{\text{Im}(z)}{\text{Re}(z)}\right) = \arctan\left(\frac{b}{a}\right)$

### Unidad imaginaria

$i = (0, 1)$ satisface

$$i^2 = (0, 1)^2 = (0, 1)\cdot (0, 1) = (-1, 0)$$

De aquí obtenemos la igualdad $i = \sqrt{-1}$, que es otra de las definiciones que se le da a la unidad imaginaria.

### Otras representaciones

Representación binómica: $z = a + bi$

* $a = \text{Re}(z)$
* $b = \text{Im}(z)$

Representación polar: $z = re^{i\phi}$

* $r = \text{Mod}(z)$
* $\phi = \text{Arg}(z)$

### Números complejos en `Python`

**Observación.** En `Python`, los números complejos se definen en forma binómica y en vez de utilizar una `i`, se utiliza la letra `j` para representar la unidad imaginaria.

```python
z = 2 + 5j
z

#RESPUESTA
(2+5j)
```

```python
type(z)

#RESPUESTA
complex
```

También podemos definir números complejos en `Python` con la función `complex()`

```python
z = complex(1, -7)
z

#RESPUESTA
(1-7j)
```

```python
type(z)

#RESPUESTA
complex
```

Para obtener la parte real, utilizamos el método `.real`

```python
z.real

#RESPUESTA
1.0
```

Para obtener la parte imaginaria, utilizamos el método `.imag`

```python
z.imag

#RESPUESTA
-7.0
```

Para sumar números complejos, utilizamos la función `+`

```python
z1 = 2-6j
z2 = 5+4j

z1 + z2

#RESPUESTA
(7-2j)
```

Para restar números complejos, utilizamos la función `-`

```python
z1 - z2

#RESPUESTA
(-3-10j)
```

Para multiplicar una constante por un número complejo, o bien multiplicar dos números complejos, utilizamos la función `*`

```python
-1 * z1

#RESPUESTA
(-2+6j)
```

```python
z1 * z2

#RESPUESTA
(34-22j)
```

Para dividir números complejos, utilizamos la función `/`

```python
z1 = -1 - 1j
z2 = 1 - 1j

z1 / z2

#RESPUESTA
-1j
```

**Observación.** Si queremos indicar que la parte imaginaria es 1 o -1, no basta con poner `j` o `-j`, sino que hay que escribir `1j` o `-1j`, siempre que definamos el número complejo en su forma binómica.

Para calcular el conjugado de un número complejo, utilizamos el método `.conjugate()`

```python
z = -2 + 1j
z.conjugate()

#RESPUESTA
(-2-1j)
```

Para calcular el módulo de un número complejo, utilizamos la función `abs()`

```python
z = -2j
abs(z)

#RESPUESTA
2.0
```

Para calcular el módulo de un número complejo, utilizamos la función `abs()`

```python
z = -2j
abs(z)

#RESPUESTA
2.0
```

Para calcular el argumento de un número complejo, utilizamos la función `phase()` del paquete `cmath`.

```python
import cmath
cmath.phase(z)

#RESPUESTA
-1.5707963267948966
```

Para pasar de forma binómica a forma polar, usamos la función `polar()` del paquete `cmath`.

```python
z

#RESPUESTA
(-0-2j)
```

Como Vemos en el siguiente ejemplo, la forma polar se escribe en radianes ($pi/2$ rad)

```python
cmath.polar(z)

#RESPUESTA
(2.0, -1.5707963267948966)
```

Para pasar de forma polar a forma binómica, usamos la función `rect()` del paquete `cmath`.

```python
cmath.rect(abs(z), cmath.phase(z))

#RESPUESTA
(1.2246467991473532e-16-2j)
```

La parte real calculada por Python no es exactamente cero, ya que el error del sistema (a causa de la memoria finita que impide guardar todos los decimales del número pi) hace que se obtenga una pequeña cantidad en la parte real.

## TAREA DE REPASO

```python
# EJERCICIO 1:
#Calcula la división entera de 45 entre 6

45 // 6


#RESPUESTA
7
```

```python
#Ejercicio 2
#Calcula el resto de la división entera de 45 entre 6
45%6

#RESPUESTA
3
```

```python
#Ejercicio 3
#Realiza la siguiente operación en Python, donde ÷ indica la división entera:

10+20//7-2

#RESPUESTA
10
```

```python
#Ejercicio 4
#Realiza la siguiente operación en Python:

(9-(25+5-2)/(7*4))/2**3

#RESPUESTA
1.0
```

```python
#Ejercicio 5
#Realiza la siguiente operación en Python:

(2+2**3-2*(2-2**5)+2**2*2+2)/(2*(2*2-2**4)+2**2)

#RESPUESTA
-4.0
```

```python
#jercicio 6
#Realiza la siguiente operación en Python:

z = 6j
k = 4 + 1j
z-k*2

#RESPUESTA
(-8+4j)
```

```python
#Ejercicio 7
#Realiza la siguiente operación en Python:

((1+1j)/(1-1j))+(2/(-1+1j))

#RESPUESTA
(-1+0j)
```

```python
#Ejercicio 8
#Realiza la siguiente operación en Python:

(1+1j)**2

#RESPUESTA
2j
```

```python
#Ejercicio 9
#Realiza la siguiente operación en Python, donde Mod(z) indica módulo del complejo z:

z = ((9-3j)/(-2-1j))
abs(z)

#RESPUESTA
4.242640687119285
```

```python
#Ejercicio 10
#¿Cuál es el argumento del número complejo i?

import cmath 
z = 1j
cmath.phase(z) 

#RESPUESTA
1.5707963267948966
```
