---
description: Explicación del uso de cadenas de texto en Python 3.
---

# Tema 3. Strings en Python

## Variable string

**String.** Cadena ordenada de caracteres.

Una variable de tipo string es aquella que guarda un string. Cuando queremos que una variable se trate de una variable de tipo string, `str` en `Python`, a la hora de declararla, el contenido de la variable debe ir o bien entre comillas dobles `" "`, o bien entre comillas simples `' '` .

```python
s1 = "Esto es un string entre comillas dobles"
type(s1)

#RESPUESTA
str
```

```python
s2 = 'Esto es un string entre comillas simples'
type(s2)

#RESPUESTA
str
```

**¡Cuidado!** `Python` no trabaja bien con los acentos. Por tanto, aunque no esté del todo bien escrito, mejor evitarlos, pues nos ahorraremos muchos problemas.

### String literals

El hecho de que el contenido de las variables de tipo `str` vaya entre comillas, ya sean simples o dobles, conlleva a que algunos caracteres deban ser tratados de forma especial.

Aquí entran en juego los string literals. Algunos de los más utilizados se muestran en la siguiente tabla:

| Código |      Significado      |
| :----: | :-------------------: |
|  `\\`  |     Backslash, `\`    |
|  `\'`  |  Comilla simple, `'`  |
|  `\"`  |   Comilla doble, `"`  |
|   \n   |     Salto de línea    |
|   \t   | Tabulación horizontal |

Para más información acerca de los string literals ir a la [documentación](https://docs.python.org/3.7/reference/lexical\_analysis.html#string-and-bytes-literals).

***

#### **Ejemplo 1**

Si queremos guardar en una variable el siguiente texto,

`Juan dijo: "me gusta el chocolate"`

lo tendremos que hacer del siguiente modo

```python
s1 = "Juan dijo: \"me gusta el chocolate \""
s1

#RESPUESTA
'Juan dijo: "me gusta el chocolate "'
```

```python
s2 = 'Juan dijo: "me gusta el chocolate "'
s2

#RESPUESTA
'Juan dijo: "me gusta el chocolate "'
```

**Observación.** Si usamos comillas dobles, para guardar la frase de este ejemplo necesitaremos usar string literals, ya que si no nos saltará error. Sin embargo, si usamos comillas simples, para guardar la frase de este ejemplo en una variable no hace falta que cambiemos nada.

#### **Ejemplo 2**

Si queremos guardar en una variable el siguiente texto,

`Ricardo dijo: 'me gusta la playa'`

lo tendremos que hacer del siguiente modo

```python
s1 = "Ricardo dijo: 'me gusta la playa'"
s1

#RESPUESTA
"Ricardo dijo: 'me gusta la playa'"
```

```python
s2 = 'Ricardo dijo: \'me gusta la playa\''
s2

#RESPUESTA
"Ricardo dijo: 'me gusta la playa'"
```

**Observación.** Si usamos comillas dobles, para guardar la frase de este ejemplo no necesitaremos usar string literals. Sin embargo, si usamos comillas simples, para guardar la frase de este ejemplo en una variable tendremos que usar string literals, porque si no nos saltará un error.

#### **Ejemplo 3**

Si queremos guardar en una variable el siguiente texto y que se conserve el salto de línea,

`Con diez cañones por banda,`

`viento en popa a toda vela`

lo tendremos que hacer del siguiente modo

```python
s3 = "Con diez cañones por banda,\nviento en popa a toda vela"
s3

#RESPUESTA
'Con diez cañones por banda,\nviento en popa a toda vela'
```

**Observación.** El resultado con el salto de línea aplicado lo veremos cuando hablemos de la función `print()`, cosa que haremos más adelante en esta sección.

## Concatenación de strings

La concatenación es una operación que une dos o más strings en uno solo.

En `Python`, para concatenar dos variables de tipo string usamos la función `+`.

```python
s1 = "Hola, "
s2 = "Juan"
s1 + s2

#RESPUESTA
'Hola, Juan'
```

**Observación.** La concatenación viene a ser como pegar el final del primer string con el princio del segundo. Entonces, conviene poner un espacio al final de la primera variable a concatenar, o bien al principio de la segunda para que así, al realizar la concatenación, exista ese espacio entre las palabras.

De no añadir espacios adicionales, obtendríamos resultados como el mostrado en el siguiente chunk:

```python
s1 = "Bienvenido"
s2 = "al curso."
s1 + s2

