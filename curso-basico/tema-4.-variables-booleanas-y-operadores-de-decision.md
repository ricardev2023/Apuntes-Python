---
description: Explicación del uso de Variables Booleanas y Decisiones en Python 3
---

# Tema 4. Variables Booleanas y Operadores de Decisión

## Booleanos

**Dato booleano.** Es un tipo de dato que solamente puede tomar 2 valores: `True` (verdadero) o `False` (falso).

**Variable lógica.** Variable que almacena datos booleanos.

```python
is_adult = True
type(is_adult)

#RESPUESTA
bool
```

**Observación.** Observad que tanto `True` como `False` únicamente tienen la primera letra mayúscula. Además, a diferencia de otros lenguajes de programación, como por ejemplo `R`, `Python` solamente admite los booleanos escritos de esta forma: `True` o `False`.

### Tablas de verdad

Dadas dos variables lógicas, **A** y **B**,  podemos definir los operadores básicos mediante tablas de verdad, donde el valor verdadero se representa con la letra **V** o bien con un **1**, mientras que el valor falso se representa mediante la letra **F** o bien con un **0**.

La tabla de verdad para la variable **A** sería

|  A  |
| :-: |
|  V  |
|  F  |

La tabla de verdad para la variable **B** sería

|  B  |
| :-: |
|  V  |
|  F  |

#### **Negación**

El operador negación aplicado a una variable (unario) se representa con ¬ y devuelve el valor contrario. **Equivalente a NO**.

|  A  | ¬ A |
| :-: | :-: |
|  V  |  F  |
|  F  |  V  |

#### **Conjunción**

La conjunción entre dos variables se representa con ∧ y devuelve verdadero únicamente cuando ambas variables valen verdadero. **Equivalente a Y**.

|  A  |  B  | A ∧ B |
| :-: | :-: | :---: |
|  V  |  V  |   V   |
|  V  |  F  |   F   |
|  F  |  V  |   F   |
|  F  |  F  |   F   |

#### **Disyunción**

La disyunción entre dos variables se representa con ∨ y devuelve verdadero cuando al menos una de las variables lógicas vale verdadero. **Equivalente a O**.

|  A  |  B  | A ∨ B |
| :-: | :-: | :---: |
|  V  |  V  |   V   |
|  V  |  F  |   V   |
|  F  |  V  |       |
|  F  |  F  |   F   |

### Operadores lógicos en `Python`

Para hacer la negación, utilizamos el operador `not`.

```python
A = True
not A

#RESPUESTA
False
```

```python
B = False
not B

#RESPUESTA
True
```

Para hacer la conjunción entre dos variables lógicas, utilizamos el operador `and`.

```python
A, B = True, True
A and B

#RESPUESTA
True
```

```python
A and (not B)

#RESPUESTA
False
```

Para hacer la disyunción entre dos variables lógicas, utilizamos el operador `or`.

```python
A, B = False, False
A or B

#RESPUESTA
False
```

```python
(not A) or B

#RESPUESTA
True
```

### Operadores de comparación

En `Python` podemos comparar datos y obtener un resultado booleano. Los operadores de comparación disponibles son

| Operador | Significado         |
| :------: | ------------------- |
|     >    | Estrictamente mayor |
|     ≥    | Mayor o igual       |
|     <    | Estrictamente menor |
|     ≤    | Menor o igual       |
|    ==    | Igual               |
|    !=    | Diferente           |

```python
7 == 7.0

#RESPUESTA
True
```

```python
3.14 > 9

#RESPUESTA
False
```

```python
7 != "7"

#RESPUESTA
True
```

```python
0.01 <= 1

#RESPUESTA
True
```

**Observación.** Observad que cuando hemos comparado el número 7 en formato integer y en formato float, hemos obtenido que eran iguales, mientras que al haber comparado el número 7 en formato integer con el mismo número, pero en formato string, nos ha devuelto que son diferentes. Esto lo que nos viene a decir es que numéricamente, `Python` considera iguales los números enteros tanto si están en formato integer como en formato float. No obstante, nunca considerará iguales dos datos donde uno esté en formato numérico y el otro, en formato string.

