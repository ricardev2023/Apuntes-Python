---
description: >-
  Explicación de la creación, apertura, cierre y edición de archivos en Python
  3.
---

# Tema 14. Archivos TXT y CSV

## Archivos TXT

### Leyendo el primer `txt`

Vamos a crear un archivo `txt` con el editor de textos que diga:

```
"¡Qué ilusión! Vamos a cargar por primera vez un archivo txt con Python"
```

y lo guardaremos en la carpeta datasets con el nombre `first_read.txt`.

A continuación, vamos a cargar el archivo que acabamos de crear en este mismo notebook. Para ello vamos a usar la función `open()` y los métodos `.read()` y `.close()`, para abrir, leer y cerrar, respectivamente, el archivo `txt`.

```python
f = open("/content/drive/MyDrive/python-basico/datasets/first_read.txt")
print(f.read())
f.close()
```

* La función `open()` abre el archivo indicado y nos permite acceder a él. Como parámetro necesita el path del archivo que queremos abrir.
* El método `.read()` lo usamos para leer el contenido del output que nos proporciona la función `open()` al cual hemos llamado `f`
* Cuando hayamos acabado de trabajar con el archivo `f`, hay que cerrarlo. Este proceso se lleva a cabo con el método `.close()`

Otra forma de abrir el archivo y guardarlo en la variable `f` sería:

```python
with open("/content/drive/MyDrive/python-basico/datasets/first_read.txt") as f:
  print(f.read())
```

**Observación.** Con esta nueva sintaxis ya no es necesario hacer uso del método `.close()` para cerrar el archivo `f`. El comando `with` garantiza que el objeto `file` precedente, `f`, se cerrará automáticamente después de salir del bloque de código.

### Leyendo parcialmente un archivo

Dado un archivo `txt` abierto con la función `open()`, no es necesario leerlo al completo. Si solamente nos interesase leer una parte, podríamos indicárselo por parámetro al método `.read()`

En el siguiente chunk de código vamos a leer solamente los 7 primeros caracteres del archivo `f`

```python
f = open("/content/drive/MyDrive/python-basico/datasets/first_read.txt") 
print(f.read(7))
f.close()
```

```
"¡Qué i
```

### Leyendo un archivo línea a línea

El método `.readline()` hace que el archivo `f` sea leido línea a línea.

* Si solamente llamamos una vez al método `.readline()` leeremos únicamente la primera línea del fichero.
* Si llamamos dos veces al método, leeremos las dos primeras líneas del fichero.
* Y así sucesivamente.

En nuestro caso solo tenemos una línea, de modo que nos sirve una llamada al método `.readline()` para leer todo el fichero. Sin embargo, podemos probar con un archivo con más de una línea como el `first_read_multiline` que hemos creado para esta clase.

```python
with open("/content/drive/MyDrive/python-basico/datasets/first_read_multiline.txt") as f:
  print(f.readline())
  print(f.readline())
  print(f.readline())
```

```
"¡Qué ilusión!

Vamos a cargar por primera vez un archivo txt con Python

¡Y encima contiene múltiples líneas! =D"
```

### Escribiendo un archivo `txt`

Podemos crear y escribir un archivo `txt` desde este mismo notebook.

Para ello, volveremos a usar la función `open()`, pero esta vez con un parámetro adicional: `mode = "w"`. Este nuevo parámetro nos permitirá acceder al archivo en modo escritura, mientras que si no indicásemos nada, por defecto accederíamos en modo lectura.

Para escribir en el fichero, tendremos que usar el método `.write()` e indicarle el string que queremos plasmar en nuestro `txt`.

Además, para crear un nuevo archivo `txt`, a la hora de introducir el path (que será el mismo que el del archivo `first_read.txt`), como nombre del archivo indicaremos `first_write.txt`.

```python
f = open("/content/drive/MyDrive/python-basico/datasets/first_write.txt", mode = "w")
f.write("Este es el primer archivo txt que escribimos\ny lo estamos haciendo desde el notebook de Google Colab!")
f.close()
```