#RESPUESTA
'Bienvenidoal curso.'
```

Si dejamos un espacio adicional al final del string `s1`, obtenemos

```python
s1 = "Bienvenido "
s2 = "al curso."
s1 + s2

#RESPUESTA
'Bienvenido al curso.'
```

Si dejamos un espacio adicional al principio del string `s2` obtenemos

```python
s1 = "Bienvenido"
s2 = " al curso."
s1 + s2

#RESPUESTA
'Bienvenido al curso.'
```

Si dejamos un espacio adicional tanto al final del string `s1` como al principio del string `s2` obtenemos

```python
s1 = "Bienvenido "
s2 = " al curso."
s1 + s2

#RESPUESTA
'Bienvenido  al curso.'
```

Si dejamos más de un espacio adicional ya sea al final del string `s1` como al principio del string `s2` obtenemos

```python
s1 = "Bienvenido   " # Se han dejado 3 espacios adicionales
s2 = "al curso."
s1 + s2

#RESPUESTA
'Bienvenido   al curso.'
```

**Observación.** El número de espacios añadidos se conserva. Más adelante en esta sección veremos como eliminar los posibles espacios en blanco sobrantes.

## Repetición de strings

La repetición es una operación que repite la variable string tantas veces como indiquemos.

En `Python`, para repetir una variable de tipo string usamos la función `*`. El orden de los factores no altera el producto. Es decir, tanto da usar la sintaxis `num_repeticiones * variable_str` como `variable_str * num__repeticiones`.

```python
s1 = "¿Falta mucho? "
s1 * 5

#RESPUESTA
'¿Falta mucho? ¿Falta mucho? ¿Falta mucho? ¿Falta mucho? ¿Falta mucho? '
```

```python
s2 = " ¿Hemos llegado ya?"
5 * s2

#RESPUESTA
' ¿Hemos llegado ya? ¿Hemos llegado ya? ¿Hemos llegado ya? ¿Hemos llegado ya? ¿Hemos llegado ya?'
```

**Observación.** Al igual que ocurría con la concatenación, hay que añadir manualmente uno o más espacios en blanco al principio o al final del string para que las repeticiones no estén pegadas las unas a las otras, tal y como ocurre en el siguiente chunk de código.

```python
s3 = "Había una vez un barquito chiquitito"
s3 * 2

#RESPUESTA
'Había una vez un barquito chiquititoHabía una vez un barquito chiquitito'
```

### La función `print()`

Hasta ahora, cada vez que mostrábamos strings por pantalla, estos salían entre comillas simples.

La función `print()` nos sirve, entre otras muchas cosas, para mostrar strings por pantalla.

```python
s = "Hello world"
s

#RESPUESTA
'Hello world'
```

```python
print(s)

#RESPUESTA
Hello world
```

**Observación.** Como véis, una de las principales diferencias entre usar la función `print()` o no usarla es que a la hora de mostrar la cadena de caracteres por pantalla, ésta no va entre comillas simples y el formato en que se imprime también es diferente.

No solamente podemos imprimir strings, sino que podemos mostrar el resultado de cualquier variable (numérica o de tipo string)

```python
x = "Vivo en una isla"
print(x)

#RESPUESTA
Vivo en una isla
```

```python
y = 2.0
print(y)

#RESPUESTA
2.0
```

Al igual que podíamos concatenar strings con la función `+`, combinando ésta junto con la función `print()` podemos concatenar strings con variables que almacenan strings

```python
name = "Don Pepito"
print("¡Buenos días, " + name + "!")

#RESPUESTA
¡Buenos días, Don Pepito!
```

**Observación.** Recordad introducir un espacio adicional siempre que vayáis a concatenar cualquier cosa (strings con strings, strings con variables...), para que así el resultado quede legible.

**Observación.** Utilizando la función `print()`, el uso de acentos o de algunos caracteres especiales como `¿` o `¡` ya no dan problemas a la hora de mostrarse por pantalla. Ésto se debe a que con la función print, python procesa el texto y lo muestra de la manera que se espera.

**Observación.** Podemos obtener exactamente el mismo resultado utilizando comas (`,`) en vez de la función `+`. Eso sí, después de cada coma se nos añade automáticamente un espacio en blanco que no siempre buscamos, como ocurre a continuación después del resultado de la variable `name`.

```python
name = "Don Pepito"
print("¡Buenos días,", name + "!") #Utilizo el simbolo de suma para que no me 
                                   #ponga un espacio detrás del nombre.
                                   
                                   