#### **Múltiples comparaciones simultáneas**

Podemos realizar múltiples comparaciones a la vez.

Supongamos que tenemos que tener 16 años o más, pero como mucho 40 para poder concertar una entrevista y aspirar a ser miembros de la tripulación del pirata Pyratilla.

Queremos saber si nos concederá una entrevista si tenemos 17 años.

```python
edad = 17
(edad >= 16) and (edad <= 40)

#RESPUESTA
True
```

Hemos obtenido `True`, por tanto podemos concertar una entrevista. Que nos admita o no en su tripulación tras la entrevista, eso ya es otra cosa.

#### **Comparaciones de strings**

No solamente podemos comparar datos numéricos, sino que también podemos comparar strings en relación al orden alfabético. **Como lo ordenaría un diccionario**

```python
"Mallorca" < "Dubai"

#RESPUESTA
False
```

El resultado que obtenemos no se debe a que Mallorca sea mejor que Dubai, sino a que la primera letra de la primera palabra, M, no se encuentra antes en el abecedario que la primera letra de la segunda palabra, D.

**Observación.** En caso de que la primera letra de cada una de las palabras comparadas coincidan, se comparan los caracteres que se encuentran en la siguiente posición. En caso de empate, seguiríamos comparando los caracteres de la tercera posición y así sucesivamente.

```python
"Mallorca" >= "Madrid"

#RESPUESTA
True
```

### Más métodos de string

El método `.startswith()` nos devuelve verdadero si el string empieza con el caracter o la cadena de caracteres indicado.

```python
s = "Mallorca es una isla preciosa"
s.startswith("m")

#RESPUESTA
False
```

```python
s.startswith("Mallorca")

#RESPUESTA
True
```

**Observación.** Como podéis observar, `Python` diferencia entre letras en mayúscula y letras en minúscula. Por eso es que obtenemos falso al preguntar si el string empieza por m, en vez de M.

El método `.endswith()` nos devuelve verdadero si el string acaba con el caracter o la cadena de caracteres indicado.

```python
s = "Mallorca es una isla preciosa"
s.endswith("a")

#RESPUESTA
True
```

```python
s.endswith("bonita")

#RESPUESTA
False
```

El método `.isalnum()` nos devuelve verdadero si todos los caracteres del string son alfanuméricos.

```python
s = "Python365"
s.isalnum()

#RESPUESTA
True
```

```python
s = "Han creado un blog llamado Python365"
s.isalnum()

#RESPUESTA
False
```

**¡Cuidado!** No se consideran caracteres alfanuméricos los siguientes: espacio en blanco, !, %, ?, & y un largo etcétera.

El método `.isalpha()` nos devuelve verdadero si todos los caracteres del string son del alfabeto.

```python
s = "Cachalote"
s.isalpha()

#RESPUESTA
True
```

```python
s = "Mi perro se llama Guindilla"
s.isalpha()

#RESPUESTA
False
```

El método `.isdigit()` nos devuelve verdadero si todos los caracteres del string son dígitos.

```python
s = "365"
s.isdigit()

#RESPUESTA
True
```

```python
s = "Pyo365"
s.isdigit()

#RESPUESTA
False
```

El método `.isspace()` nos devuelve verdadero si todos los caracteres del string son espacios en blanco.

```python
s = "                  "
s.isspace()

#RESPUESTA
True
```

El método `.islower()` nos devuelve verdadero si todos los caracteres del string están en minúscula.

```python
s = "Mi gato se llama Bigotes"
s.islower()

#RESPUESTA
False
```

```python
s = "me gusta hacer puzzles"
s.islower()

#RESPUESTA
True
```