**¡Cuidado!** El archivo que creemos no debe existir. En caso de existir un archivo con el mismo nombre, lo estaríamos rescribiendo.

Comprobamos que se ha guardado el nuevo archivo `txt` llamado `first_write` en nuestra carpeta datasets.

Una vez comprobada la existencia de este archivo `txt`, podemos leerlo desde este notebook tal cuál hemos hecho en el apartado anterior

```python
# Con el método .read()
with open("/content/drive/MyDrive/python-basico/datasets/first_write.txt") as f:
  print(f.read())
```

```
Este es el primer archivo txt que escribimos
y lo estamos haciendo desde el notebook de Google Colab!
```

```python
# Con el método .readline()
with open("/content/drive/MyDrive/python-basico/datasets/first_write.txt") as f:
  print(f.readline())
  print(f.readline())
```

```
Este es el primer archivo txt que escribimos

y lo estamos haciendo desde el notebook de Google Colab!
```

Al haber más de una línea, también podemos leer todas ellas con un bucle:

```python
with open("/content/drive/MyDrive/python-basico/datasets/first_write.txt") as f:
  for line in f:
    print(line)
```

```
Este es el primer archivo txt que escribimos

y lo estamos haciendo desde el notebook de Google Colab!
```

### Creando un `txt` vacío

Si queremos crear un `txt` vacío, indicamos `mode = "x"`.

En este caso vamos a crear un `txt` vacío llamado `first_empty`

```python
f = open("/content/drive/MyDrive/python-basico/datasets/first_empty.txt", mode = "x")
f.close()
```

**¡Cuidado!** El archivo que creemos no debe existir. En caso de existir un archivo con el mismo nombre, nos saltaría error indicando que el archivo en cuestión ya existe.

### Sobrescribiendo un archivo `txt` existente

Al igual que podemos crear y escribir un archivo `txt` desde 0, podemos modificar un archivo `txt` ya existente.

En este caso, el parámetro `mode` debe ser igualado a `"a"`.

Vamos entonces a modificar el archivo `first_write` y vamos a añadirle al final la siguiente frase:

"\nY esta última línea se ha añadido posteriormente."

**Observación.** Añadimos el comando  al principio de la frase para que ésta se considere una nueva frase tras un salto de línea.

```python
f = open("/content/drive/MyDrive/python-basico/datasets/first_write.txt", mode = "a")
f.write("\nY esta última línea se ha añadido posteriormente.")
f.close()
```

**¡Cuidado!** Cada vez que ejecutéis la celda anterior se añadirá el string indicado. Por tanto, no la ejecutéis más de una vez u os encontraréis con la frase en cuestión repetida múltiples veces!

```python
with open("/content/drive/MyDrive/python-basico/datasets/first_write.txt") as f:
  for line in f:
    print(line)
```

```
Este es el primer archivo txt que escribimos

y lo estamos haciendo desde el notebook de Google Colab!

Y esta última línea se ha añadido posteriormente.
```

**¡Cuidado!** Si en vez de indicar `mode = "a"` indicáis `mode = "w"` eliminaréis el contenido del fichero y lo sobrescribiréis por completo por el string que indiquéis al método `.write()`

```python
f = open("/content/drive/MyDrive/python-basico/datasets/first_write.txt", mode = "w")
f.write("Ups! Todo lo anterior ha sido borrado!!!\n")
f.write("Hay que ir con cuidado cuando queremos editar un archivo txt...\n")
f.write("Hay que prestar mucha atención al método con el que accedemos al fichero!")
f.close()
```

```python
with open("/content/drive/MyDrive/python-basico/datasets/first_write.txt") as f:
  for line in f:
    print(line)
```

```
Ups! Todo lo anterior ha sido borrado!!!

Hay que ir con cuidado cuando queremos editar un archivo txt...

Hay que prestar mucha atención al método con el que accedemos al fichero!
```

### Eliminando archivos

En este caso vamos a tener que importar el módulo `os`