#RESPUESTA
¡Buenos días, Don Pepito!
```

Al igual que podíamos repetir un mismo string un número cualquiera de veces con la función `*`, combinando ésta junto con la función `print()` podemos multiplicar un string o variables que contengan strings

```python
print("¿Falta mucho? " * 5)

#RESPUESTA
¿Falta mucho? ¿Falta mucho? ¿Falta mucho? ¿Falta mucho? ¿Falta mucho? 
```

```python
pregunta = "¿Falta mucho? "
print(pregunta * 5)

#RESPUESTA
¿Falta mucho? ¿Falta mucho? ¿Falta mucho? ¿Falta mucho? ¿Falta mucho? 
```

#### Ejercicio 1: Cumpleaños Feliz

Vamos a combinar concatenación y repetición de strings para reproducir la canción "Cumpleaños feliz"

```python
s1 = "¡Cumpleaños feliz!"
s2 = "Te deseamos todos"

song = (s1 + "\n") * 2 + s2 + ",\n" + s1
print(song)

#RESPUESTA
¡Cumpleaños feliz!
¡Cumpleaños feliz!
Te deseamos todos,
¡Cumpleaños feliz!
```

### La función `str()`

La función `str()` sirve para convertir cualquier variable a tipo string. A esto se le llama **casting**.

Con la función `str()`, podemos concatenar strings y variables de cualquier tipo dentro de un `print()`:

```python
nombre = "María"
edad = 22
print("Mi hermana se llama " + nombre + " y su edad es " + str(edad))

#RESPUESTA
Mi hermana se llama María y su edad es 22
```

### El método `.format()`

Existe otra forma de concatenar strings y variables de cualquier tipo dentro de un `print()` y es gracias al método `.format()`.

Lo que hay que hacer es indicar con llaves, `{}`, donde queremos situar el resultado de las variables y luego, dentro de los paréntesis del método `.format()`, indicar las variables en su respectivo orden entre paréntesis.

```python
nombre = "Ricardo"
numero_gatos = 3
print("Mi abuelo se llama {} y tiene {} gatos".format(nombre, numero_gatos))

#RESPUESTA
Mi abuelo se llama Ricardo y tiene 3 gatos
```

## Saltos de línea y tabulaciones

Si recordáis el ejemplo 3, teníamos la variable `s3`, que contenía un salto de línea

```python
s3 = "Con diez cañones por banda,\nviento en popa a toda vela"
Con la función print(), seremos capaces de visualizar dicho salto de línea 
```

Con la función print(), seremos capaces de visualizar dicho salto de línea

```python
print(s3)

#RESPUESTA
Con diez cañones por banda,
viento en popa a toda vela
```

Y lo mismo ocurriría con la tabulación horizontal.

```python
s4 = "La string literal \\t producía \t una tabulación horizontal"
s4

#RESPUESTA
'La string literal \\t producía \t una tabulación horizontal'
```

```python
print(s4)

#RESPUESTA
La string literal \t producía 	 una tabulación horizontal
```

## Substrings

Para **acceder a un caracter de una variable string** usamos la sintaxis de `[]`

```python
s = "Soy fan de los videojuegos"
```

```python
s[0] # Primer caracter

#RESPUESTA
'S'
```

```python
s[5] # Sexto caracter

#RESPUESTA
'a'
```

**¡Cuidado!** En `Python`, los índices siempre empiezan en 0, al contrario de lo que ocurre con otros lenguajes de programación, como por ejemplo `R`.

Si precedemos el índice por un `-`, entonces **empezamos desde el final**

```python
s[-1] # Último elemento

#RESPUESTA
's'
```

```python
s[-7] # Séptimo elemento empezando por el final

#RESPUESTA
'o'
```

Si queremos acceder a varios caracteres seguidos, podemos utilizar la función `:`

```python
s[4:7] # Del quinto al séptimo

#RESPUESTA
'fan'
```

```python
s[:7] # Del primero al séptimo

#RESPUESTA
'Soy fan'
```

```python
s[8:] # Del noveno al final