El método `.isupper()` nos devuelve verdadero si todos los caracteres del string están en mayúscula.

```python
s = "Mi gato se llama Bigotes"
s.isupper()

#RESPUESTA
False
```

```python
s = "ME GUSTA HACER PUZZLES"
s.isupper()

#RESPUESTA
True
```

El método `.istitle()` nos devuelve verdadero si todas las palabras del string empiezan en mayúscula y el resto de las letras de la palabra están en minúscula.

```python
s = "Platero Y Yo"
s.istitle()

#RESPUESTA
True
```

```python
s = "PLATERO Y YO"
s.istitle()

#RESPUESTA
False
```

## Operadores de decisión

### `if`

Cuando queremos comprobar si se cumple alguna condición, utilizamos el operador de decisión `if`. **SOLO SE EJECUTA SI EL RESULTADO DE LA CONDICIÓN ES TRUE**. La sintaxis que debemos seguir es la siguiente:

```python
if condicion:
    consecuencia
```

**¡Cuidado!** La sintaxis de los dos puntos después de la condición y la indentación (equivalente a una tabulación, un total de 4 espacios en blanco) que precede a la consecuencia es muy importante. De hecho, si se omite alguna de las dos cosas o bien nos pasamos de indentación, nos saltará error.

* Si queréis hacer una tabulación, debéis pulsar el tabulador una vez.
* Podéis hacer tabulaciones en bloque seleccionando las líneas de código que queráis indentar y, a continuación, pulsando el tabulador.
* Podéis deshacer tabulaciones pulsando Shift + Tab
* Podéis deshacer tabulaciones en bloque seleccionando las líneas de código que queráis desindentar y, a continuación, pulsando el Shift + Tab.

Siguiendo con nuestro ejemplo, si el usuario tiene más de 16 años, pero menos de 40, entonces puede formar parte de la tripulación de Pyratilla.

```python
age = 23
if (age >= 16 and age <= 40):
    print("Puedes formar parte de la tripulación de Pyratilla")
    
#RESPUESTA
Puedes formar parte de la tripulación de Pyratilla
```

#### EJERCICIO 1:

```python
#Dado un string vamos a comprobar si tiene espacios en blanco en su interior y contaremos cuantos tiene:
#Opción 1, utilizando s.find(" ") si no es -1 implica que tengo espacios.

print("Escriba un texto para comprobar si tiene espacios.")
s = input("Su texto aquí: ")
idx = s.find (" ")
if (idx != -1):
    print("El string tiene {} espacios".format(s.count(" ")))
else:
    print("El string NO TIENE espacios")
```

```python
#RESPUESTA
Escriba un texto para comprobar si tiene espacios.
Su texto aquí: aaaa a
El string tiene 1 espacios
```

```python
#Dado un string vamos a comprobar si tiene espacios en blanco en su interior y contaremos cuantos tiene:
#Opción 2, utilizando el operador in para comprobar en el if si hay espacios o no.

print("Escriba un texto para comprobar si tiene espacios.")
s = input("Su texto aquí: ")
if (" " in s):
   print("El string tiene {} espacios".format(s.count(" ")))
else:
    print("El string NO TIENE espacios")
```

### `else`

Ahora, nos podríamos preguntar qué le podríamos decir al usuario en el caso en que no satisfaga la condición. Ahí es donde entra en juego el operador de decisión `else`. **SOLO SE EJECUTA SI LA CONDICIÓN ARROJA FALSE**. Esta vez, la sintaxis a seguir es la siguiente:

```python
if condición:
    consecuencia_si_es_verdad
else:
    consecuencia_si_es_falsa
```

Siguiendo el ejemplo anterior, si el usuario tiene 16 años o más, pero menos de 40, entonces puede formar parte de la tripulación de Pyratilla. Si no, le diremos que no satisface una necesidad básica para ser miembro.

