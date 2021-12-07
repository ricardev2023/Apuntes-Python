---
description: Explicación del uso de estructuras de datos tipo diccionarios en Python 3.
---

# Tema 7. Estructura de Datos. Diccionarios

## Diccionario

La segunda estructura de datos que veremos son los **diccionarios**. Éstos son un conjunto de elementos no ordenados escritos entre llaves, `{}`, que constan de claves y valores.

Cada conjunto `clave: valor` es separado por comas. Las claves funcionan como identificadores y preceden a `:`. A continuación van los valores, que son elementos (numéricos, booleanos, strings, listas, diccionarios...) asociados a esa clave.

Los diccionarios, al igual que las listas, son:

* **heterogéneos**: los elementos pueden ser de distinto tipo en un mismo diccionario
* **mutables**: los elementos pueden ser modificados

Un ejemplo de diccionario sería

```python
dicc = {"Jose": 32, "Marina": 21}
print(dicc)

#RESPUESTA
{'Jose': 32, 'Marina': 21}
```

**¡Cuidado!** En `Python`, las claves de un diccionario deben ser únicas. Esto es, no puede haber dos claves que sean exactamente iguales. Si se da que hay dos claves iguales, entonces `Python` se queda con el último valor asociado a dicha clave.

```python
dicc = {"Jose": 32,
        "Marina": 21,
        "Jose": 23}
print(dicc)

#RESPUESTA
{'Jose': 23, 'Marina': 21}
```

**Observación.** Al decir que los diccionarios no tienen orden, lo que ocurre es que `Python` no mantendrá el que hemos introducido, tal y como hacía con las listas, sino que reordenará todos los elementos por orden primero numérico (yendo antes los positivos que los negativos) y luego alfabético de las claves. Esto no ocurre si usamos la función `print()`.

```python
l = ["Jose", "Marina", "Elena"]
l

#RESPUESTA
['Jose', 'Marina', 'Elena']
```

```python
dicc = {"Jose": 32,
        "Marina": 21,
        "Elena": 10}
dicc

#RESPUESTA
{'Elena': 10, 'Jose': 32, 'Marina': 21}
```

```python
print(dicc)

#RESPUESTA
{'Jose': 32, 'Marina': 21, 'Elena': 10}
```

```python
dicc = {"Alba": 2, 7: "a", -5: "b", "Javi": 28}
dicc

#RESPUESTA
{-5: 'b', 7: 'a', 'Alba': 2, 'Javi': 28}
```

```python
print(dicc)

#RESPUESTA
{'Alba': 2, 7: 'a', -5: 'b', 'Javi': 28}
```

### Elementos de un diccionario

Anteriormente se ha comentado que los diccionarios no tienen orden. De modo que a sus elementos no se accede por posición, sino que debemos hacerlo mediante sus claves.

La sintaxis es `diccionario[clave]`

```python
dicc = {
    "names": ["Ana", "Borja", "Carmen"],
    "ages" : [31, 25, 16]
    }
dicc["names"]

#RESPUESTA
['Ana', 'Borja', 'Carmen']
```

```python
dicc["ages"]

#RESPUESTA
[31, 25, 16]
```

Podemos acceder a todas las claves de un diccionario con el método `.keys()`

```python
dicc.keys()

#RESPUESTA
dict_keys(['names', 'ages'])
```

También podemos acceder a todos los valores de un diccionario con el método `.values()`

```python
list(dicc.values())

#RESPUESTA
[['Ana', 'Borja', 'Carmen'], [31, 25, 16]]
```

Al ser una estructura mutable, podemos modificar los valores de los diccionarios

```python
dicc = {"names": ["Ana", "Borja", "Carmen"],
        "ages": [31, 25, 16]}
dicc["names"] = ["David", "Emilia", "Fernando"]
dicc["ages"][2] = 36
print(dicc)

#RESPUESTA
{'names': ['David', 'Emilia', 'Fernando'], 'ages': [31, 25, 36]}
```

_En el caso de la clave "ages" como dentro tenemos una lista, si que podemos acceder al segundo valor en orden._