```python
import os
```

Para eliminar un archivo usaremos el método `.remove()` al que por parámetro indicaremos el path de dicho archivo.

```python
os.remove("/content/drive/MyDrive/python-basico/datasets/first_empty.txt")
```

Podemos comprobar en la carpeta datasets que efectivamente ha dejado de existir el archivo `first_empty`.

Para evitar errores, antes de proceder a la eliminación de un archivo, podemos comprobar su existencia con el método `.path.exists()`, al que por parámetro le indicamos el path del archivo en cuestión.

Para realizar este ejemplo, vamos a volver a crear el `txt` `first_empty`. Luego comprobaremos su existencia y, de existir, lo eliminaremos. De no existir, lo indicaremos por pantalla.

```python
path = "/content/drive/MyDrive/python-basico/datasets/first_empty.txt"
f = open(path, mode = "x")
f.close()
```

```python
if os.path.exists(path):
  os.remove(path)
else:
  print("El archivo que se quiere eliminar no existe")
```

Si volvemos a ejecutar la celda anterior, puesto que el archivo `first_empty` se habrá eliminado, obtendremos el mensaje `"El archivo que se quiere eliminar no existe"`

```python
if os.path.exists(path):
  os.remove(path)
else:
  print("El archivo que se quiere eliminar no existe")
```

```
El archivo que se quiere eliminar no existe
```

### Eliminando carpetas

Si se deseara eliminar toda una carpeta, esto sería posible con el método `.rmdir()`.

Para ver su funcionamiento, vamos a crear una carpeta dentro de la carpeta datasets. A esta nueva carpeta la llamaremos `carpeta_temporal` y estará vacía.

**Observación.** Este métodosolo nos permite eliminar carpetas vacías.

```python
path = "/content/drive/MyDrive/python-basico/datasets/carpeta_temporal"
os.rmdir(path)
```

Navegamos hasta la carpeta datasets de nuestro Google Drive y comprobamos que efectivamente, la carpeta vacía que acabábamos de crear, `carpeta_temporal`, ha sido eliminada.

## Archivos CSV

### Leyendo `csv` con `open()`

Además de usar la función `open()`, vamos a necesitar algunos métodos del módulo `csv`.

```python
import csv
```

Empezaremos mostrando como leer un `csv` haciendo uso del método `.reader()` del módulo `csv`.

En este caso vamos a trabajar con el archivo `csv_example.csv`. Si abrimos el archivo, veremos que todos los valores están separados por comas y cada observación se encuentra en una línea diferente.

Para leerlo, ejecutaremos el siguiente chunk de código:

```python
with open("/content/drive/MyDrive/python-basico/datasets/csv_example.csv", "r") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)
```

```
['id', 'Name', 'City', 'Age']
['1234', 'Arturo', 'Madrid', '22']
['2345', 'Beatriz', 'Barcelona', '25']
['3456', 'Carlos', 'Sevilla', '18']
['4567', 'Dolores', 'Cuenca', '34']
```

Con la función `open()` hemos accedido al archivo, al cuál hemos identificado por `f`. A continuación, hemos usado el método `.reader()` para leer el archivo `f`. Dicho método nos ha devuelto el iterable `reader`, del cuál hemos mostrado todas sus filas iterando con un bucle `for`.

### Cambiando el separador

Por defecto, los archivos `csv` tienen como delimitador la coma `,`. No obstante, algunos archivos `csv` usan otros delimitadores. Las alternativas más populares a la coma suelen ser `|` o .

Observemos el archivo `csv_delimiter_example.csv`, donde esta vez sus elementos están separados por tabuladores, .

El método `.reader()` nos permite configurar dicho separador con el parámetro `delimiter`.

```python
with open("/content/drive/MyDrive/python-basico/datasets/csv_delimiter_example.csv", "r") as f:
    reader = csv.reader(f, delimiter = "|")
    for row in reader:
        print(row)
```