```python
age = 13
if (age >= 16 and age <= 40):
    print("Puedes formar parte de la tripulación de Pyratilla")
else:
    print("No satisfaces una necesidad básica para pertenecer a la tripulación del gran Pyratilla")
    
#RESPUESTA
No satisfaces una necesidad básica para pertenecer a la tripulación del gran Pyratilla
```

#### EJERCICIO 2: Ecuaciones de primer grado

```python
#Vamos a hacer un programa que resuelva ecuaciones de primer grado de la forma  Ax+B=0  proporcionadas por el usuario donde  A≠0 .

print("A continuación escriba los digitos de la ecuacion a resolver (Ax+B=0)")
a = float(input("+ Introduzca un valor para A: ")) #Hacemos casting en float para que no se trunque el resultado en caso necesario.
if (a == 0):
    print("- ERROR. el valor de A no puede ser cero")
else:
    b = float(input("+ Introduzca un valor para B: "))
    solution = -b / a
    print("+ El resultado de su ecuación es: {}".format(solution))
```

```python
#RESPUESTA
A continuación escriba los digitos de la ecuacion a resolver (Ax+B=0)
+ Introduzca un valor para A: 5
+ Introduzca un valor para B: 3
+ El resultado de su ecuación es: -0.6
```

### `elif`

Ahora, en vez de comprobar si se cumple o no una condición, nos podríamos preguntar cómo haríamos para comprobar más de una condición. Podríamos hacerlo a lo bruto anidando operadores `if`, esto es, metiendo un `if` dentro de otro; o bien, podríamos hacerlo utilizando el operador de decisión `elif`.

El operador `elif` funciona del siguiente modo: se empieza con un operador `if`; si la condición de este no se cumple, pasamos a la siguiente condición posible precedida de un `elif`; si esta tampoco se cumple, pasamos al siguiente `elif`; seguimos así hasta que o bien se satisface alguna condición y realizamos su consecuencia, o hasta llegar al `else`, que implica que no se ha satisfecho ninguna de las condiciones anteriores.

La sintaxis del operador de decisión `elif` es la siguiente:

```python
if condición_1:
  consecuencia
elif condición_2:
  consecuencia
elif condición_3:
  consecuencia
. 
. 
. 
else:
  consecuencia
```

Recuperemos el ejemplo de que tenemos que tener 16 años o más, pero menos de 40 para ser miembros de la tripulación del pirata Pyratilla. Vamos a mejorar lo que habíamos conseguido con el `if` y el `else`, añadiendo el operador `elif`.

Además, veremos que nos dice con la edad de 20 años.

```python
age = 20

if age > 40:
  print("No puedes pertenecer a la tripulación, te pasas de la edad límite que ha puesto el gran capitán Pyratilla.")
elif age >= 16:
  print("Podrás optar a pertenecer la tripulación. Aún te queda superar la entrevista con el capitán.")
else:
  print("Eres muy pequeño todavía para la vida pirata!")

#RESPUESTA
Podrás optar a pertenecer la tripulación. Aún te queda superar la entrevista con el capitán.
```

El funcionamiento del código anterior es el siguiente:

* El `if` comprueba si la edad introducida es mayor a 40.
* El `elif` comprueba si la edad se encuentra en el intervalo \[16, 40]
* El `else` implica que la edad introducida es menor a 16

### Operador ternario

Si queremos hacer un simple `if` / `else` en una sola línea de código, podemos utilizar el operador ternario, que tiene la siguiente estructura:

```python
consecuencia_cierto if condición else consecuencia_falso
```

Por ejemplo, hagamos el caso de mayor de edad. Si la edad es mayor o igual a 18, entonces es mayor de edad en España. Si no, entonces es menor de edad en España.

```python
age = 20
texto_mayor = "Eres mayor de edad en España"
texto_menor = "Eres menor de edad en España"

print(texto_mayor) if age >= 18 else print(texto_menor)

#RESPUESTA
Eres mayor de edad en España
```

#### EJERCICIO 3: Numero par o impar

