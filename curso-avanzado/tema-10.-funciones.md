---
description: Explicación y conceptos básicos de la definición de Funciones en Python 3.
---

# Tema 10. Funciones

## Función

**Función.** Una función en `Python` es una pieza de código reutilizable que solo se ejecuta cuando es llamada.

Se define usando la palabra reservada `def` y estructura general es la siguiente:

```python
def nombre_funcion(input1, input2, ..., inputn):
  cuerpo de la función
  return output
```

**Observación.** La instrucción `return` finaliza la ejecución de la función y devuelve el resultado que se indica a continuación. Si no se indicase nada, la función finalizaría, pero no retornaría nada.

Como hemos visto, en general, las funciones constan de 3 partes:

* **Inputs (parámetros o argumentos).** Son los valores que le pasamos como entrada a la función.
* **Cuerpo.** Son todas las operaciones que lleva a cabo la función.
* **Output.** Es el resultado que devuelve la función.

**Observación.** Los parámetros son variables internas de la función. Si probásemos a ejecutar una de dichas variables en el entorno global, nos saltaría un error. Este tema lo trataremos más en detalle más adelante.

Con lo visto anteriormente, a la hora de construir una función hau que hacerse las siguientes preguntas:

* ¿Qué datos necesita conocer la función? (inputs)
* ¿Qué hace la función? (cuerpo)
* ¿Qué devuelve? (output)

**Observación.** Los inputs y el output son opcionales: podemos definir una función sin necesidad de proporcionarle inputs y sin que nos devuelva nada.

Una vez definida una función, para llamarla utilizamos su nombre seguido de paréntesis:

```python
def my_first_function():
    print("Tu primera función te saluda")
```

```python
my_first_function()

#RESPUESTA
Tu primera función te saluda
```

Hemos dicho que tanto los inputs como el output son opcionales. Veamos algunos ejemplos con diferentes casos.

#### **Ejemplo 1**

Veamos otro ejemplo que no necesite ningún parámetro y no nos devuelva nada, tal y como ocurría con `my_first_function()`

```python
def hello_world():
  print("Hola mundo!")
```

```python
hello_world()

#RESPUESTA
Hola mundo!
```

Nuestra función `hello_world()`, cuando es llamada, imprime "Hola mundo!", pero no devuelve absolutamente nada.

#### **Ejemplo 2**

Veamos un ejemplo de función que no necesita ningún input, pero que devuelve un output. Por ejemplo, una función que nos devuelve "¡Buenos días!"

```python
def good_morning():
    return "Buenos días"
```

Ya hemos declarado la función. Si la llamamos, obtenemos el siguiente resultado:

```python
good_morning()

#RESPUESTA
'Buenos días'
```

Como nos devuelve el saludo, lo podemos guardar en una variable, que será de tipo string

```python
goodMorning = good_morning()
print(goodMorning)
print(type(goodMorning))

#RESPUESTA
Buenos días
<class 'str'>
```

#### **Ejemplo 3**

Veamos ahora un ejemplo de función que no nos devuelva nada, pero que sí toma algún parámetro

```python
def good_morning(name):
  print("¡Buenos días, {}!".format(name))
```

```python
good_morning(name = "Don Pepito")
good_morning(name = "Don José")

#RESPUESTA
¡Buenos días, Don Pepito!
¡Buenos días, Don José!
```

```python
good_morning("María")

#RESPUESTA
¡Buenos días, María!
```

Ahora nuestra función `good_morning()` recibe como parámetro un nombre y nos muestra por pantalla un "¡Buenos días!" junto con el nombre indicado.

#### **Ejemplo 4**

Por último, vamos a crear una función que nos calcule la división entera de dos números y nos retorne el cociente y el resto.

```python
def euclidean_division(x, y):
  q = x // y
  r = x % y
  return q, r
```

Esta función, a la que hemos llamado `euclidean_division`, calcula el cociente y el resto de dos números cualesquiera y devuelve como resultado esos dos números calculados.

Utilicemos ahora nuestra función para calcular el cociente y el resto de la división **41÷ 7** euclidean\_division(x = 41, y = 7)

```python

#RESPUESTA
(5, 6)
```

```python
euclidean_division(41, 7)

#RESPUESTA
(5, 6)
```

```python
euclidean_division(y = 7, x = 41)

#RESPUESTA
(5, 6)
```

Al llamar a la función e indicarle por parámetros `x = 41` e `y = 7`, hemos obtenido como resultado la tupla `(5, 6)`. El significado de dicho resultado es que el cociente entero de **41 ÷ 7** es 5, mientras que el resto es **6**. Efectivamente:

$$41 = 7\cdot 5 + 6$$

También podríamos guardar en variables diferentes los resultados que nos devuelve nuestra función, para poder trabajar con ellos en el entorno global

```python
quotient, remainder = euclidean_division(x = 41, y = 7)
print(quotient)
print(remainder)
print(41 == 7 * quotient + remainder)
```

```
#RESPUESTA
5
6
True
```

#### EJERCICIO 1:

&#x20;Vamos a crear una función que cuente y devuelva todas las apariciones de una letra proporcionada por parámetro en una frase también proporcionada por parámetro.

```python
def letter_counter(frase, letra):
    frase = frase.lower()
    count = frase.count(letra)
    return count

letter_counter("hoy no me puedo levantar", "o")
```

```
3
```

## Parámetros

Por defecto, una función debe ser llamada con el número correcto de argumentos. Esto es, si la función espera 2 argumentos, tenemos que llamar a la función con esos 2 argumentos. Ni más, ni menos.

```python
def complete_name(name, surname):
  print("El nombre completo es", name, surname)
```

```python
complete_name("María", "Santos")

#RESPUESTA
El nombre completo es María Santos
```

```python
complete_name("Juan Gabriel", "Gomila")

#RESPUESTA
El nombre completo es Juan Gabriel Gomila
```

Si intentamos llamar a la función `complete_name()` pasando 1 solo parámetro o 3 parámetros, entonces la función devuelve error.

```python
complete_name(name = "María")

#RESPUESTA
TypeError: complete_name() missing 1 required positional argument: 'surname'
```

```python
complete_name("Juan", "Gabriel", "Gomila")

#RESPUESTA
TypeError: complete_name() takes 2 positional arguments but 3 were given
```

### Número arbitrario de argumentos

Si no sabemos el número de parámetros que van a ser introducidos, entonces añadimos un asterisco `*` previo al nombre del parámetro en la definición de la función. Los valores introducidos serán guardados en una **tupla**.

```python
def sum_numbers(*numbers):
  sum = 0
  for n in numbers:
    sum += n
  
  return sum
```

```python
sum_numbers(1, 2, 3)

#RESPUESTA
6
```

```python
sum_numbers(2, 4, 6, 8, 10)

#RESPUESTA
30
```

### Número arbitrario de claves de argumento

Hasta ahora hemos visto que al pasar valores por parámetro a la función, podemos hacerlo con la sintaxis `clave_argumento = valor` o directamente pasar por parámetro el valor siguiendo el orden posicional de la definición de la función:

```python
def complete_name(name, surname):
  print("El nombre completo es", name, surname)
```

```python
complete_name(name = "María", surname = "Santos")

#RESPUESTA
El nombre completo es María Santos
```

```python
complete_name(surname = "Santos", name = "María")

#RESPUESTA
El nombre completo es María Santos
```

```python
complete_name("María", "Santos")

#RESPUESTA
El nombre completo es María Santos
```

En realidad, los nombres completos pueden tener dos o incluso más apellidos, pero no sabemos si el usuario tiene 1 o 2 o más. Entones, podemos añadir dos asteriscos `**` antes del nombre del parámetro para así poder introducir tantos como queramos sin que salte error

```python
def complete_name(name, **surname):
    print("El nombre completo es {}".format(name), end = " ")
    for i in surname.items():
      print("{}".format(i[1]), end = " ")
```

```python
complete_name(name = "María", surname1 = "Santos", surname2 = "Fernández")

#RESPUESTA
El nombre completo es María Santos Fernández 
```

```python
complete_name(name = "María", surname = "Santos")

#RESPUESTA
El nombre completo es María Santos 
```

### Parámetros por defecto

Hemos visto que una función en `Python` puede tener o no parámetros.

En caso de tener, podemos indicar que alguno tenga un valor por defecto.

La función `diff()` calcula la diferencia entre los dos números que introducimos por parámetros. Podemos hacer que el sustraendo por defecto valga 1 del siguiente modo:

```python
def diff(x, y = 1):
  return x - y
```

```python
diff(65, 18)

#RESPUESTA
47
```

Si ahora llamamos a la función indicando únicamente el valor del parámetro `x`, ocurre lo siguiente:

```python
diff(x = 20)

#RESPUESTA
19
```

Como resultado hemos obtenido 19, ya que el valor que ha tomado el parámetro `y` ha sido el que le hemos dicho que tome por defecto, es decir, $y = 1$ y, consecuentemente, $x-y = 20-1 = 19$