```
['id', 'Name', 'City', 'Age']
['1234', 'Arturo', 'Madrid', '22']
['2345', 'Beatriz', 'Barcelona', '25']
['3456', 'Carlos', 'Sevilla', '18']
['4567', 'Dolores', 'Cuenca', '34']
```

### Eliminando espacios adicionales

A veces puede ocurrir que algunos `csv` tengan un espacio en blanco tras el delimitador, cosa que se ve reflejado al leer los datos.

Para eliminar estos espacios en blanco adicionales, el método `.reader()` trae el parámetro `skipinitialspace`. Si lo igualamos a `True`, los espacios adicionales desaparecerán.

Observemos que el archivo `csv_spaces_example.csv` tiene espacios en blanco adicionales tras el separador, que es la coma. Veamos la diferencia entre igualar el parámetro `skipinitialspace` a `True` o a `False`.

```python
# skipinitialspace = False (valor por defecto)
with open("/content/drive/MyDrive/python-basico/datasets/csv_spaces_example.csv", "r") as f:
    reader = csv.reader(f, skipinitialspace = False)
    for row in reader:
        print(row)
```

```
['id', ' Name', ' City', ' Age']
['1234', ' Arturo', ' Madrid', ' 22']
['2345', ' Beatriz', ' Barcelona', ' 25']
['3456', ' Carlos', ' Sevilla', ' 18']
['4567', ' Dolores', ' Cuenca', ' 34']
```

**Observación.** Salvo la primera entrada de cada fila, todas tienen un espacio inicial adicional.

```python
# skipinitialspace = True
with open("/content/drive/MyDrive/python-basico/datasets/csv_spaces_example.csv", "r") as f:
    reader = csv.reader(f, skipinitialspace = True)
    for row in reader:
        print(row)
```

```
['id', 'Name', 'City', 'Age']
['1234', 'Arturo', 'Madrid', '22']
['2345', 'Beatriz', 'Barcelona', '25']
['3456', 'Carlos', 'Sevilla', '18']
['4567', 'Dolores', 'Cuenca', '34']
```

### Comillas en las entradas

Algunos archivos `csv` puede que tengan entradas entre comillas. Si no indicamos nada, por defecto aparecerán las comillas en las entradas tras haber leído el fichero.

Si en cambio queremos deshacernos de ellas, disponemos del parámetro `quoting`, que admite diferentes valores:

* `csv.QUOTE_ALL`: indica al objeto `reader` que todos los valores en el archivo `csv` están entre comillas
* `csv.QUOTE_MINIMAL`: indica al objeto `reader` que los valores en el archivo `csv` que están entre comillas son entradas que contienen caracteres como el delimitador, comillas o cualquier caracter de terminación de línea
* `csv.QUOTE_NONNUMERIC`: indica al objeto `reader` que los valores en el archivo `csv` que están entre comillas son entradas que contienen entradas no-numéricas
* `csv.QUOTE_NONE`: indica al objeto `reader` que ninguno los valores en el archivo `csv` están entre comillas

Observemos el archivo `csv_quotation_example.csv`, donde las observaciones entre comillas son aquellas que no tienen valores numéricos. En este caso, nos convendría usar la opción `csv.QUOTE_NONNUMERIC`

```python
with open("/content/drive/MyDrive/python-basico/datasets/csv_quotation_example.csv", "r") as f:
    reader = csv.reader(f, quoting = csv.QUOTE_NONNUMERIC)
    for row in reader:
        print(row)
```

```
['id', 'Name', 'City', 'Age']
[1234.0, 'Arturo', 'Madrid', 22.0]
[2345.0, 'Beatriz', 'Barcelona', 25.0]
[3456.0, 'Carlos', 'Sevilla', 18.0]
[4567.0, 'Dolores', 'Cuenca', 34.0]
```

**Observación.** Las entradas numéricas han dejado de ser leídas como strings y han pasado a ser consideradas entradas de tipo `float`.

Si en cambio hubiésemos usado la opción `csv.QUOTATE_ALL`, no hubiésemos obtenido ningún error, pero las entradas numéricas habrían sido tratadas como `string`.