También podríamos partir de un diccionario vacío e ir introduciéndole valores asociados a claves. De hecho, podemos hasta pedirle a un usuario que introduzca él los datos.

```python
ficha_usuario = {}
print("Introduzca su nombre:")
ficha_usuario["name"] = str(input())
print("Introduzca su edad:")
ficha_usuario["age"] = int(input())
print("¿Es usted una mujer? Responda f en caso afirmativo y m en caso contrario")
ficha_usuario["gender"] = "female" if input() == "f" else "male"
print(ficha_usuario)
```

```
#RESPUESTA
Introduzca su nombre:
Juan Gabriel Gomila
Introduzca su edad:
32
¿Es usted una mujer? Responda f en caso afirmativo y m en caso contrario
m
{'name': 'Juan Gabriel Gomila', 'age': 32, 'gender': 'male'}
```

**Observación.** La función de casting `str()` impone que lo que sea que introduzcamos sea un dato de tipo `string`. Funciona exactamente del mismo modo que lo hacen las funciones `int()` y `float()` introducidas y utilizadas en temas anteriores.

```python
value = 0
type(value)

#RESPUESTA
int
```

```python
value_string = str(0)
type(value_string)

#RESPUESTA
str
```

#### EJERCICIO 1:&#x20;

Vamos a hacer que el usuario rellene una ficha del cliente y vamos a guardar toda la información en un diccionario. Para ello, vamos a pedir el nombre, los apellidos, la edad, el dni y el dinero total que va a pagar el cliente.

```python
ficha_cliente = {}
print("+ Introduzca su nombre:")
ficha_cliente["first_name"] = str(input())
print("+ Introduzca sus apellidos:")
ficha_cliente["last_name"] = str(input())
print("+ Introduzca su edad:")
ficha_cliente["age"] = int(input())
print("+ Introduzca su número de DNI:")
ficha_cliente["NIF"] = int(input())
print("+ Introduzca el importe a pagar:")
ficha_cliente["Money"] = float(input())

print(ficha_cliente)
```

```
#RESPUESTA
+ Introduzca su nombre:
a
+ Introduzca sus apellidos:
b
+ Introduzca su edad:
1
+ Introduzca su número de DNI:
111222333
+ Introduzca el importe a pagar:
123.4
{'first_name': 'a', 'last_name': 'b', 'age': 1, 'NIF': 111222333, 'Money': 123.4}
```

### Tamaño de un diccionario

Para saber cuántos elementos contiene un diccionario, podemos usar la función `len()`del siguiente modo:

```python
dicc = {"fruit": ["Manzana", "Pera", "Naranja", "Melon"],
        "price": [2, 1.5, 1],
        "color": ["roja", "verde", "naranja"]}
        
print(len(dicc))
print(len(dicc["fruit"]))

#RESPUESTA
3
4
```

## Bucles y diccionarios

Para recorrer todo el diccionario, podemos hacer uso de un bucle `for`, pues el diccionario es una estructura iterable:

```python
dicc = {"username": "msf",
        "name": "María",
        "age": 22,
        "city": "Palma de Mallorca"}

for key in dicc:
  print(key, ":", dicc[key])
```

```
#RESPUESTA
username : msf
name : María
age : 22
city : Palma de Mallorca
```

Otra forma de recorrer el diccionario sería obteniendo una lista de tuplas de la forma `(clave, valor)` para cada elemento de un diccionario, que construimos con el método `.items()`. Al ser una lista, sabemos que es iterable y podemos mostrar todas sus entradas haciendo uso de un bucle `for`.

```python
dicc.items()

#RESPUESTA
dict_items([('username', 'msf'), ('name', 'María'), ('age', 22), ('city', 'Palma de Mallorca')])
```

```python
for item in dicc.items():
  print(item)
```

```
#RESPUESTA
('username', 'msf')
('name', 'María')
('age', 22)
('city', 'Palma de Mallorca')
```

**Observación.** Veremos las tuplas, que son otro tipo de Estructuras de datos en `Python`, en futuras secciones.

Para tener clave y valor por separado, podemos hacerlo del siguiente modo:

```python
for key, value in dicc.items():
  print(key, ":", value)
```

```
#RESPUESTA
username : msf
name : María
age : 22
city : Palma de Mallorca
```

## Diccionarios y listas

Como se ha mencionado antes, un diccionario puede contener listas u otros diccionarios. Por su parte, una lista también puede contener diccionarios:

```python
dicc_1 = {"name": "Elisa",
        "age": 30,
        "gender": "female",
        "ID": [4, 4, 2, 1, 5, 6, 7, 2, "L"],
        "user&password": {
            "username": "eli88",
            "password": "1234catsareawesome"
            }
          }
dicc_2 = {"name": "Henry",
        "age": 27,
        "gender": "male",
        "ID": [1, 1, 0, 1, 3, 8, 6, 9, "A"],
        "user&password": {
            "username": "superhenry",
            "password": "1432superme"
            }
          }
lista = [dicc_1, dicc_2]

for item in lista:
  print(item)
```

```
#RESPUESTA
{'name': 'Elisa', 'age': 30, 'gender': 'female', 'ID': [4, 4, 2, 1, 5, 6, 7, 2, 'L'], 'user&password': {'username': 'eli88', 'password': '1234catsareawesome'}}
{'name': 'Henry', 'age': 27, 'gender': 'male', 'ID': [1, 1, 0, 1, 3, 8, 6, 9, 'A'], 'user&password': {'username': 'superhenry', 'password': '1432superme'}}
```

#### EJERCICIO 2:&#x20;

Tenemos un diccionario con 5 claves: Math, English, History, Science, IT. Cada clave contiene una lista de tamaño 3, donde cada una de esas entradas se corresponde con una nota de 0 a 10. El usuario va a ser quien introduzca esas notas por teclado. Finalmente, para cada clave, mostraremos la media de las 3 notas.

PISTA: Necesitarás la función sum().

```python
grades = {"math"    : [],
          "english" : [],
          "history" : [],
          "science" : [],
          "IT"      : []
         }

for key in grades:
    print("===", key, "===")
    for item in range(1,4):
        grades[key].append(float(input("Nota del {} cuatrimestre: ".format(item))))

print("\n Medias por asignatura:")
for key, val in grades.items():
  print(key, ":", sum(val)/len(val))
```

```
#RESPUESTA
=== math ===
Nota del 1 cuatrimestre: 5
Nota del 2 cuatrimestre: 6
Nota del 3 cuatrimestre: 8
=== english ===
Nota del 1 cuatrimestre: 4
Nota del 2 cuatrimestre: 2
Nota del 3 cuatrimestre: 3
=== history ===
Nota del 1 cuatrimestre: 6
Nota del 2 cuatrimestre: 9
Nota del 3 cuatrimestre: 8
=== science ===
Nota del 1 cuatrimestre: 7
Nota del 2 cuatrimestre: 8
Nota del 3 cuatrimestre: 5
=== IT ===
Nota del 1 cuatrimestre: 4
Nota del 2 cuatrimestre: 2
Nota del 3 cuatrimestre: 8

 Medias por asignatura:
math : 6.333333333333333
english : 3.0
history : 7.666666666666667
science : 6.666666666666667
IT : 4.666666666666667
```

## Más métodos de diccionarios

El método `.clear()` elimina todos los elementos del diccionario dejándolo vacío.

```python
dicc = {"a": 4, "b": 3, "c": 2, "d": 1}
print(dicc)

dicc.clear()
print(dicc)
```

```
#RESPUESTA
{'a': 4, 'b': 3, 'c': 2, 'd': 1}
{}
```

El método `.copy()` devuelve una copia del diccionario original.

```python
dicc = {"a": 4, "b": 3, "c": 2, "d": 1}
dicc_copy = dicc.copy()

print(dicc_copy)

#RESPUESTA
{'a': 4, 'b': 3, 'c': 2, 'd': 1}
```

El método `dict.fromkeys()` recibe como parámetros un iterable y un valor y devuelve un diccionario que contiene como claves los elementos del iterable con el mismo valor ingresado.