#RESPUESTA
'e los videojuegos'
```

**¡Cuidado!** En `Python`, siempre que usemos la función `:`, el índice que se encuentra a la derecha nunca es incluido, tal y como hemos visto en los ejemplos anteriores.

Si precedemos por `-` al índice de la izquierda de `:` y no ponemos ninguno a su derecha, lo que hacemos es **obtener los últimos elementos**. No se puede acceder al -0, se accede al -1 como último elemento.

```python
s[-10:] # Diez últimos elementos

#RESPUESTA
'ideojuegos'
```

Si al contrario, precedemos por `-` al índice de la derecha, sin poner ningún índice a la izquierda de `:`, **obtendremos todos los elementos salvo el número de elementos del final indicados por el índice** (recordemos que si precedíamos por `-`, los índices empezaban desde el final).

```python
s[:-10]

#RESPUESTA
'Soy fan de los v'
```

Estos substrings pueden contar con un tercer elemento que marca los espaciosa saltar desde el punto inicial al punto inicial.

**`string[1:5:1]` implicará desde la segunda posición (1) hasta la quinta (4) de uno en uno.**

### Revertir un string

Puesto que en Python no existe un método .reverse() para las strings, podemos utilizar una substring que vaya desde el primer caracter hasta el último con un salto de -1. Así conseguimos el efecto de reverse string.

PE: **`string[::-1]`** equivale a **`gnirts`**

## Métodos para trabajar con strings

El método `.lower()` nos transforma el string que indiquemos a minúsculas.

```python
s = "Me ENCANTAN el chocolate y las galletas"
s.lower()

#RESPUESTA
'me encantan el chocolate y las galletas'
```

El método `.upper()`, por el contrario, lo transforma a mayúsculas.

```python
s.upper()

#RESPUESTA
'ME ENCANTAN EL CHOCOLATE Y LAS GALLETAS'
```

El método `.count()` cuenta cuántas veces aparece una letra o un string dentro del string al cuál le aplicamos dicho método.

```python
s.count("o")

#RESPUESTA
2
```

```python
s.count("la")

#RESPUESTA
2
```

El método `.capitalize()` convierte a mayúscula el primer caracter de un string.

```python
s = "me encanta aprender con udemy"
s.capitalize()

#RESPUESTA
'Me encanta aprender con udemy'
```

El método `.title()` convierte a mayúscula el primer caracter de cada palabra de un string.

```python
s.title()

#RESPUESTA
'Me Encanta Aprender Con Udemy'
```

El método `.swapcase()` convierte a mayúscula las minúsculas y viceversa.

```python
s = "Me ENCANTA aprender con Udemy"
s.swapcase()

#RESPUESTA
'mE encanta APRENDER CON uDEMY'
```

El método `.replace()` reemplaza el caracter (o caracteres) que le indiquemos por el string que queramos.

```python
s = "Los tomberis son buenos"
s.replace("buenos", "malos")

#RESPUESTA
'Los tomberis son malos'
```

El método `.split()` rompe el string en el caracter que le indiquemos y elimina dicho caracter.

```python
s = "El elefante tiene las orejas muy grandes"
s.split("e") # Rompemos por la letra e minúscula

#RESPUESTA
['El ', 'l', 'fant', ' ti', 'n', ' las or', 'jas muy grand', 's']
```

```python
s.split(" ") # Rompemos por los espacios

#RESPUESTA
['El', 'elefante', 'tiene', 'las', 'orejas', 'muy', 'grandes']
```

```python
s.split("tiene") # Rompemos por la palabra tiene

#RESPUESTA
['El elefante ', ' las orejas muy grandes']
```

El método `.strip()` elimina los espacios sobrantes a principio y final del string.

```python
s = "       El elefante tiene las orejas muy grandes        "
s.strip()

#RESPUESTA
'El elefante tiene las orejas muy grandes'
```

El método `.rstrip()` elimina los espacios sobrantes al final del string.

```python
s.rstrip()

#RESPUESTA
'       El elefante tiene las orejas muy grandes'
```

El método .lstrip() elimina los espacios sobrantes al principio del string.

```python
s.lstrip()


#RESPUESTA
'El elefante tiene las orejas muy grandes        '
```

El método `.find()` busca el carácter que indiquemos y nos devuelve la primera posición en la que aparece (empezando por 0).

```python
s = "Este es un curso de Python para hacer en casa o en cualquier lado"
s.find("e")