```python
with open("/content/drive/MyDrive/python-basico/datasets/csv_quotation_example.csv", "r") as f:
    reader = csv.reader(f, quoting = csv.QUOTE_ALL)
    for row in reader:
        print(row)
```

```
['id', 'Name', 'City', 'Age']
['1234', 'Arturo', 'Madrid', '22']
['2345', 'Beatriz', 'Barcelona', '25']
['3456', 'Carlos', 'Sevilla', '18']
['4567', 'Dolores', 'Cuenca', '34']
```

### Dialectos

Hasta ahora solamente hemos usado uno de los parámetros cada vez, pero podría darse el caso de que tuviésemos un csv con un delimitador distinto a la coma, con espacios adicionales y entradas entrecomilladas a causa de contener delimitadores o finales de línea.

Una opción sería indicar todos los parámetros a la función, pero existe una alternativa que nos será muy útil en caso de no estar tratando con un solo archivo `csv` sino con múltiples con formatos similares. Es el caso de los dialectos.

Los dialectos ayudan a agrupar patrones de formato específicos como el delimitador, las comillas, los espacios adicionales tras los delimitadores...

En caso de querer usar nuestro dialecto personalizado, `.reader()` nos ofrece el parámetros `dialect` al cual podemos pasarle dicho dialecto.

Consideremos el archivo `csv_dialect_example.csv`, el cual tiene el delimitador `|`, espacios adicionales y todos sus valores no numéricos entrecomillados.

En vez de indicar todos esos parámetros al método `.reader()`, vamos a crear nuestro dialecto, `my_dialect`, con el método `.register_dialect()` y se lo vamos a pasar al parámetro `dialect` de `.reader()`

```python
csv.register_dialect("my_dialect",
                     delimiter = "|",
                     skipinitialspace = True,
                     quoting = csv.QUOTE_NONNUMERIC)

with open("/content/drive/MyDrive/python-basico/datasets/csv_dialect_example.csv", "r") as f:
    reader = csv.reader(f, dialect = "my_dialect")
    for row in reader:
        print(row)
```

```
['id', 'Name', 'City', 'Age']
[1234.0, 'Arturo', 'Madrid', 22.0]
[2345.0, 'Beatriz', 'Barcelona', 25.0]
[3456.0, 'Carlos', 'Sevilla', 18.0]
[4567.0, 'Dolores', 'Cuenca', 34.0]
```

Al método `.register_dialect()` en primer lugar le hemos dado un nombre en formato `string` y luego hemos configurado los parámetros `delimiter`, `skipinitialspace` y `quoting`.

A continuación, al método `.reader()` le hemos pasado el nombre del dialecto, `my_dialect`, al parámetro `dialect` y se ha leído el archivo correctamente.

Una vez creado el dialecto personalizado, podemos usarlo tantas veces como queramos para abrir y leer archivos `csv` con el mismo formato, en este caso, que `csv_dialect_example.csv`.

### Diccionarios y `csv`

En este caso vamos a trabajar de nuevo con el archivo `csv_example.csv`.

Para leerlo, usaremos el método `.DictReader()` del módulo `csv`, lo que nos devolverá un objeto `OrderedDict`, que es iterable.

```python
with open("/content/drive/MyDrive/python-basico/datasets/csv_example.csv", "r") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row)
```

```
OrderedDict([('id', '1234'), ('Name', 'Arturo'), ('City', 'Madrid'), ('Age', '22')])
OrderedDict([('id', '2345'), ('Name', 'Beatriz'), ('City', 'Barcelona'), ('Age', '25')])
OrderedDict([('id', '3456'), ('Name', 'Carlos'), ('City', 'Sevilla'), ('Age', '18')])
OrderedDict([('id', '4567'), ('Name', 'Dolores'), ('City', 'Cuenca'), ('Age', '34')])
```

**Observación.** Podríamos usar la función `dict()` dentro del `print()` para mostrar los objetos `OrderedDict` como diccionarios.