```python
dicc = dict.fromkeys(["a", "b", "c", "d", "e"], [1, 2, 3, 4])
print(dicc)

#RESPUESTA
{'a': [1, 2, 3, 4], 'b': [1, 2, 3, 4], 'c': [1, 2, 3, 4], 'd': [1, 2, 3, 4], 'e': [1, 2, 3, 4]}
```

**Observación.** Si el parámetro valor se deja en blanco, el método devolverá un diccionario con el valor `None` para todas las claves.

```python
dicc = dict.fromkeys(["a", "b", "c", "d", "e"])
print(dicc)

#RESPUESTA
{'a': None, 'b': None, 'c': None, 'd': None, 'e': None}
```

El método `.get()` recibe como parámetro una clave y devuelve el valor de dicha clave.

```python
dicc = {"a": 1, "e": 2, "i": 3, "o": 4, "u": 5}
print(dicc.get("a"))

#RESPUESTA
1
```

**Observación.** Si la clave no se encuentra en el diccionario, el método devuelve un objeto `None`.

```python
dicc = {"a": 1, "e": 2, "i": 3, "o": 4, "u": 5}
print(dicc.get("b"))

#RESPUESTA
None
```

El método `.pop()` recibe como parámetro una clave, la elimina y devuelve su valor.

```python
dicc = {"a": 1, "e": 2, "i": 3, "o": 4, "u": 5}
print(dicc)

print(dicc.pop("i"))
print(dicc)

#RESPUESTA
{'a': 1, 'e': 2, 'i': 3, 'o': 4, 'u': 5}
3
{'a': 1, 'e': 2, 'o': 4, 'u': 5}
```

**Observación.** Si la clave indicada por parámetro no se encuentra en el diccionario, el método devuelve error.

El método `.setdefault()` puede funcionar de dos formas:

* Como el método `.get()`
* Para agregar un nuevo elemento al diccionario.

```python
# Como .get()
dicc = {"a": 1, "e": 2, "i": 3, "o": 4, "u": 5}
print(dicc.setdefault("i"))

# Para agregar nuevo elemento
print(dicc.setdefault("ü", 6))
print(dicc)
```

```
#RESPUESTA
3
6
{'a': 1, 'e': 2, 'i': 3, 'o': 4, 'u': 5, 'ü': 6}
```

El método `.update()` recibe como parámetro otro diccionario. En caso de tener claves iguales, actualiza el valor de la clave repetida. En caso de no haber claves iguales, el par `clave: valor` es agregado al diccionario al que es aplicado el método.

```python
dicc1 = {"a": 1, "e": 2, "i": 3, "o": 4, "u": 5}
dicc2 = {"a": 1, "b": 2, "c": 3, "d": 4, "e": 5}
dicc1.update(dicc2)

print(dicc1)

#RESPUESTA
{'a': 1, 'e': 5, 'i': 3, 'o': 4, 'u': 5, 'b': 2, 'c': 3, 'd': 4}
```

#### EJERCICIO 3:&#x20;

Dado un diccionario, vamos a solicitar al usuario una clave que quiera eliminar y vamos a eliminarla. Al final, le mostraremos el diccionario actualizado.

```python
dicc = {"a": 1, "e": 2, "i": 3, "o": 4, "u": 5}
print("+ Este es el diccionario original\n", dicc)

print("\n+ Introduzca la clave que quiere eliminar del diccionario:")
dicc.pop(input(""))

print("\+ Este es el diccionario actualizado\n", dicc)
```

```
#RESPUESTA
+ Este es el diccionario original
 {'a': 1, 'e': 2, 'i': 3, 'o': 4, 'u': 5}

+ Introduzca la clave que quiere eliminar del diccionario:
e
\+ Este es el diccionario actualizado
 {'a': 1, 'i': 3, 'o': 4, 'u': 5}
```

## Construyendo diccionarios con dict()

Para convertir un objeto iterable de `Python` a diccionario, hay que usar la función `dict()`

```python
l = [["x", 1], ["y", 2]]
dict(l)

#RESPUESTA
{'x': 1, 'y': 2}
```

Aunque la función `dict()` también sirve para definir diccionarios directamente:

```python
dicc1 = dict(x = 0, y = 1, z = -1)
print(dicc1)

#RESPUESTA
{'x': 0, 'y': 1, 'z': -1}
```

```python
dicc2 = dict({"x": 0, "y": 1, "z": -1})
print(dicc2)

#RESPUESTA
{'x': 0, 'y': 1, 'z': -1}
```

```python
dicc3 = dict({"x": 0}, y = 1, z = -1)
print(dicc3)

#RESPUESTA
{'x': 0, 'y': 1, 'z': -1}
```

#### EJERCICIO 4:&#x20;

Vamos a solicitar al usuario 8 números enteros del 0 al 9. Se supone que son los números de su DNI, que guardaremos cada uno en una entrada de una lista. A continuación, con esos números calcularemos la letra correspondiente y la guardaremos en una variable. Finalmente, crearemos un diccionario con dos claves, cada una guardará, respectivamente, los números y la letra del DNI. Finalmente, mostraremos el diccionario resultante.

```python
dni = []

for item in range(8):
    dni.append(int(input("Introduzca el {} de su DNI: ".format(item + 1))))
total_dni = 0

for item in dni:
    total_dni += item
letras_dni = ["T", "R", "W", "A", "G", "M", "Y", "F", "P", "D", "X", "B", "N", "J", "Z", "S", "Q", "V", "H", "L", "C", "K", "E"] 
letra = letras_dni[total_dni % 23]

dicc = {"numero_dni" : dni, "letra_dni" : letra}

print(dicc)
```

```
#RESPUESTA
Introduzca el 1 de su DNI: 5
Introduzca el 2 de su DNI: 6
Introduzca el 3 de su DNI: 3
Introduzca el 4 de su DNI: 5
Introduzca el 5 de su DNI: 8
Introduzca el 6 de su DNI: 4
Introduzca el 7 de su DNI: 1
Introduzca el 8 de su DNI: 2
{'numero_dni': [5, 6, 3, 5, 8, 4, 1, 2], 'letra_dni': 'B'}
```

#### EJERCICIO 5:&#x20;

Vamos a leer un string por teclado y vamos a devolver un diccionario con la cantidad de apariciones de cada caracter en el string proporcionado por el usuario.

```python
print("+ Introduce una frase:")
s = input("")

counted = []
counter = {}
s = s.lower()
for i in s:
    if i not in counted:
        counter[i.upper()] = (s.count(i))
        counted.append(i)

for key, value in counter.items():
    print(key, " : ",  value)
```

```
#RESPUESTA
+ Introduce una frase:
hola que ase tio duro
H  :  1
O  :  3
L  :  1
A  :  2
   :  4
Q  :  1
U  :  2
E  :  2
S  :  1
T  :  1
I  :  1
D  :  1
R  :  1
```

## REPASO

```python
#EJERCICIO 1: Crea un programa que pida un número entero positivo por teclado y que cree un diccionario cuyas claves
#sean desde el número 1 hasta el número indicado. Los valores de cada clave serán las propias claves elevadas
#al cubo.

n = int(input("Introduzca un número entero positivo: "))
if n < 0:
    print("El número {} es negativo.").format(n)
elif n == 0:
    print("El número indicado es cero.")
else:
    dicc = {}
    for i in range(1, n+1):
        dicc[i] = i ** 3
print(dicc)
```

```
#RESPUESTA
Introduzca un número entero positivo: 2
{1: 1, 2: 8}
```

```python
#EJERCICIO 2:Escribe un programa que pregunte al usuario su nombre, edad y teléfono y lo guarde en un diccionario.
#Después, debe mostrar por pantalla el mensaje ‘{nombre} tiene {edad} años y su número de teléfono es {teléfono}.

ficha = {}
print("Introduzca su nombre:")
ficha["nombre"] = str(input(""))
print("Introduzca su edad:")
ficha["edad"] = int(input(""))
print("Introduzca su teléfono:")
ficha["telefono"] = int(input(""))

print("{} tiene {} años y su número de teléfono es {}".format(ficha["nombre"], ficha["edad"], ficha["telefono"]))
```