```python
#Vamos a comprobar si un número es par o impar haciendo uso del operador ternario.

print("Escriba un número al azar, el programa le dirá si es par o impar.")
n = int(input("número: "))

par = "El número {} es par".format(n)
impar = "El número {} es impar".format(n)

print(par) if (n % 2 == 0) else print(impar)
```

```python
#RESPUESTA
Escriba un número al azar, el programa le dirá si es par o impar.
número: 3
El número 3 es impar
```

#### EJERCICIO 4: Punto dentro de cuadrado

Vamos a comprobar si un punto del plano euclidiano de la forma (x,y) pertenece o no al cuadrado unidad.

El cuadrado unidad es el que tiene por vértices los puntos (0,0) , (0,1) , (1,0) y (1,1)

```python
#Vamos a comprobar si un punto del plano euclidiano de la forma  (x,y)  pertenece o no al cuadrado unidad.
#El cuadrado unidad es el que tiene por vértices los puntos  (0,0) ,  (0,1) ,  (1,0)  y  (1,1)

print("Introduzca las coordenadas de un punto y el programa comprobará si se encuentra dentro del \"cuadrado unidad\".")
x = float(input("Coordenada X: "))
y = float(input("Coordenada Y: "))
if (x >= 0 and x <= 1 and y >= 0 and y <= 1 ):
    print("El punto con coordenadas ({},{}) se encuentra dentro del \"cuadrado unidad\".".format(x,y))
else:
    print("El punto con coordenadas ({},{}) se encuentra fuera del \"cuadrado unidad\".".format(x,y))
```

```python
#RESPUESTA
Introduzca las coordenadas de un punto y el programa comprobará si se encuentra dentro del "cuadrado unidad".
Coordenada X: -0.3
Coordenada Y: 0.6
El punto con coordenadas (-0.3,0.6) se encuentra fuera del "cuadrado unidad".
```

### Operadores Anidados

```python
age = 20
name = "Martin"

if age >= 18:
  if name.startswith("M") or name.startswith("m"):
    print("Eres mayor de edad pues tienes {} años y tu nombre, que es {}, empieza por M".format(age, name))
  else:
    print("Eres mayor de edad pues tienes {} años".format(age))
else:
  print("Eres muy joven")
  
  #RESPUESTA
  Eres mayor de edad pues tienes 20 años y tu nombre, que es Martin, empieza por M
```

#### EJERCICIO 5: Año bisiesto

```python
#Vamos a comprobar si un año es bisiesto o no.
#Un año es bisiesto si es divisible entre cuatro pero no es múltiplo de cien a no ser que lo sea de 400.

print("Escriba el año que quiere saber si es bisiesto.")
year = int(input("año: "))
if year < 0:
    print("Los años no pueden ser negativos.")
else:
    if (year % 4 == 0) and (year % 100 != 0):
        print("El año {} es bisiesto".format(year))
    elif (year % 4 == 0) and (year % 400 == 0):
        print ("El año {} es bisiesto".format(year))
    else:
        print ("El año {} no cumple las características de los años bisiestos.".format(year))
```

```python
#RESPUESTA
Escriba el año que quiere saber si es bisiesto.
año: 5
El año 5 no cumple las características de los años bisiestos
```

```python
#Solución de la profesora

year = int(input("Año: "))

if year % 4 == 0:
  if year % 100 == 0:
    if year % 400 == 0:
      print("El año {} es bisiesto".format(year))
    else: print("El año {} no es bisiesto".format(year))
  else: print("El año {} es bisiesto".format(year))
else: print("El año {} no es bisiesto".format(year))
```

### REPASO

```python
#EJERCICIO 1:
#Haz que un usuario introduzca un número real y evalúa si dicho número es positivo, negativo o cero. Devuelve
#por pantalla el resultado en cada caso.

print("Introduzca un número real y el programa le dirá si es positivo, negativo o cero.")
num = float(input("su numero: "))

if num > 0:
    print("El número {} es positivo.".format(num))
elif num < 0:
    print("El número {} es negativo.".format(num))
elif num == 0:
    print("Es {}. ni positivo ni negativo.".format(num))
```

