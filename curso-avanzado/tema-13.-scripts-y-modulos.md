---
description: Explicación del uso y funcionamiento de Scripts y Módulos en Python 3.
---

# Tema 13. Scripts y Módulos

## Scripts

**Script.** Es un archivo que contiene líneas de código. En nuestro caso, dichas líneas estarán escritas con el lenguaje de programación `Python`.

Un script de `Python` tiene la extensión `.py`.

Para ejecutar un script de `Python` necesitamos un intérprete como bien puede ser `Spyder`, `Jupyter`, `Google Colab` o `Python` (en Linux) pero para crearlo nos basta un editor de texto.

## Módulos

**Módulo.** Es una librería de código. Es un script que contiene un conjunto de funciones.

Un módulo de `Python`, al ser un script, tiene la extensión `.py`.

Para ejecutar un módulo de `Python` necesitaremos seguir los mismos pasos que cuando trabajábamos con scripts

### Creando un módulo

Hemos dicho que un módulo es un script que contiene funciones. Por tanto, lo primero que hacemos es crear un nuevo documento con el editor de texto al que llamaremos `my_first_module.py`.

En él declararemos las siguientes funciones:

```python
def sum(*numbers):
    """
    Función que suma los elementos que introduzcamos por parámetro
    """
    result = 0
    for n in numbers:
        result += n
  
    return result
  
def prod(*numbers):
    """
    Función que multiplica los elementos que introduzcamos por parámetro
    """
    result = 1
    for n in numbers:
        result *= n
  
    return result
    
def description():
    print("Este módulo tiene 3 funciones: ")
    print("\t- la que muestra la descripción del módulo")
    print("\t- la que suma los números que introduzcamos por parámetro")
    print("\t- la que multiplica los números que introduzcamos por parámetro")
```

### Importando un módulo

Para importar un módulo de Python dentro de un script deberemos tenerlo alojado en la misma carpeta que el script o en la ruta en la que el interprete los tenga almacenados (en mi caso es `/usr/lib/python3.9/`).

```python
import my_first_module

my_first_module.my_description()
total_sum = my_first_module.my_sum(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
total_prod = my_first_module.my_prod(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

print("\nEl resultado de la suma ha sido {} y el del producto, {}".format(total_sum, total_prod))
```

```
Este módulo tiene 3 funciones: 
	- la que muestra la descripción del módulo
	- la que suma los números que introduzcamos por parámetro
	- la que multiplica los números que introduzcamos por parámetro

El resultado de la suma ha sido 55 y el del producto, 3628800
```

### **Renombrando un módulo**

Como recordaréis, cuando vimos por primera vez la palabra reservada `import`, si lo combinábamos con la palabra reservada `as`, conseguíamos renombrar el objeto que importábamos.

En este caso, `my_first_module` es un nombre muy largo. Podemos renombrarlo a `mfm` con la siguiente línea de código, de modo que a partir de ahora cuando queramos invocar alguna función de nuestro módulo, en vez de preceder a cada función por `my_first_module`, lo haremos por `mfm`

```python
import my_first_module as mfm

mfm.my_description()
total_sum = mfm.my_sum(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
total_prod = mfm.my_prod(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

print("\nEl resultado de la suma ha sido {} y el del producto, {}".format(total_sum, total_prod))
```

```
Este módulo tiene 3 funciones: 
	- la que muestra la descripción del módulo
	- la que suma los números que introduzcamos por parámetro
	- la que multiplica los números que introduzcamos por parámetro

El resultado de la suma ha sido 55 y el del producto, 3628800
```

### **Variables en un módulo**

Hasta ahora solo hemos visto como acceder a funciones de un módulo, pero los módulos también pueden contener variables. Añadamos a nuestro módulo las dos siguientes líneas de código:

```python
sum1to10 = my_sum(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
prod1to10 = my_prod(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
```

```python
import my_first_module as mfm

print("\nEl resultado de la suma de los 10 primeros números enteros es {} y su producto, {}".
      format(mfm.sum1to10, mfm.prod1to10))
```

```
El resultado de la suma de los 10 primeros números enteros es 55 y su producto, 3628800
```

Si recordáis, cuando vimos la función `import`, observamos que no era necesario importar todo el módulo, sino que podíamos importar funciones o incluso variables concretas del módulo con la sintaxis siguiente, y así evitar tener que indicar el nombre del módulo previo al nombre de la función o la variable en cuestión

```python
from my_first_module import sum1to10, prod1to10
```

De modo que el `print` anterior queda modificado del siguiente modo