#### EJERCICIO 2

Vamos a crear una función que muestre por pantalla el [triángulo de Pascal](https://es.wikipedia.org/wiki/Tri%C3%A1ngulo\_de\_Pascal). Por parámetro se indicará el número de filas a mostrar. Por defecto `n` valdrá 1.

Para calcular el [número combinatorio](https://es.wikipedia.org/wiki/Coeficiente\_binomial) en `Python`, utilizaremos el siguiente método:

```python
def choose(n, k):
  """
  Calcula el número combinatorio n sobre k
  """
  import math
  if (n >= k and k >= 0):
    return math.factorial(n) / (math.factorial(k) * math.factorial(n - k))
  else:
    return "No se puede calcular el número factorial indicado"
```

```python
def pascal_triangle(n = 1):
  print(1)
  for i in range(1, n + 1):
    for k in range(i + 1):
      print(choose(i, k), end = " ")
    print("")

pascal_triangle(5)
```

```
#RESPUESTA
1
1.0 1.0 
1.0 2.0 1.0 
1.0 3.0 3.0 1.0 
1.0 4.0 6.0 4.0 1.0 
1.0 5.0 10.0 10.0 5.0 1.0 
```

## Docstring

**Docstring.** Son comentarios explicativos que ayudan a comprender el funcionamiento de una función.

* Van entre triple comilla doble.
* Pueden ser multilínea.
* Se sitúan al principio de la definición de la función.

Retomando el ejemplo de la división entera, podríamos utilizar docstring del siguiente modo:

```python
def euclidean_division(x, y):
  """
  Esta función calcula el cociente y el resto de la
  división entera de x entre y.

  Args:
    x (int): dividendo
    y (int): divisor (que no puede ser cero)

  Returns:
    (q, r): tupla con el valor de (cociente, resto)
  """
  q = x // y
  r = x % y
  return q, r
```

Con la ayuda del método `.__doc__` podemos acceder directamente a la información indicada en el docstring de una función

```python
print(euclidean_division.__doc__)
```

```
#RESPUESTA  
  Esta función calcula el cociente y el resto de la
  división entera de x entre y.

  Args:
    x (int): dividendo
    y (int): divisor (que no puede ser cero)

  Returns:
    (q, r): tupla con el valor de (cociente, resto)
  
```

## Variables de una función

Dentro de una función en `Python` existen dos tipos de variables:

* **Variable local.** Aquella que es creada y solamente existe dentro de la función.
* **Variable global.** Aquella que es creada en el entorno global.

Dada la siguiente función:

```python
def arithmetic_operations(x, y):
  sum = x + y
  diff = x - y
  prod = x * y
  div = x / y
  return {"sum": sum,
          "difference": diff,
          "product": prod,
          "division": div}
```

Si nosotros queremos imprimir por ejemplo el valor que toma la variable `prod` en el entorno global nos saltará un error, pues esta variable no existe a nivel global porque no ha sido declarada en dicho entorno ya que solamente ha sido declarada a nivel local, dentro de la función `arithmetic_operations()`.

```python
print(arithmetic_operations(x = 5, y = 3))

#RESPUESTA
{'sum': 8, 'difference': 2, 'product': 15, 'division': 1.6666666666666667}
```

```python
print(prod)

#RESPUESTA
NameError: name 'prod' is not define
```

Si se diese el caso de que sí hubiese sido definida la variable `prod` en el entorno global, como lo que ocurre en el siguiente bloque de código, por mucho que la variable local tenga el mimso nombre y por mucho que ejecutemos la función, el valor de la variable global no se ve modificado

```python
prod = 10
print(arithmetic_operations(x = 5, y = 3))
print(prod)

#RESPUESTA
{'sum': 8, 'difference': 2, 'product': 15, 'division': 1.6666666666666667}
10
```

Si dentro de una función utilizamos la palabra reservada `global` a una variable local, ésta automáticamente pasa a ser una variable global previamente definida.

Veamos un ejemplo de función que nos devuelve el siguiente número del entero `n` definido en el entorno global:

```python
n = 7

def next_n():
  global n
  return n + 1

next_n()

#RESPUESTA
8
```

### Paso por copia vs. paso por referencia

Dependiendo del tipo de dato que pasemos por parámetro a la función, podemos diferenciar entre

* **Paso por copia.** Se crea una copia local de la variable dentro de la función.
* **Paso por referencia.** Se maneja directamente la variable y los cambios realizados dentro de la función afectan también a nivel global.

En general, los tipos de datos básicos como enteros, en coma flotante, strings o booleanos se pasan por copia, mientras que estructuras de datos como listas, diccionarios, conjuntos o tuplas u otros objetos se pasan por referencia.

Un ejemplo de paso por copia sería:

```python
def double_value(n):
    n = n*2
    return n
```

```python
num = 5
print(double_value(num))
print(num)

#RESPUESTA
10
5
```

Un ejemplo de paso por referencia sería:

```python
def double_values(ns):
  for i, n in enumerate(ns):
    ns[i] *= 2

  return ns
```

```python
nums = [1, 2, 3, 4, 5]
print(double_values(nums))
print(nums)

#RESPUESTA
[2, 4, 6, 8, 10]
[2, 4, 6, 8, 10]
```

Para evitar la modificación de la lista original, podemos hacerlo introduciendo por parámetro una copia de dicha lista

```python
nums = [1, 2, 3, 4, 5]
print(double_values(nums[:]))
print(nums)

#RESPUESTA
[2, 4, 6, 8, 10]
[1, 2, 3, 4, 5]
```

## Funciones más complejas

Las funciones pueden ser más completas, pues admiten tanto operadores de decisión como de iteración.

Volviendo al ejemplo 4, la función creada claramente es muy sencilla, pues suponemos que el usuario va a introducir por parámetros números enteros.

#### **Ejercicio.**&#x20;

Mejora la función `euclidean_division()` para que

* Compruebe que los números introducidos son enteros. En caso de no ser así, indicar que se ha tomado la parte entera de los valores introducidos.
* Realice la división entera del mayor parámetro (en valor absoluto) entre el menor parámetro. Esto es, si el usuario introduce `x = -2` e `y = -10`, como 10 > 2, entonces la función debe llevar a cabo la división entera de -10 entre -2.
* Imprima por pantalla una frase indicando la división realizada y el cociente y el resto obtenidos.
* Devuelva el cociente y el resto a modo de tupla

```python
def euclidean_division(x, y):
  ints = (x == int(x)) and (y == int(y))
  
  if not ints:
    x = int(x)
    y = int(y)
    print("Se tomarán como parámetros la parte entera de los valores introducidos.")
  
  if abs(x) >= abs(y):
    q = x // y
    r = x % y
    print("Se ha realizado la división {} entre {} y se ha obtenido como cociente q = {} y como resto, r = {}".format(x, y, q, r))

  else:
    q = y // x
    r = y % x
    print("Se ha realizado la división {} entre {} y se ha obtenido como cociente q = {} y como resto, r = {}".format(y, x, q, r))


  return q, r
```

```python
quotient, remainder = euclidean_division(x = -10.3, y = -5)

#RESPUESTA
Se tomarán como parámetros la parte entera de los valores introducidos.
Se ha realizado la división -10 entre -5 y se ha obtenido como cociente q = 2 y como resto, r = 0
```

```python
-10 == -5 * quotient + remainder

#RESPUESTA
True
```

```python
euclidean_division(x = -3, y = 19)

#RESPUESTA
Se ha realizado la división 19 entre -3 y se ha obtenido como cociente q = -7 y como resto, r = -2
(-7, -2)
```

#### **Ejemplo 5**

Veamos una función que dado un número, nos dice si éste es positivo, negativo o vale 0.

```python
def sign(num):
  """
  Función que dado un número devuelve el signo positivo, 
  negativo o cero del mismo

  Args:
    num (int): número del cual queremos hallar su signo

  Returns:
    signo (string): string positivo, negativo o cero
  """
  if num > 0:
    return "Positivo"
  elif num < 0:
    return "Negativo"
  else:
    return "Cero"
```

```python
print(sign(num = 3.1415))

#RESPUESTA
Positivo
```

```python
print(sign(num = -100))

#RESPUESTA
Negativo
```

```python
print(sign(num = 0))

#RESPUESTA
Cero
```

#### **Ejemplo 6**

Veamos ahora una función que contiene un bucle `for` y que dado un número entero, nos imprime su tabla de multiplicar con sus 10 primeros múltiplos y nos devuelve una lista con todos esos múltiplos:

```python
def multiplication_table10(num):
  """
  Dado un número entero, imprimimos su tabla de multiplicar con
  los 10 primeros múltiplos y devolvemos una lista de los múltiplos. 

  Args:
    num (int): valor del cual vamos a calcular sus tabla de multiplicar

  Returns: 
    multiples (list): lista con los 10 primeros múltiplos de num
  """
  multiples = []
  print("La tabla de multiplicar del {}:".format(num))
  
  for i in range(1, 11):
    multiple = num * i
    print("{} x {} = {}".format(num, i, multiple))
    multiples.append(multiple)
  
  return multiples
```

```python
multiples7 = multiplication_table10(num = 7)
print(multiples7)
```

```
#RESPUESTA
7  x  1  =  7
7  x  2  =  14
7  x  3  =  21
7  x  4  =  28
7  x  5  =  35
7  x  6  =  42
7  x  7  =  49
7  x  8  =  56
7  x  9  =  63
7  x  10  =  70
[7, 14, 21, 28, 35, 42, 49, 56, 63, 70]
```

Vamos ahora a mejorar la función `multiplication_table10()` para que si el usuario decide introducir un número que no sea entero, nuestra función le avise y le explique el error que está cometiendo:

```python
def multiplication_table10(num):
  """
  Dado un número entero, primero comprovamos si es entero. 
  Si no lo es, no devolvemos nada.
  Si lo es, imprimimos su tabla de multiplicar con los 10 
  primeros múltiplos y devolvemos una lista de los múltiplos. 

  Args:
    num (int): valor del cual vamos a calcular sus 10 primeros múltiplos

  Returns: 
    multiples (list): lista con los 10 primeros múltiplos de num
  """

  if type(num) != type(1):
    print("El número introducido no es entero")
    return

  multiples = []
  print("La tabla de multiplicar del {}:".format(num))
  
  for i in range(1, 11):
    multiple = num * i
    print("{} x {} = {}".format(num, i, multiple))
    multiples.append(multiple)
  
  return multiples
```

```python
multiples3 = multiplication_table10(num = 3)
print(multiples3)
```

```
#RESPUESTA
La tabla de multiplicar del 3:
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
[3, 6, 9, 12, 15, 18, 21, 24, 27, 30]
```

```python
multiples_float = multiplication_table10(num = "3.7")
print(multiples_float)

#RESPUESTA
El número introducido no es entero
None
```

#### **Ejemplo 7**

Creemos ahora una función que dada una frase acabada en punto, nos devuelva si contiene o no la letra "a" haciendo uso de un bucle `while`

```python
#Mi respuesta si no hay a da error.
def letter_a(phrase):
    """
    función que dada una frase acabada en punto, 
    nos devuelva si contiene o no la letra "a"

    Args:
        phrase (string): Una frase terminada en punto.

    Return:
        a (string): "La frase contiene la letra a"
                    "La frase no contiene la a"
    """
    if phrase[-1] != ".":
        print("La frase no termina con un punto")
        return -1
    i = 0
    contain = False
    else:
        while phrase[i] != "a":
            i += 1
        else:
            contain = True
        if contain == True:
            a = "La frase contiene la letra a"
        else:
            a = "La frase NO contiene la letra a"
    return a
            
```

```python
#Ejemplo del profesor
def contains_a(sentence):
  i = 0
  while sentence[i] != ".":
    if sentence[i] == "a":
      return True
    i += 1
  return False
```

```python
contains_a("El erizo es bonito.")

#RESPUESTA
False
```

```python
contains_a("El elefante es gigante.")

#RESPUESTA
True
```

#### **Ejercicio.**&#x20;

Generalizad la función `contains_a()` a una función llamada contains\_letter() que devuelva si una frase cualquiera (no necesariamente acabada en punto) contiene o no la letra indicada también por el usuario. Tenéis que hacerlo únicamente con operadores de decisión e iteración. No vale usar ningún método existente de `string`.

```python
def contains_letter(sentence, letter):
  for c in sentence:
    if c == letter:
      return True
  return False

contains_letter("Mi amigo es muy inteligente, pero un poco pesado", "t")

#RESPUESTA
True
```

## Funciones recursivas

**Función recursiva.** Es una función que se llama a sí misma.

**¡Cuidado!** Hay que tener mucho cuidado con este tipo de funciones porque podemos caer en un bucle infinito. Es decir, que la función no acabara nunca de ejecutarse.

Una función recursiva que entraría en bucle infinito sería la siguiente.

```python
def powers(x, n):
  print(x ** n)
  powers(x, n + 1)
```

¿Por qué decimos que entra en bulce infinito? Pues porque solo parará si nosotros interrumpimos la ejecución.

Esto se debe a que no le hemos indicado un caso de parada a la función, denominado caso final.

**Caso final.** Es el caso que indica cuándo debe romperse la recursión. Hay que indicarlo siempre para no caer en un bucle infinito.

En el caso de la función `powers()`, podemos indicar como caso final cuando el valor resultante supere 1000000. Lo indicamos con un `if`

```python
def powers(x, n):
  if x ** n > 1000000:
    return x ** n

  print(x ** n)
  powers(x, n + 1)
```

```python
powers(2, 1)
```

```
#RESPUESTA
2
4
8
16
32
64
128
256
512
1024
2048
4096
8192
16384
32768
65536
131072
262144
524288
```

#### EJERCICIO 3:&#x20;

Vamos a crear una función recursiva que lleve a cabo una cuenta atrás.

```python
def countdown(initial):
    """
    Función recursiva que lleva a cabo una cuenta atrás.

    Args:
        initial (int): Número desde el que empezamos la cuenta atrás.

    Return:
        countdown(initial - 1): Para que siga bajando.
    """
    if initial == 0:
       return 0
    else:
        print(initial)
    return(countdown(initial - 1))
```

```python
countdown(10)

#RESPUESTA
10
```

#### EJERCICIO 4:&#x20;

Vamos a crear una función recursiva que calcule el factorial de un número entero positivo.

```python
def factorial(n):
    """
    función recursiva que calcule el factorial 
    de un número entero positivo.

    Args:
        n (int +): número del que calculamos el 
        factorial.

    Return:
        factorial(n - 1): para sacar el factorial 
        completo.
    """
    if n < 0:
        print("No es un número positivo.")
        return -1
    elif n == 0:
        return 1
    else:
        return n * factorial (n - 1)
```

```python
factorial(4)

#RESPUESTA
24
```

#### Ejemplo 8

Veamos ahora un ejemplo clásico de función recursiva que funciona correctamente.

Queremos una función que nos imprima el término i-ésimo de la sucesión de Fibonacci. Es decir, nosotros le indicamos el índice del término y la función nos devuelve el valor de dicho término.

La sucesión de Fibonacci es

$$1, 1, 2, 3, 5, 8, 13,\dots$$

Es decir, cada término se obtiene de la suma de los dos anteriores.

$$F_0 = F_1 = 1$$ $$F_n = F_{n-1} + F_{n-2}, n\geq 2$$

Con lo cual, la función que queremos y a la que hemos llamado `Fibonacci()` es:

```python
def Fibonacci(index):
  if index == 0 or index == 1:
    return 1
  
  return Fibonacci(index - 1) + Fibonacci(index - 2) 
```

Como veis, le hemos indicado a la función cuando parar. Esto es, el caso final resulta ser cuando el índice vale 0, pues no existen índices negativos.

```python
Fibonacci(index = 7)

#RESPUESTA
21
```

```python
Fibonacci(8)

#RESPUESTA
34
```

```python
Fibonacci(30)

#RESPUESTA
1346269
```

#### EJERCICIO 5:&#x20;

Vamos a crear una función que resuelva ecuaciones de primer grado de la forma Ax+B=0 siempre que A≠0 .

```python
def first_grade_eq(A, B):
    """
    Función que resuelva ecuaciones de primer grado 
    de la forma  Ax+B=0  siempre que  A≠0 .

    Args:
        A (int != 0)
        B (int)

    Return:
        result (float): Resultado de la operación.    
    """
    if A == 0:
        print("No se cumplen las normas.")
        return -1
    else:
        result = float(-B / A)
    return result
```

```python
first_grade_eq(4, -4)

#RESPUESTA
1.0
```

## Funciones helper

Al igual que las funciones pueden llamarse a sí mismas, también pueden llamar a otras funciones.

**Función helper.** Es una función cuyo propósito es evitar la repetición de código.

Si nos dan la siguiente función

```python
def sign_sum(x, y):
  if x + y > 0:
    print("El resultado de sumar {} más {} es positivo".format(x, y))
  elif x + y == 0:
    print("El resultado de sumar {} más {} es cero".format(x, y))
  else:
    print("El resultado de sumar {} más {} es negativo".format(x, y))
```

```python
sign_sum(5, 4)
sign_sum(3, -3)
sign_sum(1, -8)
```

```
#RESPUESTA
El resultado de sumar 5 más 4 es positivo
El resultado de sumar 3 más -3 es cero
El resultado de sumar 1 más -8 es negativo
```

Vemos que el `print` se repite salvo por la última palabra.

Podríamos pensar en crear la función helper siguiente:

```python
def helper_print(x, y, sign):
  print("El resultado de sumar {} más {} es {}.".format(x, y, sign))
```

Si utilizamos la función helper, la función `sign_sum()` quedaría modificada del siguiente modo:

```python
def sign_sum(x, y):
  if x + y > 0:
    helper_print(x, y, "positivo")
  elif x + y == 0:
    helper_print(x, y, "cero")
  else:
    helper_print(x, y, "negativo")
```

```python
sign_sum(5, 4)
sign_sum(3, -3)
sign_sum(1, -8)
```

```
#RESPUESTA
El resultado de sumar 5 más 4 es positivo.
El resultado de sumar 3 más -3 es cero.
El resultado de sumar 1 más -8 es negativo.
```

Con lo cual ya no hay código repetido.

Y como se puede observar, la función original funciona correctamente.

#### EJERCICIO 5:&#x20;

Vamos a crear una función que haga de calculadora (suma, resta, producto y división), haciendo uso de funciones helper para mostrar la operación realizada. Pediremos por parámetro tipo de operación ("sum", "subract", "product", "division") y dos números reales. Devolveremos el resultado de la operación correspondiente.

```python
def calc(operation, a, b):
    """
    función que haga de calculadora (suma, resta, 
    producto y división), haciendo uso de funciones 
    helper para mostrar la operación realizada

    Args:
        operation (str): sum, sub, prod, div.
        a (float): Operando 1.
        b (float): Operando 2.

    Return:
        result (float): resultado de la operación.
    """
    if operation == "sum":
        result = a + b
    
    elif operation == "sub":
        result = a - b
    
    elif operation == "prod":
        result = a * b
    
    elif operation == "div":
        result = a / b

    else:
        print("- Operación no soportada.")
        result = "NULL"
        return -1

    if result != "NULL":
        helper_result(operation, a, b)
        return result

def helper_result(operation, a, b):
    """
    Función que muestra por pantalla el resultado de 
    la función calc

    Args:
        Los mismos que calc
    
    Return:
        0.
    """
    if operation == "sum":
        simbol = "+"
    elif operation == "sub":
        simbol = "-"
    elif operation == "prod":
        simbol = "x"
    else:
        simbol = "/"
    
    print("Se ha realizado la operación {} {} {}".format(a, simbol, b))
    return 0
```

```python
calc("sum", 1, 2)

#RESPUESTA
Se ha realizado la operación 1 + 2
3
```

## REPASO

```python
#EJERCICIO 1:Crea una función que busque todos los divisores del número entero positivo dado por parámetro y devuelva
#una lista con todos los divisores de dicho número.

def divisors(x):
    """
    Función que busca todos los divisores de un
    número entero dado.

    Args:
        x (int): Número del que sacar los divisores.
    
    Return:
        div (list): Lista con los divisores.
    """

    div = []
    for i in range(1, x + 1):
        if x % i == 0:
            div.append(i)
    return div
```

```python
divisors(124)
```

```
#RESPUESTA
[1, 2, 4, 31, 62, 124]
```

```python
#EJERCICIO 2: Crea una función que dados dos números reales por parámetro, devuelve el mayor.

def higher(a, b):
    """
    Función que devuelve el mayor de dos
    números.

    Args:
        a (float)
        b (float)
    
    Return:
        devuelve a o b en función de cual sea mayor.
    """

    if a > b:
        return a
    elif b > a:
        return b
    else:
        print("Ambos números son iguales.")
        return -1
```

```python
higher(9,9)
```

```
#RESPUESTA
Ambos números son iguales.
-1
```

```python
#EJERCICIO 3: Crea una función que dado un número devuelva su valor absoluto. Recuerda,

def absolut(x):
    """
    Función que devuelve el valor absoluto de x.

    Args:
        x (float)
    
    Return:
        x o -x (valor absoluto de x).
    """

    if x < 0:
        return (- x)
    else:
        return x
   
```

```python
absolut(-6)

#RESPUESTA
6
```

```python
#EJERCICIO 4: Crea una función que devuelva True si el caracter introducido por parámetro se trata de una vocal y False
# en caso contrario.

def vowels(n):
    """
    Función que devuelve si n es vocal o no.

    Args:
        n ("char")

    Return:
        vowel (bool): True si es vocal.
                    False si no es vocal.
    """
    if n == "a" or n == "e" or n == "i" or n == "o" or n == "u":
        vowel = True
    else:
        vowel = False
    return vowel
```

```python
vowels("6")

#RESPUESTA
False
```

```python
#EJERCICIO 5: Crea una función que devuelva el MCD (máximo común divisor) de 2 números proporcionados por parámetro.
#PISTA: Aprovecha la función que calcula el mayor entre dos números dados. También necesitarás una función
#que calcula el menor entre dos números dados.

def mcd(a, b):
    """
    Función que devuelve el MCD de a y b
    utilizando el algoritmo de Euclides.

    Args:
        a (int)
        b (int)
    Return:
        MDC (int)
    """
    if higher(a, b) == a:
        while a % b != 0:
            c = a
            a = b
            b = c % b
        return b
    elif higher(a, b) == b:
        while b % a != 0:
            c = b
            b = a
            a = c % a
        return a
```

```python
mcd(273, 665)

#RESPUESTA
7
```

```python
#EJERCICIO 6: Crea una función que devuelva el MCM (mínimo común múltiplo) de 2 números proporcionados por
#parámetro.
#PISTA: Aprovecha la función que calcula el MCD de dos números del ejercicio anterior y la función que
#calcula el valor absoluto de un número.

def mcm(a, b):
    """
    Función que calcula el MCM de dos números
    utiizando el método (a * b) / MCD.

    Args:
        a (int)
        b (int)
    Return:
        MCM (int)
    """
    return (a * b) / mcd(a, b)
```

```python
mcm(72, 50)

#RESPUESTA
1800.0
```

```python
#EJERCICIO 7: Crea una función que dada una palabra devuelva si es palíndroma.

def palindrome(word):
    """
    Función que comprueba si una palabra es palíndroma.

    Args:
        word (string): palabra a comprobar.

    Return:
        True or False
    """
    if word.lower() == word.lower()[::-1]:
        return True
    else:
        return False
```

```python
palindrome("Ana")

#RESPUESTA
True
```

```python
#EJERCICIO 8: Crea una función que dado un color en hexadecimal devuelva una lista de 3 posiciones, cada una de ellas
#correspondiente al valor R, G o B en este orden. Los valores de RGB varían entre 0 y 255.

def colors(hexa_color):
    """
    Función que dado un color en formato: #00FFAA
    devuelva una lista con los valores decimales
    RGB.
    
    Args:
        hexa_color (string): color en formato #00FFAA
    
    Return:
        rgb (list): lista con los valores decimales RGB.
    """

    if len(hexa_color) != 7:
        print("El formato del color no es válido.")
    
    else:
        #Con lo siguiente transformo hexadecimal a decimal con el int(x, 16).
        rgb = [int(hexa_color[1:3], 16), int(hexa_color[3:5], 16), int(hexa_color[5:7], 16)]
    return rgb
```

```python
colors("#FF0000")

#RESPUESTA
[255, 0, 0]
```

```python
#EJERCICIO 9: Crea una función que dada una lista de palabras por parámetro, devuelva un diccionario que contenga
#cuántas son de longitud par y cuántas de longitud impar.

def even(words):
    """
    Función que indica cuantas palabras 
    de una lista son pares y cuantas impares
    y lo devuelve en forma de diccionario.

    Args:
        words (list): lista de palabras.
    
    Return:
        even_odd (dic): diccionario pares e 
        impares
    """

    even_odd = {
                "even" : 0,
                "odd" : 0
                }
    
    for word in words:
        if len(word) % 2 == 0:
            even_odd["even"] += 1
        else:
            even_odd["odd"] += 1
    return even_odd
```

```python
even(["basura", "comida", "albondiga", "hola", "adios"])

#RESPUESTA
{'even': 3, 'odd': 2}
```

```python
#EJERCICIO 10: Crea una función que dado un string por parámetro cuente cuántas veces sale cada caracter en dicho string
# y devuelva toda esa información en un diccionario.

def letter_counter(sentence):
    """
    Función que cuenta las apariciones de cada uno
    de los carácteres en sentence.

    Args:
        sentence (str): string a contar.
    
    Return:
        counter (dic): diccionario con todo contado.
    """
    counted = []
    counter = {}
    sentence = sentence.lower()
    for i in sentence:
        if i not in counted:
            counter[i.upper()] = (sentence.count(i))
            counted.append(i)
    return counter
```

```python
letter_counter("aqui hace un frio brutal pero en la playa hace muy buen día")
```

```
#RESPUESTA
{' ': 12,
 'A': 8,
 'B': 2,
 'C': 2,
 'D': 1,
 'E': 5,
 'F': 1,
 'H': 2,
 'I': 2,
 'L': 3,
 'M': 1,
 'N': 3,
 'O': 2,
 'P': 2,
 'Q': 1,
 'R': 3,
 'T': 1,
 'U': 5,
 'Y': 2,
 'Í': 1}
```