#RESPUESTA
3
```

Si le pedimos buscar un conjunto de caracteres, nos devuelve la posición del primer carácter de dicho conjunto

```python
s.find("casa")

#RESPUESTA
41
```

El método `.find()` tiene otros dos parámetros de uso opcional: `start` y `end`, que sirven para indicar donde queremos que empiece la búsqueda y donde queremos que acabe.

```python
s.find("e", 10) # Solamente indicamos start

#RESPUESTA
18
```

```python
s.find("e", 30, 40) # Indicamos start y end

#RESPUESTA
35
```

El método `.index()` busca el carácter que indiquemos y nos devuelve la primera posición en la que aparece.

```python
s = "Este es un curso de Python para hacer en casa o en cualquier lado"
s.index("e")

#RESPUESTA
3
```

Si le pedimos buscar un conjunto de caracteres, nos devuelve la posición del primer carácter de dicho conjunto

```python
s.index("casa")

#RESPUESTA
41
```

El método `.index()` tiene otros dos parámetros de uso opcional: `start` y `end`, que sirven para indicar donde queremos que empiece la búsqueda y donde queremos que acabe.

```python
s.index("e", 10) # Solamente indicamos start

#RESPUESTA
18
```

```python
s.index("e", 30, 40) # Indicamos start y end

#RESPUESTA
35
```

**Observación.** Observemos que los métodos `.index()` y `.find()` son casi idénticos. El único punto en que difieren es que si el carácter indicado no se encuentra en el string, el método `.index()` arroja error, mientras que `.find()` arroja el índice -1.

El método `.rindex()` busca el carácter que indiquemos y devuelve el último indice en el que fue encontrado.

```python
s.rindex("e")

#RESPUESTA
58
```

También consta de los dos parámetros de uso opcional: `start` y `end`, que sirven para indicar donde queremos que empiece la búsqueda y donde queremos que acabe.

## Otras funciones a tener en cuenta

La función `len()` nos devuelve el número de caracteres del string.

```python
s = "Tengo hambre"
len(s)

#RESPUESTA
12
```

**Observación.** Los espacios en blanco también son caracteres, por lo que éstos también son incluidos al contar el número de caracteres de los que consta un string.

Si tenemos un número en formato string, por mucho que sea un número para nosotros, en realidad `Python` no lo ve así. El gran problema es cuando queremos operar con un número que se encuentra en formato string. Ahí es donde entran en juego las funciones `int()` y `float()`, que lo que hacen es convertir a formato integer o float, respectivamente.

```python
numero = "5" 
type(numero)

#RESPUESTA
str
```

En este caso, pasamos a formato integer:

```python
numero_int = int(numero)
numero_int

#RESPUESTA
5
```

```python
numero_int ** 2

#RESPUESTA
25
```

```python
numero_int ** 2

#RESPUESTA
25
```

```python
type(numero_int)

#RESPUESTA
int
```

En este otro caso, pasamos a formato float:

```python
numero_float = float(numero)
numero_float

#RESPUESTA
5.0
```

```python
numero_float ** 2 - numero_float

#RESPUESTA
20.0
```

```python
type(numero_float)

#RESPUESTA
float
```

La función `input()` sirve para que el usuario introduzca un string por consola:

```python
print("Introduce tu nombre: ")
name = input("Nombre: ")

#RESPUESTA
Introduce tu nombre: 
Nombre: Juan Juan Juan
```

```python
name

#RESPUESTA
'Juan Juan Juan'
```

Aquí también nos serán útiles las funciones `int()` y `float()`, pues si en vez del nombre queremos que el usuario nos indique su edad o su altura, querremos tratar dichos valores como números. Entonces, haríamos lo siguiente

```python
print("Introduce tu edad: ")
age = int(input("Edad: "))

#RESPUESTA
Introduce tu edad: 
Edad: 32
```

```python
print("Introduce tu altura: ")
height = float(input("Altura (en m): "))

#RESPUESTA
Introduce tu altura: 
Altura (en m): 1.66
```

```python
print("La edad de {} es {} y mide {}m".format(name, age, height))