```python
print("\nEl resultado de la suma de los 10 primeros números enteros es {} y su producto, {}".
      format(sum1to10, prod1to10))
```

```
El resultado de la suma de los 10 primeros números enteros es 55 y su producto, 3628800
```

Finalmente, así como podemos modificar el nombre de los módulos, también podemos modificar el nombre tanto de las funciones como de las variables del módulo:

```python
from my_first_module import my_description as mfm_desc
mfm_desc()
```

```
Este módulo tiene 3 funciones: 
	- la que muestra la descripción del módulo
	- la que suma los números que introduzcamos por parámetro
	- la que multiplica los números que introduzcamos por parámetro
```

## Módulos de `Python`

`Python` es un software libre que de por sí ya tiene muchos módulos creados que nos son de mucha utilidad:

* `pwn` para trabajar en la escritura de exploits.
* `pycryptodome` para trabajar con criptografía a bajo nivel.
* `os` para interacción entre el interprete y el sistema.
* `socket` para trabajar con redes.

¡Y muchos más!

En secciones futuras veremos en detalle algunos de estos módulos para saber aprovecharlos al máximo.

### La función `dir()`

La función `dir()` aplicada a un script nos devuelve los métodos y las variables que contiene.

Si la aplicamos a nuestro módulo, al que recordad habíamos renombrado como `mfm`, lo que obtenemos es la siguiente lista de métodos y variables.

```python
dir(mfm)
```

```
['__builtins__',
 '__cached__',
 '__doc__',
 '__file__',
 '__loader__',
 '__name__',
 '__package__',
 '__spec__',
 'my_description',
 'my_prod',
 'my_sum',
 'prod1to10',
 'sum1to10']
```

**Observación.** Como resultado no solamente hemos obtenido los métodos y las variables creados por nosotros, sino que se muestran algunos atributos extras como `.__file__`, que guarda el path donde está guardado el módulo, que son los que se han creado por defecto y a los cuales también podemos acceder:

```python
mfm.__file__
```

```
'/content/drive/My Drive/python-basico/scripts/my_first_module.py'
```

#### EJERCICIO 1:&#x20;

Vamos a crear un script llamado `geometry.py` y en él vamos a crear la clase `RegularPolygon`.

* El constructor tomará 2 parámetros:
  * `base`: longitud de la base
  * `n`: número de lados
* El método `.__str__()` mostrará "Soy un polígono de {} lados de longitud {}".
* El método de instancia `.apothem()` calculará el apotema. Lo convertiremos en una propiedad.
* El método de instancia `.area()` calculará el área del polígono. Lo convertiremos en una propiedad.
* El método de instancia `.perimeter()` calculará el perímetro del polígono. Lo convertiremos en una propiedad.

```python
#Contenido del script geometry.py
#NO EJECUTAR, UTILIZAR EL SCRIPT
class RegularPolygon():
    import math

    def __init__(self, base, n):
        self.base = base
        self.n = n

    def __str__(self):
        return ("Soy un polígono de {} lados de longitud {}".format(self.n, self.base))

    @property
    def apothem(self):
        return (self.base / (2 * tan((360 / self.n)/ 2)))

    @property
    def perimeter(self):
        return self.base * self.n
    
    @property
    def area(self):
        return ((self.perimeter * self.apothem) / 2)
```

#### EJERCICIO 2:&#x20;

Vamos a crear las clases `Triangle`, `Square` y `Pentagon`, que hereden de la clase `RegularPolygon`. Solamente cambiaremos el constructor.

```python
class Triangle(RegularPolygon):
    def __init__(self, base):
        super().__init__(base, 3)
    
    
class Square(RegularPolygon):
    def __init__(self, base):
        super().__init__(base, 4)
    
    
class Pentagon(RegularPolygon):
    def __init__(self, base):
        super().__init__(base, 5)
```

#### EJERCICIO 3:&#x20;

Vamos a crear las clases `Tetrahedron` y `Cube`. La primera hereda de la clase `Triangle` y la segunda, de la clase `Square`. A ambas clases les vamos a añadir el método `.volume()`, que convertiremos en ambos casos a propiedad. También tendremos que modificar ligeramente la propiedad `.area` y el método `.__str__()`.

```python
class Tetrahedron(Triangle):
    def __str__(self):
        return "Soy un tetraedro con lados de longitud {}".format(self.base)
        
    @property    
    def area(self):
        return 4 * super().area
        
    @property
    def volume(self):
        return math.sqrt(2) / 12 * self.base
        

class Cube(Square):
    def __str__(self):
        return "Soy un cubo con lados de longitud {}".format(self.base)
        
    @property
    def area(self):
        return 6 * super().area
        
    @property
    def volume(self): 
        return super().area * self.base
```