```
#RESPUESTA
Introduzca su nombre:
a
Introduzca su edad:
22
Introduzca su teléfono:
112233
a tiene 22 años y su número de teléfono es 112233
```

```python
#EJERCICIO 3: Escribe un programa que cree un diccionario simulando una cesta de la compra. El programa debe preguntar
#el artículo y su precio por unidad. El artículo será la clave y el valor el precio, hasta que el usuario decida
#terminar. Después se debe mostrar por pantalla la lista de la compra y el coste total, con el siguiente formato

shopping_list = {}
n = " "
while n != "":
    print("Introduzca el nombre del artículo (para terminar presione solo enter):")
    n = str(input(""))
    if n == "":
        break
    else:
        shopping_list[n] = int(input("Introduzca el precio: "))
total = 0
print("--------------------------------")
for key, item in shopping_list.items():
    print(key, "\t", item)
    total += item
print("\nTOTAL\t", total)
print("--------------------------------")
```

```
#RESPUESTA
Introduzca el nombre del artículo (para terminar presione solo enter):
asd
Introduzca el precio: 54
Introduzca el nombre del artículo (para terminar presione solo enter):
asdew
Introduzca el precio: 54165
Introduzca el nombre del artículo (para terminar presione solo enter):

--------------------------------
asd 	 54
asdew 	 54165

TOTAL	 54219
--------------------------------
```

```python
#EJERCICIO 4: Crea un programa que lea números enteros hasta que introduzca el 0 y devuelva un diccionario con la cantidad números positivos y negativos introducidos.

numeros = {"positivos" : 0,
           "negativos" : 0
          }
n = 1

while n != 0:
    n = int(input("Introduzca un número entero diferente de 0: "))
    if n == 0:
        break
    elif n > 0:
        numeros["positivos"] += 1
    else:
        numeros["negativos"] += 1

for key, item in numeros.items():
    print(key, "\t", item)
```

```
#RESPUESTA
Introduzca un número entero diferente de 0: 1
Introduzca un número entero diferente de 0: -1
Introduzca un número entero diferente de 0: 1
Introduzca un número entero diferente de 0: -1
Introduzca un número entero diferente de 0: 0
positivos 	 2
negativos 	 2
```

```python
#EJERCICIO 5: Crea un programa que lea números enteros hasta que introduzca el 0 y devuelva un diccionario con la cantidad números pares e impares introducidos.

numeros = {"pares" : 0,
           "impares" : 0
          }
n = 1

while n != 0:
    n = int(input("Introduzca un número entero diferente de 0: "))
    if n == 0:
        break
    else:
        if n % 2 == 0:
            numeros["pares"] += 1
        else:
            numeros["impares"] += 1

for key, item in numeros.items():
    print(key, "\t", item)
```

```
#RESPUESTA
Introduzca un número entero diferente de 0: 1
Introduzca un número entero diferente de 0: 2
Introduzca un número entero diferente de 0: 3
Introduzca un número entero diferente de 0: 4
Introduzca un número entero diferente de 0: 5
Introduzca un número entero diferente de 0: 6
Introduzca un número entero diferente de 0: 7
Introduzca un número entero diferente de 0: 8
Introduzca un número entero diferente de 0: 9
Introduzca un número entero diferente de 0: 0
pares 	 4
impares 	 5
```

```python
#EJERCICIO 6: Crea un programa que permita al usuario introducir los nombres de los alumnos de una clase y las notas que
#han obtenido. Cada alumno puede tener distinta cantidad de notas. Guarda la información en un diccionario
#cuyas claves serán los nombres de los alumnos y los valores serán listas con las notas de cada alumno.
#El programa va a pedir el número de alumnos que vamos a introducir, pedirá su nombre e irá pidiendo sus
#notas hasta que introduzcamos un número negativo. Al final el programa nos mostrará la lista de alumnos
#y la nota media obtenida por cada uno de ellos.
#PISTA: Vas a necesitar la función sum().

alumnos = {}
n = int(input("Introduzca el número de alumnos que van a ser evaluados: "))
if n <= 0:
    print("Es imposible evaluar ese número de alumnos.")
else:
    for i in range(n):
        nombre = str(input("Introduzca el nombre del alumno: "))
        notas = []
        nota = 0
        while nota >= 0:
            nota = float(input("Introduzca una nota del alumno: "))
            if nota < 0:
                break
            else:
                notas.append(nota)
        alumnos[nombre] = notas
    print("\n---------------------------\nALUMNO\tNOTA\n
    ")
    for key, item in alumnos.items():
        print(key, "\t", sum(item) / len(item))
```