```python
#RESPUESTA
Introduzca un número real y el programa le dirá si es positivo, negativo o cero.
su numero: 0.5
El número 0.5 es positivo.
```

```python
#EJERCICIO 2:
#Haz que un usuario introduzca su nombre y evalúa con operadores if y else si dicho nombre tiene una
#longitud mayor a 10 caracteres o no. Devuelve por pantalla el resultado en cada caso.

print("Introduzca su nombre y comprobaremos si es más largo que 10 caracteres.")
name = input("Introduzca su nombre: ")

if len(name) >= 10:
    print("El nombre {} es más largo de 10 caracteres incluyendo el espacio si lo hubiera.".format(name))
else:
    print("El nombre {} no llega a 10 caracteres incluyendo el espacio si lo hubiera.".format(name))
```

```python
#RESPUESTA
Introduzca su nombre y comprobaremos si es más largo que 10 caracteres.
Introduzca su nombre: aaaaaaaaaaaaaaaaaaaaaaa
El nombre aaaaaaaaaaaaaaaaaaaaaaa es más largo de 10 caracteres incluyendo el espacio si lo hubiera.
```

```python
#EJERCICIO 3:
#Realiza el ejercicio anterior con el uso del operador ternario.

print("Introduzca su nombre y comprobaremos si es más largo que 10 caracteres.")
name = input("Introduzca su nombre: ")
mas10 = "El nombre {} es más largo de 10 caracteres incluyendo el espacio si lo hubiera.".format(name)
menos = "El nombre {} no llega a 10 caracteres incluyendo el espacio si lo hubiera.".format(name)

print(mas10) if len(name) >= 10 else print(menos)
```

```
#RESPUESTA
Introduzca su nombre y comprobaremos si es más largo que 10 caracteres.
Introduzca su nombre: aaaaaaaaaaaaaaaaaaaaaaaaaaaa
El nombre aaaaaaaaaaaaaaaaaaaaaaaaaaaa es más largo de 10 caracteres incluyendo el espacio si lo hubiera.
```

```python
#EJERCICIO 4:
#Haz que un usuario introduzca dos números enteros positivos. Comprueba si el primer número introducido
#por el usuario es mayor o igual que el segundo número introducido por el usuario. Devuelve por pantalla el
#resultado en cada caso.
#PISTA: Asegúrate de hacer uso de la función int() donde pertoque

print("Escriba dos números enteros positivos y el programa le dirá si el primero es mayor, igual o menor que el segundo.")
a = float(input("Escriba el primer número entero positivo: "))
if a > 0 and int(a):
    b = float(input("Escriba el segundo número entero positivo: "))
    if b > 0 and int(b):
        if a > b:
            print("A es {} unidades MAYOR que B".format(int((a - b))))
        elif a < b:
            print("A es {} unidades MENOR que B".format(int((b - a))))
        else:
            print("A y B son el mismo número.")
    else:
        print("El numero {} no cumple las especificaciones".format(b))
else: 
    print("El numero {} no cumple las especificaciones".format(a))
```

```
#RESPUESTA
Escriba dos números enteros positivos y el programa le dirá si el primero es mayor, igual o menor que el segundo.
Escriba el primer número entero positivo: 6
Escriba el segundo número entero positivo: 0.5
El numero 0.5 no cumple las especificaciones
```