```python
with open("/content/drive/MyDrive/python-basico/datasets/csv_example.csv", "r") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(dict(row))
```

```
{'id': '1234', 'Name': 'Arturo', 'City': 'Madrid', 'Age': '22'}
{'id': '2345', 'Name': 'Beatriz', 'City': 'Barcelona', 'Age': '25'}
{'id': '3456', 'Name': 'Carlos', 'City': 'Sevilla', 'Age': '18'}
{'id': '4567', 'Name': 'Dolores', 'City': 'Cuenca', 'Age': '34'}
```

**Observación.** Si se usa una versión de `Python` 3.8 o superior, podría ser que no fuera necesario usar la función `dict()` pues el resultado de `.DictReader()` ya sería un diccionario.

### Escribiendo `csv`

Para crear y escribir un `csv` usamos la función `open()` junto al método `csv.writer()`:

```python
data = [["id", "Name", "City", "Age"], 
        [1234, "Arturo", "Madrid", 22], 
        [2345, "Beatriz", "Barcelona", 25],
        [3456, "Carlos", "Sevilla", 18], 
        [4567, "Dolores", "Cuenca", 34]]

with open("/content/drive/MyDrive/python-basico/datasets/csv_write.csv", "w") as f:
  writer = csv.writer(f)
  for row in data:
    writer.writerow(row)
```

Si ahora vamos a la carpeta datasets, observaremos que ha aparecido un nuevo archivo llamado `csv_write.csv` el cual contiene como valores las entradas de la lista `data`, donde cada sublista corresponde a una fila del `csv` gracias al bucle `for` y al método `.writerow()`.

Podríamos haber obtenido exactamente el mismo resultado sin haber usado un bucle, lo que para ello tendríamos que haber hecho uso del método `.writerows()`.

```python
with open("/content/drive/MyDrive/python-basico/datasets/csv_write_writerows.csv", "w") as f:
  writer = csv.writer(f)
  writer.writerows(data)
```

Si ahora vamos a la carpeta datasets, observaremos que ha aparecido un nuevo archivo llamado `csv_write_writerows.csv` el cual contiene como valores las entradas de la lista `data`, donde cada sublista corresponde a una fila del `csv` gracias al método `.writerows()`.

### Diccionarios y csv

También podemos escribir un `csv` a partir de un diccionario. Para ello tendremos que usar el método `.DictWriter()`.

```python
data = [{"id": 1234, "Name": "Arturo", "City": "Madrid", "Age": 22},
        {"id": 2345, "Name": "Beatriz", "City": "Barcelona", "Age": 25},
        {"id": 3456, "Name": "Carlos", "City": "Sevilla", "Age": 18},
        {"id": 4567, "Name": "Dolores", "City": "Cuenca", "Age": 34}]

# La cabecera es la lista de las keys de cualquiera de las entradas de data
header = list(data[0].keys())
```

```python
with open("/content/drive/MyDrive/python-basico/datasets/csv_write_dict.csv", "w") as f:
  writer = csv.DictWriter(f, fieldnames = header)
  
  writer.writeheader()
  for d in data:
    writer.writerow(d)
```

En este caso, los datos están guardado en una lista de diccionarios llamada `data`. A continuación guardamos la cabecera en la variable `header` como una lista de los nombres de las variables.

Abrimos (y creamos) el archivo `csv_write_dict.csv` y creamos el objeto `writer` con el método `.DictWriter()` al cual le pasamos la cabecera `header` mediante el parámetro `fieldnames`.

Finalmente, escribimos en primer lugar la cabecera con el método `.writeheader()` y luego, con la ayuda de un bucle `for`, cada observación, correspondiente a cada uno de los diccionarios de la lista `data`, en una fila diferente con el método `.writerow()`.

Podríamos haber obtenido el mismo resultado sin usar ningún bucle, pero haciendo uso del método `.writerows()`