```
#RESPUESTA
Introduzca el número de alumnos que van a ser evaluados: 2
Introduzca el nombre del alumno: edu
Introduzca una nota del alumno: 5
Introduzca una nota del alumno: 5
Introduzca una nota del alumno: 5
Introduzca una nota del alumno: 10
Introduzca una nota del alumno: -1
Introduzca el nombre del alumno: erik
Introduzca una nota del alumno: 10
Introduzca una nota del alumno: 10
Introduzca una nota del alumno: 10
Introduzca una nota del alumno: 6
Introduzca una nota del alumno: -1
---------------------------
ALUMNO	NOTA

edu 	 6.25
erik 	 9.0
```

```python
#EJERCICIO 7: Crea un programa que pida un número entero positivo por teclado y que cree un diccionario cuyas claves
#sean desde el número 1 hasta el número indicado. Los valores de cada clave serán tantos símbolos "*" como
#indique la clave.

n = int(input("Introduzca un número entero positivo: "))
if n < 0:
    print("El número {} es negativo.").format(n)
elif n == 0:
    print("El número indicado es cero.")
else:
    dicc = {}
    for i in range(1, n+1):
        dicc[i] = "*" * i
print(dicc)
```

```
#RESPUESTA
Introduzca un número entero positivo: 5
{1: '*', 2: '**', 3: '***', 4: '****', 5: '*****'}
```

```python
#EJERCICIO 8: Crea un programa que pida el número de palabras a introducir. Crear un diccionario de clave la palabra y de valor la longitud de dicha palabra.

n_words = int(input("Introduzca el número de palabras a introducir: "))
if n_words <= 0:
    print("No se puede utilizar ese número de palabras.")
else:
    palabras = {}

    for i in range(n_words):
        word = input("Introduzca la palabra: ")
        palabras[word] = len(word)
    for key, item in palabras.items():
        print(key, "\t", item)
```

```
#RESPUESTA
Introduzca el número de palabras a introducir: 2
Introduzca la palabra: poltergueist
Introduzca la palabra: supercalifragilisticoespialidoso
poltergueist 	 12
supercalifragilisticoespialidoso 	 32
```

```python
#EJERCICIO 9: Crea un programa que pida el número de palabras a introducir. Crear un diccionario de clave la palabra y de valor el número de vocales de la palabra.

n_words = int(input("Introduzca el número de palabras a introducir: "))
if n_words <= 0:
    print("No se puede utilizar ese número de palabras.")
else:
    palabras = {}

    for i in range(n_words):
        word = input("Introduzca la palabra: ")
        count = 0
        for i in word:
            if i == "a" or i == "e" or i == "i" or i == "o" or i == "u":
                count += 1
        palabras[word] = count
    for key, item in palabras.items():
        print(key, "\t", item)
```

```
#RESPUESTA
Introduzca el número de palabras a introducir: 2
Introduzca la palabra: supercalifragilisticoespialidoso
Introduzca la palabra: hermano
supercalifragilisticoespialidoso 	 15
hermano 	 3
```

```python
#EJERCICIO 10: Dada una matriz, crea un diccionario que guarde el número de filas, el de columnas y cada fila en una entrada de un diccionario.

matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

dicc = {}
dicc["filas"] = len(matrix)
dicc["columnas"] = len(matrix[0])

for n in range(len(matrix)):
    dicc["fila " + str(n + 1)] = matrix[n]
print(dicc)

#RESPUESTA
{'filas': 3, 'columnas': 3, 'fila 1': [1, 2, 3], 'fila 2': [4, 5, 6], 'fila 3': [7, 8, 9]}
```