#RESPUESTA
La edad de Juan Gabriel Gomila es 32 y mide 1.66m
```

#### Ejercicio 2: substrings y eliminación de palabras.

Dado un string, vamos a pedir al usuario que introduzca una palabra perteneciente a dicho string y vamos a obtener el substring sin la palabra indicada por el usuario utilizando el método `.find()` y la función `len()`

```python
string= "El camino está cerrado pero seguro que podemos encontrar una alternativa\n"
print("Esta es la string original:", end = " ")
print(s1)

word= input("¿Qué palabra desea eliminar del string original?: ")

idx= string.find(word) # Obtenemos así la posicion del primer caracter de la palabra a eliminar
result= string[:idx] + string[(idx + len(word) + 1):] # Aquí generamos una substring hasta el indice de la primera letra de la palabra a eliminar
                                                      # más el substring despues del (indice + longitud de la palabra +1) Así evitamos el doble espacio en la unión.
print(result)
```

```python
#RESPUESTA
Esta es la string original: El camino está cerrado pero seguro que podemos encontrar una alternativa

¿Qué palabra desea eliminar del string original?: que
El camino está cerrado pero seguro podemos encontrar una alternativa
```

#### Ejercicio 3: personalizar la canción de cumpleaños feliz

Vamos a aprovechar el ejercicio sobre la canción "Cumpleaños feliz" y vamos a permitir al usuario elegir a quien va dirigida la canción

```python
#Opción 1: modificamos s2 para que no ponga "todos" y luego añadimos la variable name detras.
s1 = "¡Cumpleaños feliz!"
s2 = "Te deseamos "
name = input("¿De quien es el cumpleaños?: ")

song = "\n" + (s1 + "\n") * 2 + s2 + name + ",\n" + s1
print(song)
```

```
#RESPUESTA
¿De quien es el cumpleaños?: a

¡Cumpleaños feliz!
¡Cumpleaños feliz!
Te deseamos a,
¡Cumpleaños feliz!
```

```python
#Opción 2: utilizamos el método .replace() para reemplazar una substring por otra.
print("Indica el destinitario de la canción:")
name = input()

s1 = "¡Cumpleaños feliz!"
s2 = "Te deseamos todos"

song = (s1 + "\n") * 2 + s2.replace("todos", name) + ",\n" + s1
print(song)
```

#### Ejercicio 4: Metodos variados

Vamos a pedirle al usuario palabras o frases y le vamos a devolver el mismo string modificado con alguno de los métodos aprendidos según se indique:

1. Devolver la palabra en mayúscula
2. Devolver la frase con todas las palabras empezando en mayúscula
3. Devolver la palabra (con 3 o más letras) con todas las letras en minúscula salvo la tercera letra
4. Devolver la palabra con todas las letras en mayúsculas salvo la primera y la última
5. Devolver la frase donde cada vez que aparezcan las dos primeras letras de la primera palabra, sean substituidas por cualesquiera otras dos letras.

```python
greeting = "Vamos a pedirle al usuario palabras o frases y le vamos a devolver el mismo string modificado con alguno de los métodos aprendidos según se indique\n"
print(greeting)

part1 = "Introducirá una palabra en minúscula y se convertirá en mayuscula."
print(part1)
word1 = input("palabra en minuscula: ")
print("su palabra en mayuscula es: " + word1.upper() + "\n")

part2 = "Introducirá una frase en minuscula, mayuscula o combinación de ambas y se devolverá con la primera letra de cada palabra en mayuscula."
print(part2)
phrase2 = input("introduzca su frase: ")
print("su frase \"Capitalizada\" es: " + phrase2.title() + "\n")

part3 = "Introducirá una palabra con más de 3 caracteres en la que se convertirá a diferentes opciones."
print(part3)
word3 = input("introduzca su palabra de más de 3 letras: ")
print("Su palabra con la tercera letra en mayusculas y el resto en minusculas es: " + word3[:2].lower() + word3[2].upper() + word3[3:].lower() + "\n")

part4 = "Ahora se va a trabajar con la palabra anterior para ponerla en mayusculas salvo la primera y la última."
print("Su palabra con todas las letras en mayuscula menos la primera y la última es: " + word3[0].lower() + word3[1:-1].upper() + word3[-1].lower() + "\n")