#### EJERCICIO 4:&#x20;

Vamos a crear la clase `Circle` que por parámetro tome el radio `r` y tenga 4 métodos: el constructor y las propiedad `.diameter()`, `.perimeter()` y `.area()`.

Finalmente vamos a crear la clase `Cylinder` que herede de `Circle` y `Square`. Vamos a modificar la propiedad `.area()` y crear la propiedad `.volume()`.

```python
#ME DA PEREZA... YA LO HARÉ.
```

## REPASO

**EJERCICIO 1**:Crea un script llamado vectors.py. Ábrelo y crea una clase llamada Vector2D. El constructor debe guardar las coordenadas x e y del vector.

```python
from math import sqrt
class vector2D():
    def __init__(self, x, y):
        self.x = x
        self.y = y
```

**EJERCICIO 2**: Crea los siguientes métodos:

• La propiedad .module que devuelva el módulo del vector. Recuerda que el módulo de un vector 2D se calcula como p x2 + y2. Para calcular raíces cuadradas, dispones del método math.sqrt().

• El método de instancia .scalar\_prod() que multiplique el vector por el número real dado por parámetro, que por defecto vale 1. Configura el método .**str** para que se nos muestre por pantalla el vector de la forma (x, y).

```python
    def __str__(self):
        return "({}, {})".format(x, y)
    
    @property
    def module(self):
        return sqrt(x**2 + y **2)
    
    def scalar_prod(scale = 1):
        #Sobreescribe el vector inicial
        self.x = x * scale
        self.y = y * scale
```

**EJERCICIO 3**: Crea los siguientes métodos:

• El método de clase .sum() que dados dos vectores los sume y devuelva un objeto de la clase Vector2D.

• El método de clase .subtract() que dadoas dos vectores los reste y devuelva un objeto de la clase Vector2D.

```python
    @classmethod
    def sum(vector1, vector2):
        return cls(vector1.x + vector2.x, vector1.y + vector2.y)
    
    @classmethod
    def substract(vector1, vector2):
        return cls(vector1.x - vector2.x, vector1.y - vector2.y)
```

**EJERCICIO 4**: Crea los siguientes métodos:

• El método estático .dot\_product() que dados dos vectores calcule su producto escalar. Recuerda que el producto escalar de 2 vectores 2D u y v se calcula como u · v = uxvx + uyvy

• El método de clase .distance() que dados dos vectores calcule la distancia entre ellos. Recuerda que la distancia entre 2 vectores 2D u y v se calcula como p(ux − vx)2 + (uy − vy)2

```python
    @staticmethod
    def dot_product(vector1, vector2):
        return vector1.x * vector2.x + vector1.y * vector2.y
    
    @classmethod
    def distance(cls, vector1, vector2):
        return sqrt((vector1.x - vector2.x) ** 2 + (vector1.y - vector2.y) ** 2 )
```

**EJERCICIO 5**: Ahora crea la clase Vector3D que herede de la clase Vector2D. Empieza con el constructor para que además de las coordenadas x e y, también tome la coordenada z. Recuerda que puedes utilizar el método .super() para acceder a métodos de la clase padre.

```python
class Vector3D(Vector2D):
    
    def __init__():
        super().__init__(x, y)
        self.z = z
```

**EJERCICIO 6**: Crea en la clase Vector3D los métodos siguientes:

• el método .**str**() para que muestre el vector por pantalla de la forma (x, y, z).

• la propiedad .module. Al tener vectores 3D, el módulo se calcula como p x 2 + y 2 + z 2

• el método de instancia .scalar\_prod()

• los métodos de clase .sum() y .subtract() para que devuelvan objetos de la clase Vector3D.

• el método estático .dot\_product(), pues ahora el producto escalar se calcula como u · v = uxvx + uyvy + uzvz

• el método de clase .distance(), pues ahora la distancia se calcula como q (ux − vx) 2 + (uy − vy) 2 + (uz − vz) 2

Recuerda que dispones del método .super() para evitar repeticiones innecesarias de código.