```python
#EJERCICIO 5:
#Haz que un usuario introduzca dos números enteros positivos. Suponiendo que el primer número introducido
#por el usuario es mayor o igual al segundo número introducido por el usuario, comprueba que la división del
#primer número entre el segundo número es entera.
#En caso de la división ser entera, devuelve el cociente por pantalla e indica que la división en efecto es entera.
#En caso de la división no ser entera, devuelve el cociente y el resto por pantalla e indica que la división entre
#los dos números no es entera.

print("Escriba dos números enteros positivos y el programa le dirá si el primero es divisible por el segundo.")
a = float(input("Escriba el primer número entero positivo: "))
if a > 0 and int(a):
    b = float(input("Escriba el segundo número entero positivo: "))  
    if b > 0 and int(b):
        if a >= b:
            if a % b == 0:
                print("La división de {} entre {} es entera y su cociente es: {}".format(int(a),int(b),int(a//b)))
            else:
                print("La división de {} entre {} NO es entera. \n\tcociente: {} \n\tresto: {}".format(int(a),int(b),int(a//b),int(a%b)))
        else:
            print("La división de {} entre {} da un resultado decimal: {}".format(int(a),int(b),a/b))
    else:
        print("El numero {} no cumple las especificaciones".format(b))
else:
    print("El numero {} no cumple las especificaciones".format(a))
```

```
#RESPUESTA
Escriba dos números enteros positivos y el programa le dirá si el primero es divisible por el segundo.
Escriba el primer número entero positivo: 6
Escriba el segundo número entero positivo: 0.6
El numero 0.6 no cumple las especificaciones
```

```python
#EJERCICIO 6:
#Fusiona lo hecho en los ejercicios 4 y 5 para que
#1. Un usuario introduzca dos números enteros por pantalla.
#2. Comprobar si el primer número es mayor o igual al segundo número introducido por el usuario. Devolver por pantalla en que caso nos encontramos.
#3. Hacer la división entera pertinente en cada caso.
#4. Si la división es entera, entonces devolver por pantalla el cociente e indicar que la división es entera.
#Si la división no es entera, entonces devolver por pantalla el cociente y el resto e indicar que la división realizada no es entera.

print("Escriba dos números enteros positivos y el programa le dirá si el primero es divisible por el segundo.")
a = float(input("Escriba el primer número entero positivo: "))
if a > 0 and int(a):
    b = float(input("Escriba el segundo número entero positivo: "))  
    if b > 0 and int(b):

        if a > b:
            print("A es {} unidades MAYOR que B".format(int((a - b))))
        elif a < b:
            print("A es {} unidades MENOR que B".format(int((b - a))))
        else:
            print("A y B son el mismo número.")

        if a >= b:
            if a % b == 0:
                print("La división de {} entre {} es entera y su cociente es: {}".format(int(a),int(b),int(a//b)))
            else:
                print("La división de {} entre {} NO es entera. \n\tcociente: {} \n\tresto: {}".format(int(a),int(b),int(a//b),int(a%b)))
        else:
            print("La división de {} entre {} da un resultado decimal: {}".format(int(a),int(b),a/b))
    else:
        print("El numero {} no cumple las especificaciones".format(b))
else:
    print("El numero {} no cumple las especificaciones".format(a))
```

```
#RESPUESTA
Escriba dos números enteros positivos y el programa le dirá si el primero es divisible por el segundo.
Escriba el primer número entero positivo: 6
Escriba el segundo número entero positivo: 0.5
El numero 0.5 no cumple las especificaciones
```

```python
#EJERCICIO 7:
#Haz que un usuario introduzca dos números enteros positivos. Comprueba si el mayor es múltiplo del menor.
#Devuelve por pantalla el resultado en cada caso.

print("Escriba dos números enteros positivos y el programa le dirá si el mayor es múltiplo del menor.")
a = float(input("Escriba el primer número entero positivo: "))
if a > 0 and int(a):
    b = float(input("Escriba el segundo número entero positivo: "))
    if b > 0 and int(b):
        if a > b and a % b == 0:
            print("El número {} ES múltiplo del número {}.".format(int(a),int(b)))
        elif a > b and a % b != 0:
            print("El número {} NO ES múltiplo del número {}.".format(int(a),int(b)))
        elif a < b and b % a == 0:
            print("El número {} ES múltiplo del número {}.".format(int(b),int(a)))
        elif a < b and b % a != 0:
            print("El número {} NO ES múltiplo del número {}.".format(int(b),int(a)))
        else:
            print("Los dos números son iguales.")
    else:
        print("El numero {} no cumple las especificaciones".format(b))    
else: 
    print("El numero no cumple las especificaciones")
```