part5 = "Por último, utilizando la frase del apartado 2, vamos a sustituir las dos primeras letras de la primera palabra, cada vez que aparezcan por x y z."
cha1 = phrase2[:2]
print( "Atento: " + phrase2.replace(cha1, "xy"))
```

#### Ejercicio 5: Años de vida

Vamos a pedirle al usuario su año de nacimiento y el año actual y le vamos a imprimir por pantalla su edad

```python
ex5 = "Introduzca su año de nacimiento y el año actual para saber su edad."
print(ex5)
born = input("Introduzca su año de nacimiento: ")
current = input("Introduzca el año actual: ")
years = int(current) - int(born)
print("Tienes " + str(years) + " años.")
```

```
Introduzca su año de nacimiento y el año actual para saber su edad.
Introduzca su año de nacimiento: 1994
Introduzca el año actual: 2021
Tienes 27 años.
```

### Repaso

```python
#Ejercicio 1: Había una vez, un barquito chiquitito
#Había una vez, un barquito chiquitito que no podía, que no podía, que no podía navegar.

s1 = "Había una vez, "
s2 = "un barquito chiquitito "
s3 = "que no podía, "
s4 = "que no podía navegar."
print((s1 + s2) * 2 + s2 *2 + s3)

#RESPUESTA
Había una vez, un barquito chiquitito Había una vez, un barquito chiquitito un barquito chiquitito un barquito chiquitito que no podía, 
```

```python
#Ejercicio2: Utiliza la función print() y el comando de salto de línea, \n, para reproducir exactamente el siguiente texto.
#Érase un hombre a una nariz pegado,
#Érase una nariz superlativa,
#Érase una alquitara medio viva,
#Érase un peje espada mal barbado;
print("Érase un hombre a una nariz pegado,\nÉrase una nariz superlativa,\nÉrase una alquitara medio viva,\nÉrase un peje espada mal barbado;")
```

```python
#RESPUESTA
Érase un hombre a una nariz pegado,
Érase una nariz superlativa,
Érase una alquitara medio viva
Érase un peje espada mal barbado
```

```python
#Ejercicio 3: Transforma el siguiente string s a mayúsculas y muéstralo por pantalla con la función print():
s = "me encantan las matemáticas"
print(s.upper())

#RESPUESTA
ME ENCANTAN LAS MATEMÁTICAS
```

```python
#ejercicio 4: Calcula la longitud del string s
s = "Mi pasión por el chocolate es superior a mis fuerzas"
len(s)

#RESPUESTA
52
```

```python
#Ejercicio 5: Del string s del ejercicio anterior, obtén el substring chocolate y guárdalo en una variable llamada s_sub.
#No vale contar, deberás hallar los índices del substring con el método .find() (o el que mejor consideres) y
#la función len().
s = "Mi pasión por el chocolate es superior a mis fuerzas"
ind = s.find("chocolate")
lon = len("chocolate")
s_sub = s[ind:(ind + lon)]
print(s_sub)

#RESPUESTA
chocolate
```

```python
#Ejercicio 6: Con la función input(), indícale al usuario que introduzca su nombre y guárdalo en la variable llamada nombre
nombre = input("introduzca su nombre: ")

#RESPUESTA
introduzca su nombre: ain
```

```python
#Ejercicio 7: Con la función input(), indícale al usuario que introduzca su apellido y guárdalo en la variable llamada apellido
apellido = input("Introduzca su apellido: ")

#RESPUESTA
Introduzca su apellido: plosionado
```

```python
#Ejercicio 8: Con la función input(), indícale al usuario que introduzca su edad y guárdala en la variable llamada edad.
#¡Ojo con el tipo de dato!
edad = int(input("Introduzca su edad: "))

#RESPUESTA
Introduzca su edad: 30
```

```python
#Ejercicio 9: Con la función input(), indícale al usuario que introduzca la ciudad en la que vive y guárdala en la variable llamada ciudad.
ciudad = input("Introduzca la ciudad donde reside: ")

#RESPUESTA
Introduzca la ciudad donde reside: Bersalles
```

```python
#Ejercicio 10: Su nombre es María Santos, tiene 21 años y actualmente vive en Palma de Mallorca.
print("Su nombre es {} {}, tiene {} años y actualmente vive en {}.".format(nombre, apellido, edad, ciudad))

#RESPUESTA
Su nombre es ain plosionado, tiene 30 años y actualmente vive en Bersalles
```