```python
    def __str__():
        return super().__str__()[: -1] + ", {})".format(self.z)
    
    @property
    def module(self):
        return sqrt(self.x ** 2 + self.y ** 2 + self.z ** 2)
        
    def scalar_prod(self, scale):
        super().scalar_prod()
        self.z = self.z * scale
    
    @classmethod
    def sum(cls):
        return cls(vector1.x + vector2.x, vector1.y + vector2.y, vector1.z + vector1.z)
        
    @classmethod
    def substract(cls):
        return cls(vector1.x - vector2.x, vector1.y - vector2.y, vector1.z - vector1.z)
    
    @classmethod
    def distance(cls, vector1, vector2):
        sqrt((vector1.x - vector2.x) ** 2 + (vector1.y - vector2.y) ** 2 + (vector1.z - vector2.z) ** 2)
    
    @staticmethod
    def dot_product(vector1, vector2):
        return vector1.x * vector2.x + vector1.y * vector2.y + vector1.z * vector2.z
```

**EJERCICIO 7**: Crea en la clase Vector3D los métodos siguientes:

• el método de clase .zero() que devuelva un objeto Vector3D con todas sus componentes 0.

• el método de clase .horizontal() que devuelva un objeto Vector3D con todas sus componentes 0 salvo la primera que valdrá 1.

• el método de clase .vertical() que devuelva un objeto Vector3D con todas sus componentes 0 salvo la segunda que valdrá 1.

• el método de clase .forward() que devuelva un objeto Vector3D con todas sus componentes 0 salvo la tercera y última que valdrá 1.

```python
    @classmethod
    def zero(cls):
        return cls(0, 0, 0)
    
    @classmethod
    def horizontal(cls):
        return cls(1, 0, 0)
    
    @classmethod
    def vertical(cls):
        return cls(0, 1, 0)
    
    @classmethod
    def forward(cls):
        return cls(0, 0, 1)
    
```

**EJERCICIO 8**: Crea en la clase Vector2D el método de instancia .extend\_to\_3D() que devuelva un objeto de la clase Vector3D siendo la componente z el valor indicado por parámetro, que por defecto valdrá 0.

```python
def extend_to_3D(self, z):
        return Vector3D(self.x, self.y, z)
```

**EJERCICIO** **9**: En un notebook de Google Colab, importa el script, crea dos objetos de la clase Vector2D y prueba que todos los métodos de la clase Vector2D funcionan correctamente.

```python
#En mi caso tengo permitido el acceso de Colab a Drive permanente por lo que no tengo que montar el disco virtual

from google.colab import drive
drive.mount('/content/drive')
%cd /content/drive/MyDrive/Python/scripts/

```

```
Drive already mounted at /content/drive; to attempt to forcibly remount, call drive.mount("/content/drive", force_remount=True).
/content/drive/MyDrive/Python/scripts
```

```python
from vectors import *
```

```python
vector2D_1 = Vector2D(1, 1)
vector2D_2 = Vector2D(5, -5)
print(vector2D_1, vector2D_2)
```

```
(1, 1) (5, -5)
```

```python
print(vector2D_1.module)
print(vector2D_2.module)
```

```
1.4142135623730951
7.0710678118654755
```

```python
print(vector2D_1.scalar_prod(3))
print(vector2D_2.scalar_prod(-2))
```

```
(3, 3)
(-10, 10)
```

```python
vector3D_1 = vector2D_1.extend_to_3D(5)
print(vector3D_1)
```

```
(3, 3, 5)
```

```python
print(Vector2D.sum(vector2D_1, vector2D_2))
print(Vector2D.substract(vector2D_1, vector2D_2))
print(Vector2D.distance(vector2D_1, vector2D_2))
print(Vector2D.dot_product(vector2D_1, vector2D_2))
```

```
(6, -4)
(-4, 6)
7.211102550927978
0
```

**EJERCICIO 10**: Ahora crea dos objetos de la clase Vector3D y prueba que todos los métodos de la clase Vector3D funcionan correctamente.

```python
vector3D_1 = Vector3D(1, 2, 3)
vector3D_2 = Vector3D(-3, 10, -2)
print(vector3D_1, vector3D_2)
```

```
(1, 2, 3) (-3, 10, -2)
```

```python
print(vector3D_1.module)
print(vector3D_2.module)
```

```
3.7416573867739413
10.63014581273465
```

```python
print(vector3D_1.scalar_prod(3))
print(vector3D_2.scalar_prod(-2))
```

```
None
None
```

```python
print(Vector2D.sum(vector3D_1, vector3D_2))
print(Vector2D.substract(vector3D_1, vector3D_2))
print(Vector2D.distance(vector3D_1, vector3D_2))
print(Vector2D.dot_product(vector3D_1, vector3D_2))
```

```
(-2, 12)
(4, -8)
8.94427190999916
17
```