```python
with open("/content/drive/MyDrive/python-basico/datasets/csv_write_dict_writerows.csv", "w") as f:
  writer = csv.DictWriter(f, fieldnames = header)
  
  writer.writeheader()
  writer.writerows(data)
```

Observamos que efectivamente tanto el archivo `csv_write_dict.csv` como `csv_write_dict_writerows.csv` son idénticos.

## REPASO

#### Ejercicio 1

Pídele al usuario el nombre, el apellido, la edad y su color favorito. Guarda la información en un diccionario de claves name, surname, age y color. Crea y escribe un txt con 4 frases, una en cada línea. La primera debe indicar el nombre del usuario; la segunda, el apellido; la tercera, la edad; y la última, el color favorito del usuario.

```python
name = str(input("Introduzca su nombre: "))
surname = str(input("Introduzca su apellido: "))
age = int(input("Introduzca su edad: "))
color = str(input("Introduzca su color favorito: "))

info = {"name" : name,
        "surname" : surname,
        "age" : age,
        "color" : color}

with open("/content/drive/MyDrive/Python/txt/ejercicio_1.txt", "w") as f:
    for i in info:
        f.write("{}: {}\n".format(i, info[i]))
```

```
Introduzca su nombre: Abel
Introduzca su apellido: Garcia
Introduzca su edad: 29
Introduzca su color favorito: rojo
name: Abel
surname: Garcia
age: 29
color: rojo
```

#### Ejercicio 2

Lee el archivo txt creado en el ejercicio anterior para ver que se ha creado correctamente.

```python
with open("/content/drive/MyDrive/Python/txt/ejercicio_1.txt", "r") as f:
    print(f.read())
```

```
name: Abel
surname: Garcia
age: 29
color: rojo
```

#### Ejercicio 3

Crea un archivo txt vacío y llámalo ej3.txt.

```python
f = open("/content/drive/MyDrive/Python/txt/ej3.txt", "x")
f.close()
```

#### Ejercicio 4

Elimina el archivo creado en el ejercicio 3.

```python
import os
os.remove("/content/drive/MyDrive/Python/txt/ej3.txt")
```

#### Ejercicio 5

Crea un archivo txt vacío y llámalo ej5.txt. Sobreescribelo con las siguientes líneas: "x,y,Color,Shape \n" "1,1,#6fb7ff,< \n" "-1,1,#ffa66f,v \n" "-1,-1,#ffee6f,> \n" "1,-1,#db6fff,^ \n"

```python
f = open("/content/drive/MyDrive/Python/txt/ej5.txt", "x")
f.close()
f = open("/content/drive/MyDrive/Python/txt/ej5.txt", "a")
f.write("x,y,Color,Shape \n" "1,1,#6fb7ff,< \n" "-1,1,#ffa66f,v \n" "-1,-1,#ffee6f,> \n" "1,-1,#db6fff,^ \n")
f.close()
```

#### Ejercicio 6

Lee el archivo txt del ejercicio 5 como si fuera un archivo csv. Guarda las filas del objeto reader en una lista llamada df. Al final tendrás una lista con 5 listas de tamaño 4.

```python
import csv

with open("/content/drive/MyDrive/Python/txt/ej5.txt", "r") as f:
    reader = csv.reader(f)
    data = []
    for row in reader:
        data.append(row)
print(data)
```

```
[['x', 'y', 'Color', 'Shape '], ['1', '1', '#6fb7ff', '< '], ['-1', '1', '#ffa66f', 'v '], ['-1', '-1', '#ffee6f', '> '], ['1', '-1', '#db6fff', '^ ']]
```

#### Ejercicio 7

Utiliza el método .read\_csv() de pandas para leer el contenido del txt del ejercicio 5 y guardarlo en un dataframe llamado df.

```python
import pandas as pd

df = pd.DataFrame(data = data[1:], columns = data[0])
print(df)
```

```
    x   y    Color Shape 
0   1   1  #6fb7ff     < 
1  -1   1  #ffa66f     v 
2  -1  -1  #ffee6f     > 
3   1  -1  #db6fff     ^ 
```