```
#RESPUESTA
Escriba dos números enteros positivos y el programa le dirá si el mayor es múltiplo del menor.
Escriba el primer número entero positivo: 4
Escriba el segundo número entero positivo: 2
El número 4 ES múltiplo del número 2.
```

```python
#EJERCICIO 8:
#Haz que un usuario introduzca una palabra y comprueba si dicha palabra empieza por mayúscula. Devuelve por pantalla el resultado en cada caso.
print("Escriba una palabra y el programa le dirá si empieza por mayuscula.")
word = input("Su palabra: ")
if word.find(" ") != -1:
    print("Solo una palabra, por favor.")
else:
    if word.istitle():
        print("Su palabra empieza por mayuscula.")
    else:
        print("Su palabra NO EMPIEZA por mayuscula.")
```

```
#RESPUESTA
Escriba una palabra y el programa le dirá si empieza por mayuscula.
Su palabra: a a
Solo una palabra, por favor.
```

```python
#Ejercicio 9:
#Haz un usuario introduza una letra y comprueba si se trata de una vocal. Si el usuario introduce un string de más de un carácter, 
#infórmale de que no se puede procesar el dato, pues debe tener como máximo tamaño 1.
#PISTA: Convierte la letra introducida a minúsculas para tener que realizar menos comprobaciones

print("Introduzca una letra y el programa comprobará si es una vocal.")
letter = input("su letra: ")
if len(letter) != 1 or letter == " ":
    print("El dato introducido debe ser una sola letra. reinicie la aplicación y vuelva a intentarlo.")
elif letter.lower() == "a" or letter.lower() == "e" or letter.lower() == "i" or letter.lower() == "o" or letter.lower() == "u":
    print("Su letra: {} es una vocal.".format(letter))
else:
    print("Su letra {} es una consonante.".format(letter))
    
```

```
#RESPUESTA
 una letra y el programa comprobará si es una vocal.
su letra: U
Su letra: U es un vocal.
```

```python
#EJERCICIO 10:
#Solución de ecuaciones de segundo grado del tipo: o ax2 + bx + c = 0
from math import sqrt

print("Introduzca el valor de los coeficientes a, b y c para solucionar la ecuación de segundo grado ax2 + bx + c = 0.")
a = float(input("Coeficiente A (debe ser diferente de 0): "))
if a != 0:
    b = float(input("Coeficiente B: "))
    c = float(input("Coeficiente C: "))
    discriminante = b ** 2 - 4 * a * c
    if discriminante > 0:
        sol1 = (-b + sqrt(discriminante)) / (2 * a)
        sol2 = (-b - sqrt(discriminante)) / (2 * a)
        print("El discriminante es positivo por lo que las soluciones son:\n\tsolución 1: {}\n\tsolución2: {}".format(sol1,sol2))
    elif discriminante == 0:
        sol = (-b) / (2 * a)
        print("El discriminante es igual a cero por lo que las soluciones son: {} y {}".format(sol,sol))
    else:
        print("El discriminante es negativo por lo que no existe solución real para esta ecuación.")
else:
    print("El coeficiente a no puede ser {}".format(int(a)))
    
```

```
#RESPUESTA
Introduzca el valor de los coeficientes a, b y c para solucionar la ecuación de segundo grado ax2 + bx + c = 0.
Coeficiente A (debe ser diferente de 0): 1
Coeficiente B: 4
Coeficiente C: 4
El discriminante es igual a cero por lo que las soluciones son: -2.0 y -2.0
```
