---
description: >-
  Explicación de la aplicación de la programación orientada a objetos en Python
  3.
---

# Tema 12. Programación orientada a objetos

## Clases

![](<../.gitbook/assets/image (1).png>)

**Clase.** Una clase es una plantilla para crear objetos. Las clases contienen la definición de los objetos con los que trabajamos y definen sus propiedades (**atributos**) además de especificar las modificaciones que se pueden hacer a esos objetos (**métodos**).

Cada vez que construimos un objeto de una clase, estamos creando una instancia de dicha clase.

**Objeto.** Es la instancia de una clase y consta de:

* **Estado.** Representado por los atributos del objeto, que reflejan sus propiedades
* **Comportamiento.** Representado por los métodos del objeto, que reflejan su resupuesta a otros objetos
* **Identidad.** Cada objeto tiene un nombre único que le permite interactuar con otros objetos

Las clases son fundamentales para lenguajes de programación orientada a objetos, como por ejemplo `Python`.

En definitiva, una clase es una plantilla y una instancia es una copia de la clase con valores determinados: un objeto.

### Mi primera clase en `Python`

Vamos a crear nuestra primera clase: la clase `Book`. Las clases se crean con la palabra reservada `class`.

De momento nuestra clase constará únicamente de una **variable estática** llamada `is_electronic`, que valdrá `False`, indicando así que todos los objetos de esta clase serán libros no electrónicos.

**Variable estática.** Son las variables que pertenecen a la clase.

```python
class Book():
  is_electronic = False
```

Ya hemos creado nuestra plantilla del objeto `Book`, que únicamente contiene si el libro en cuestión es electrónico o no.

Si ahora nosotros queremos crear un objeto de la clase `Book`, tendremos que instanciarlo del siguiente modo:

```python
book1 = Book()
```

Hemos construido un objeto de la clase `Book` con nuestra plantilla, por lo tanto `book1` se trata de un libro no electrónico.

Tal cual hacíamos anteriormente, si queremos saber a qué clase pertenece el objeto `book1`, le aplicamos la función `type()`

```python
type(book1)

#RESPUESTA
__main__.Book
```

Si ahora queremos acceder a la única variable de la clase, `is_electronic`, entonces introducimos

```python
Book.is_electronic
```

```
False
```

y comprobamos así que efectivamente, el valor de la variable estática de `Book` es `False`.

Vamos a mejorar nuestra clase `Book` añadiendo docstrings

```python
class Book():
  """
  Clase para trabajar con libros
  """

  is_electronic = False
```

Ahora podemos acceder a ese docstring con el método `.__doc__`

```python
print(Book.__doc__)

#RESPUESTA
  Clase para trabajar con libros
```

### El método constructor

Sigamos mejorando nuestra clase, esta vez modificando el método `.__init__()` que es llamado cuando inicializamos un objeto de la clase. Se trata del método constructor. Por parámetro puede recibir valores para los atributos de cada objeto:

**Atributo:** Son las variables que definen a los objetos de una clase. Son sus características.

```python
class Book():
  """
  Clase para trabajar con libros
  """

  def __init__(self, title, author, electronic):
    self.title = title
    self.author = author
    self.is_electronic = electronic
```

**Observación.** Hablaremos del parámetro `self` más adelante, cuando hablemos de métodos de instancia.

Ahora, si queremos crear un objeto de la clase `Book`, por como hemos construido el método `.__init__` tendremos que indicar el título y autor del libro

```python
book2 = Book("El señor de los Anillos", "J.R.R. Tolkien", False)
```

```python
book2.title

#RESPUESTA
'El señor de los Anillos'
```

```python
book2.author

#RESPUESTA
'J.R.R. Tolkien'
```

```python
book2.is_electronic

#RESPUESTA
False
```

Para acceder a todos los atributos de un objeto y a los valores que tiene asignados, podemos usar el método `.__dict__`

```python
book2.__dict__

#RESPUESTA
{'author': 'J.R.R. Tolkien',
 'is_electronic': False,
  'title': 'El señor de los Anillos'}
```

Si queremos evitar tener que introducir alguno de esos parámetros cada vez que inicialicemos un objeto de la clase `Book`, recordad que podemos poner valores por defecto a dichos parámetros:

```python
class Book():
  """
  Clase para trabajar con libros
  """

  def __init__(self, title, author = "", electronic = False):
    self.title = title
    self.author = author
    self.is_electronic = electronic
```

```python
book3 = Book(title = "Las mil y una noches")
```

```python
book3.title

#RESPUESTA
'Las mil y una noches'
```

```python
book3.is_electronic

#RESPUESTA
False
```

Con lo cual, el único argumento obligatorio a introducir es el título. El resto son opcionales pues tienen valores por defecto.

#### EJERCICIO 1:

Vamos a crear la clase RationalNumber. Vamos a configurar el constructor de modo que haya un atributo numerator y otro denominator, este último con 1 como valor por defecto. Ambos atributos deben ser números enteros.

```python
class RationalNumber():
    """
    Clase para trabajar con números racionales
    """
    def __init__(self, n, d = 1):
        if type(n) is int and type(d) is int:
            self.numerator = n
            self.denominator = d
        else:
            print("Numerador y Denominador deben ser números enteros.")
```

### El método destructor

Así como existe un método constructor, existe un método destructor cuyo cometido consiste en eliminar instancias de una clase. Es decir, elimina un objeto.

El método destructor es el método `.__del__()`

```python
class Book():
  """
  Clase para trabajar con libros
  """

  def __init__(self, title, author = "", electronic = False):
    self.title = title
    self.author = author
    self.is_electronic = electronic

  def __del__(self):
    print("Acabas de llamar al método destructor. El objeto acaba de ser eliminado")
```

Para eliminar un objeto, utilizamos la palabra reservada `del`

```python
book = Book("Lazarillo de Tormes")
book.title

#RESPUESTA
'Lazarillo de Tormes'
```

```python
del book

#RESPUESTA
Acabas de llamar al método destructor. El objeto acaba de ser eliminado
```

Si intentásemos acceder al objeto `book`, obtendríamos error pues ha dejado de ser una instancia de la clase `Book` porque lo hemos eliminado.

## Métodos de una clase

Existen 3 tipos de métodos:

* Métodos de instancia
* Métodos estáticos
* Métodos de clase

### Métodos de instancia

Siempre toman el parámetro `self` como primer parámetro.

El parámetro `self` representa la instancia del método. Lo que hace `Python` es pasar el propio objeto como argumento del método.

```python
class Rectangle():

  def __init__(self, base = 1, height = 1, color = "blue"):
    self.base = base
    self.height = height
    self.color = color
  
  def perimeter(self):
    return 2 * self.base + 2 * self.height

  def area(self):
    return self.base * self.height
```

```python
rect1 = Rectangle(5, 2, "red")
print("El perímetro es {}".format(rect1.perimeter()))
print("El área es {}".format(rect1.area()))

#RESPUESTA
El perímetro es 14
El área es 10
```

Si ahora modificamos la base, entonces tanto el perímetro como el área también cambiarán su valor:

```python
rect1.base = 3
print("Habiendo cambiado el valor de la base a 3, el perímetro es {}".format(rect1.perimeter()))
print("Habiendo cambiado el valor de la base a 3, el área es {}".format(rect1.area()))

#RESPUESTA
Habiendo cambiado el valor de la base a 3, el perímetro es 10
Habiendo cambiado el valor de la base a 3, el área es 6
```

Los métodos de instancia pueden tener más inputs aparte del `self`. Añadamos un método que nos devuelva verdadero si la base es mayor a un valor mínimo al que llamaremos `min` y que por defecto haremos que valga 5:

```python
class Rectangle():

  def __init__(self, base = 1, height = 1, color = "blue"):
    self.base = base
    self.height = height
    self.color = color
  
  def perimeter(self):
    return 2 * self.base + 2 * self.height

  def area(self):
    return self.base * self.height

  def is_base_big(self, min = 5):
    if self.base > min:
      return True
    return False
```

```python
rect1 = Rectangle(3, 2, "red") # Como hemos modificado la clase, hay que volver a construir el objeto rect1
rect1.is_base_big()

#RESPUESTA
False
```

```python
rect2 = Rectangle(12, 7)
rect2.is_base_big(10) # Hacemos que el valor mínimo aumente a 10

#RESPUESTA
True
```

El método `.__str__` es un método de instancia. Es el método que debe ser llamado cuando el objeto se representa como un `string`. Es decir, lo que este método devuelve es lo que se muestra cuando hacemos un `print` del objeto en cuestión.

```python
class Rectangle():

  def __init__(self, base = 1, height = 1, color = "blue"):
    self.base = base
    self.height = height
    self.color = color
  
  def perimeter(self):
    return 2 * self.base + 2 * self.height

  def area(self):
    return self.base * self.height

  def is_base_big(self, min = 5):
    if self.base > min:
      return True
    return False

  def __str__(self):
    return ("Base: {}\nAltura: {}".format(self.base, self.height))
```

De modo que si ahora creamos un objeto de la clase `Rectangle` y pasamos por parámetro dicho objeto a la función `print()`, obtenemos lo siguiente

```python
rect3 = Rectangle(15, 9, "pink")
print(rect3)

#RESPUESTA
Base: 15
Altura: 9
```

#### EJERCICIO 2:&#x20;

Vamos a configurar el `método .__str__()` para que nos muestre el número racional de la forma numerador / denominador.

EXTRA: Busca cómo usar LaTeX en strings de Python y construye el `método .mathMode()` que muestre el número racional en formato $\frac{numerador}{denominador}$

```python
class RationalNumber():
    """
    Clase para trabajar con números racionales
    """
    def __init__(self, n, d = 1):
        if type(n) is int and type(d) is int:
            self.numerator = n
            self.denominator = d
        else:
            print("Numerador y Denominador deben ser números enteros.")


    def __str__(self):
        return ("{} / {}".format(self.numerator, self.denominator))


    def mathMode(self):
        from IPython.display import display, Latex
        display(Latex(f"${self.numerator}\\over{self.denominator}$"))
```

```python
q = RationalNumber(5, 5)
print(q, "\n")
q.mathMode()

#RESPUESTA
5 / 5 
```

#### EJERCICIO 3:

1. Implementa el método de instancia **.quotient()** que devuelva el cociente
2. Implementa el método de instancia **.isInfinite()** que devuelva si el denominador es 0 o no
3. Implementa el método de instancia **.simplify()** que simplifique la fracción a la fracción irreducible

```python
def bigger(a, b): 
  """
  Devuelve el mayor número de 2 números reales dados.
  Args:
    a: Número real
    b: Número real
  Returns:
    Número real
  """
  if a >= b: 
    return a
  return b

def lower(a, b): 
  """
  Devuelve el menor número de 2 números reales dados.
  Args:
    a: Número real
    b: Número real
  Returns:
    Número real
  """
  if a <= b: 
    return a
  return b

def mcd(a, b): 
  """
  Devuelve el MCD de dos números enteros.
  Args:
    a: Número entero
    b: Número entero
  Returns:
    max: Número entero
  """
  r=0
  max = bigger(a, b) 
  min = lower(a, b)
  while(min > 0):
    r = min
    min = max % min 
    max = r
  return max

class RationalNumber():
    """
    Clase para trabajar con números racionales
    """
    def __init__(self, n, d = 1):
        if type(n) is int and type(d) is int:
            self.numerator = n
            self.denominator = d
        else:
            print("Numerador y Denominador deben ser números enteros.")


    def __str__(self):
        return ("{} / {}".format(self.numerator, self.denominator))


    def mathMode(self):
        from IPython.display import display, Latex
        display(Latex(f"${self.numerator}\\over{self.denominator}$"))

    def quotient(self):
        return self.numerator / self.denominator

    def isInfinite(self):
        if self.denominator == 0:
            return True
        else:
            return False
    
    def simplify(self):
        div = mcd(self.numerator, self.denominator)
        self.numerator = int(self.numerator / div)
        self.denominator = int(self.denominator / div)
```

### Métodos estáticos

A diferencia de los métodos de instancia, los métodos estáticos no pasan como parámetro el argumento posicional `self`.

Los métodos estáticos se definen usando el decorador `@staticmethod`, que se añade antes de definir el método estático respectivo.

Los decoradores nos permiten alterar el comportamiento de las funciones o clases. Son utilizados para guardar utilidades relacionadas con la clase.

Vamos a crear un método que nos diga si dos rectángulos son iguales o no.

```python
class Rectangle():

  def __init__(self, base = 1, height = 1, color = "blue"):
    self.base = base
    self.height = height
    self.color = color
  
  def perimeter(self):
    return 2 * self.base + 2 * self.height

  def area(self):
    return self.base * self.height

  def is_base_big(self, min = 5):
    if self.base > 5:
      return True
    return False

  def __str__(self):
    return ("Base: {}\nAltura: {}".format(self.base, self.height))

  @staticmethod
  def are_equal_size(rect1, rect2):
    if rect1.base == rect2.base and rect1.height == rect2.height:
      return True
    return False
```

```python
rect1 = Rectangle(7, 5, "green")
rect2 = Rectangle(3 + 4, 7 - 2, "blue")
print(rect1, "\n")
print(rect2, "\n")
print(Rectangle.are_equal_size(rect1, rect2))
```

```
#RESPUESTA
Base: 7
Altura: 5 

Base: 7
Altura: 5 

True
```

#### EJERCICIO 4:&#x20;

Vamos a implementar los siguientes métodos estáticos:

* `.sum()` donde p1/q1+p2/q2=(p1q2+p2q1)/q1⋅q2
* `.substract()` donde p1/q1−p2/q2=(p1q2−p2q1)/q1⋅q2
* `.product()` donde p1/q1⋅p2/q2=(p1⋅p2)/(q1⋅q2)
* `.division()` donde p1/q1÷p2/q2=(p1⋅q2)/(p2⋅q1)

```python
def bigger(a, b): 
  """
  Devuelve el mayor número de 2 números reales dados.
  Args:
    a: Número real
    b: Número real
  Returns:
    Número real
  """
  if a >= b: 
    return a
  return b

def lower(a, b): 
  """
  Devuelve el menor número de 2 números reales dados.
  Args:
    a: Número real
    b: Número real
  Returns:
    Número real
  """
  if a <= b: 
    return a
  return b

def mcd(a, b): 
  """
  Devuelve el MCD de dos números enteros.
  Args:
    a: Número entero
    b: Número entero
  Returns:
    max: Número entero
  """
  r=0
  max = bigger(a, b) 
  min = lower(a, b)
  while(min > 0):
    r = min
    min = max % min 
    max = r
  return max

def helper(n, d):
    print("{} / {} = {}".format(n, d, n / d))

class RationalNumber():
    """
    Clase para trabajar con números racionales
    """
    def __init__(self, n, d = 1):
        if type(n) is int and type(d) is int:
            self.numerator = n
            self.denominator = d
        else:
            print("Numerador y Denominador deben ser números enteros.")


    def __str__(self):
        return ("{} / {}".format(self.numerator, self.denominator))


    def mathMode(self):
        from IPython.display import display, Latex
        display(Latex(f"${self.numerator}\\over{self.denominator}$"))


    def quotient(self):
        return self.numerator / self.denominator


    def isInfinite(self):
        if self.denominator == 0:
            return True
        else:
            return False
    

    def simplify(self):
        div = mcd(self.numerator, self.denominator)
        self.numerator = int(self.numerator / div)
        self.denominator = int(self.denominator / div)


    @staticmethod
    def sum(div1, div2):
        num = (div1.numerator * div2.denominator + div2.numerator * div1.denominator)
        den = (div1.denominator * div2.denominator)
        helper(num, den)
    

    @staticmethod
    def substract(div1, div2):
        num = (div1.numerator * div2.denominator - div2.numerator * div1.denominator)
        den = (div1.denominator * div2.denominator)
        helper(num, den)
    

    @staticmethod
    def product(div1, div2):
        num = div1.numerator * div2.numerator
        den = div1.denominator * div2.denominator
        helper(num,den)


    @staticmethod
    def division(div1, div2):
        num = div1.numerator * div2.denominator
        den = div1.denominator * div2.nominator
        helper(num,den)
```

### Métodos de clase

La característica de estos métodos es que la clase entera es pasada como primer argumento, `cls`. Para los métodos de clase vuelve a usarse un decorador, `@classmethod`.

Vamos a crear un método que genere un rectángulo aleatoriamente. Para ello necesitamos importar la librería `random`

```python
import random
```

```python
class Rectangle():

  def __init__(self, base = 1, height = 1, color = "blue"):
    self.base = base
    self.height = height
    self.color = color
  
  def perimeter(self):
    return 2 * self.base + 2 * self.height

  def area(self):
    return self.base * self.height

  def is_base_big(self, min = 5):
    if self.base > min:
      return True
    return False

  def __str__(self):
    return ("Base: {}\nAltura: {}".format(self.base, self.height))

  @staticmethod  
  def are_equal_size(rect1, rect2):
    if rect1.base == rect2.base and rect1.height == rect2.height:
      return True
    return False

  @classmethod
  def random_rectangle(cls):
    base = random.randrange(1, 10)
    height = random.randrange(1, 10)
    return cls(base, height)
```

```python
rect3 = Rectangle().random_rectangle()
print(rect3)

#RESPUESTA
Base: 6
Altura: 1
```

#### EJERCICIO 5:&#x20;

Vamos a configurar los siguientes métodos de clase:

* `.random()` que se encarga de crear un objeto aleatorio de la clase `RationalNumber`.
* `.zero()` que se encarga de crear el objeto de la clase `RationalNumber` que tiene por numerador 0 y denominador 1.
* `.one()` que se encarga de crear el objeto de la clase `RationalNumber` que tiene por numerador 1 y denominador 1.
* `.fromRealNumber()` que dado un número real se encarga de buscar su expresión en racional. Por ejemplo, dado 5.4, tendremos que crear el objeto `RationalNumber` con numerador 54 y denominador 10. Investiga el método `math.modf()` para este caso.

```python
def bigger(a, b): 
  """
  Devuelve el mayor número de 2 números reales dados.
  Args:
    a: Número real
    b: Número real
  Returns:
    Número real
  """
  if a >= b: 
    return a
  return b

def lower(a, b): 
  """
  Devuelve el menor número de 2 números reales dados.
  Args:
    a: Número real
    b: Número real
  Returns:
    Número real
  """
  if a <= b: 
    return a
  return b

def mcd(a, b): 
  """
  Devuelve el MCD de dos números enteros.
  Args:
    a: Número entero
    b: Número entero
  Returns:
    max: Número entero
  """
  r=0
  max = bigger(a, b) 
  min = lower(a, b)
  while(min > 0):
    r = min
    min = max % min 
    max = r
  return max

def helper(n, d):
    print("{} / {} = {}".format(n, d, n / d))

class RationalNumber():
    """
    Clase para trabajar con números racionales
    """
    def __init__(self, n, d = 1):
        if type(n) is int and type(d) is int:
            self.numerator = n
            self.denominator = d
        else:
            print("Numerador y Denominador deben ser números enteros.")


    def __str__(self):
        return ("{} / {}".format(self.numerator, self.denominator))


    def mathMode(self):
        from IPython.display import display, Latex
        display(Latex(f"${self.numerator}\\over{self.denominator}$"))


    def quotient(self):
        return self.numerator / self.denominator


    def isInfinite(self):
        if self.denominator == 0:
            return True
        else:
            return False
    

    def simplify(self):
        div = mcd(self.numerator, self.denominator)
        self.numerator = int(self.numerator / div)
        self.denominator = int(self.denominator / div)


    @staticmethod
    def sum(div1, div2):
        num = (div1.numerator * div2.denominator + div2.numerator * div1.denominator)
        den = (div1.denominator * div2.denominator)
        helper(num, den)
    

    @staticmethod
    def substract(div1, div2):
        num = (div1.numerator * div2.denominator - div2.numerator * div1.denominator)
        den = (div1.denominator * div2.denominator)
        helper(num, den)
    

    @staticmethod
    def product(div1, div2):
        num = div1.numerator * div2.numerator
        den = div1.denominator * div2.denominator
        helper(num,den)


    @staticmethod
    def division(div1, div2):
        num = div1.numerator * div2.denominator
        den = div1.denominator * div2.nominator
        helper(num,den)

    
    @classmethod
    def random(cls):
        import random
        num = random.randrange(1,11)
        den = random.randrange(1,11)
        cls(num,den)

    
    @classmethod
    def zero(cls):
        cls(0)
    

    @classmethod
    def one(cls):
        cls(1)

    
    @classmethod
    def fromRealNumber(cls, f):
    import math
    num = f
    den = 1
    d, i = math.modf(num)
    while d != 0:
      num *= 10
      den *= 10
      d, i = math.modf(num)
    num = int(num)
    den = int(den)
    return cls(num, den)
```

## Propiedades

Para manejar los atributos de un objeto, podemos utilizar el decorador `@property` que permite a un método ser accedido como un atributo, omitiendo así el uso de paréntesis vacíos.

**Observación.** los paréntesis son vacíos cuando en un método no hay parámetros que indicar.

Los métodos `.perimeter()` y `.area()` son el ejemplo perfecto para ser modificados por el decorador `@property` pues siempre que son llamados, nunca toman valores por parámetro.

```python
class Rectangle():

  def __init__(self, base = 1, height = 1, color = "blue"):
    self.base = base
    self.height = height
    self.color = color
  
  @property
  def perimeter(self):
    return 2 * self.base + 2 * self.height

  @property
  def area(self):
    return self.base * self.height

  def is_base_big(self, min = 5):
    if self.base > min:
      return True
    return False

  def __str__(self):
    return ("Base: {}\nAltura: {}".format(self.base, self.height))

  @staticmethod  
  def are_equal_size(rect1, rect2):
    if rect1.base == rect2.base and rect1.height == rect2.height:
      return True
    return False

  @classmethod
  def random_rectangle(cls):
    base = random.randrange(1, 10)
    height = random.randrange(1, 10)
    return cls(base, height)
```

```python
rect4 = Rectangle(2, 3, "yellow")
```

```python
rect4.perimeter

#RESPUESTA
10
```

```python
rect4.area

#RESPUESTA
6
```

**¡Cuidado!** El modificador únicamente nos permite acceder al método como si fuera un atributo, pero eso no significa que pueda ser tratado como tal. Si intentamos modificarlo como si fuera un atributo, nos saltará error

```python
rect4.perimeter = 12
```

Para poder modificar una propiedad, necesitamos utilizar el método `.setter()`.

Veámoslo con un ejemplo:

```python
class Person():

  def __init__(self, name, surname):
    self.name = name
    self.surname = surname

  @property
  def complete_name(self):
    return "{} {}".format(self.name, self.surname)

  @complete_name.setter
  def complete_name(self, name_surname):
    name, surname = name_surname.split(" ")
    self.name = name
    self.surname = surname
  
```

La clase `Person` toma como parámetros nombre y apellido de una persona. Tiene una propiedad que devuelve el nombre completo de dicha persona.

Gracias al método `.setter()` somos capaces de modificar dicha propiedad. Lo hemos conseguido usando un decorador con el nombre de la propiedad seguido de `.setter`.

Para modificar el nombre completo, debemos introducir este por parámetro.

```python
person1 = Person("María", "Gomila")
person1.complete_name

#RESPUESTA
'María Gomila'
```

```python
person1.complete_name = "María Santos"
person1.surname

#RESPUESTA
'Santos'
```

Otro uso muy común del método `.setter()` es prevenir al usuario de introducir valores que no deberían estar permitidos.

Por ejemplo, un círculo no puede tener un diámetro que valga 0 o menos:

```python
class Circle():

  def __init__(self, center = (0, 0), radius = 1):
    self.center = center
    self.radius = radius

  @property
  def diameter(self):
    return 2 * self.radius

  @diameter.setter
  def diameter(self, value):
    if value <= 0:
      raise ValueError("El diámetro no puede valer menor o igual a 0")
    self.radius = value / 2
  
```

Si probamos ahora de modificar el diámetro para que valga un valor 0 o negativo, entonces nos saltará el `ValueError` que hemos configurado previamente.

```python
circle1 = Circle(radius = 2)
circle1.diameter = -2

#RESPUESTA
ValueError: El diámetro no puede valer menor o igual a 0
```

#### EJERCICIO 6:&#x20;

Vamos a convertir los método .quotient() y .mathFormat() en una propiedad.

```python
def bigger(a, b): 
  """
  Devuelve el mayor número de 2 números reales dados.
  Args:
    a: Número real
    b: Número real
  Returns:
    Número real
  """
  if a >= b: 
    return a
  return b

def lower(a, b): 
  """
  Devuelve el menor número de 2 números reales dados.
  Args:
    a: Número real
    b: Número real
  Returns:
    Número real
  """
  if a <= b: 
    return a
  return b

def mcd(a, b): 
  """
  Devuelve el MCD de dos números enteros.
  Args:
    a: Número entero
    b: Número entero
  Returns:
    max: Número entero
  """
  r=0
  max = bigger(a, b) 
  min = lower(a, b)
  while(min > 0):
    r = min
    min = max % min 
    max = r
  return max

def helper(n, d):
    print("{} / {} = {}".format(n, d, n / d))

class RationalNumber():
    """
    Clase para trabajar con números racionales
    """
    def __init__(self, n, d = 1):
        if type(n) is int and type(d) is int:
            self.numerator = n
            self.denominator = d
        else:
            print("Numerador y Denominador deben ser números enteros.")


    def __str__(self):
        return ("{} / {}".format(self.numerator, self.denominator))


    @property
    def mathFormat(self):
        from IPython.display import display, Latex
        display(Latex(f"${self.numerator}\\over{self.denominator}$"))


    @property
    def quotient(self):
        return self.numerator / self.denominator


    def isInfinite(self):
        if self.denominator == 0:
            return True
        else:
            return False
    

    def simplify(self):
        div = mcd(self.numerator, self.denominator)
        self.numerator = int(self.numerator / div)
        self.denominator = int(self.denominator / div)


    @staticmethod
    def sum(div1, div2):
        num = (div1.numerator * div2.denominator + div2.numerator * div1.denominator)
        den = (div1.denominator * div2.denominator)
        helper(num, den)
    

    @staticmethod
    def substract(div1, div2):
        num = (div1.numerator * div2.denominator - div2.numerator * div1.denominator)
        den = (div1.denominator * div2.denominator)
        helper(num, den)
    

    @staticmethod
    def product(div1, div2):
        num = div1.numerator * div2.numerator
        den = div1.denominator * div2.denominator
        helper(num,den)


    @staticmethod
    def division(div1, div2):
        num = div1.numerator * div2.denominator
        den = div1.denominator * div2.nominator
        helper(num,den)

    
    @classmethod
    def random(cls):
        import random
        num = random.randrange(1,11)
        den = random.randrange(1,11)
        cls(num,den)

    
    @classmethod
    def zero(cls):
        cls(0)
    

    @classmethod
    def one(cls):
        cls(1)

    
    @classmethod
    def fromRealNumber(cls, f):
        import math
        num = f
        den = 1
        d, i = math.modf(num)
        while d != 0:
            num *= 10
            den *= 10
            d, i = math.modf(num)
        num = int(num)
        den = int(den)
        return cls(num, den)
```

## Clase `inheritance`

Esta clase permite a los atributos y métodos ser pasados de una clase a otra. Es útil cuando ya existe una clase que hace todo lo que necesitamos, a la cuál querríamos añadir algún atributo o método extra.

Supongamos que queremos crear dos clases: una representando niños (personas menores de edad) y otra representando adultos.

La clase `Children` sería:

```python
class Children():

  is_adult = False

  def __init__(self, name, surname, age):
    self.name = name
    self.surname = surname
    self.age = age

  @property
  def complete_name(self):
    return "{} {}".format(self.name, self.surname)

  @complete_name.setter
  def complete_name(self, name_surname):
    name, surname = name_surname.split(" ")
    self.name = name
    self.surname = surname
```

Y la clase `Adult`,

```python
class Adult():

  is_adult = True

  def __init__(self, name, surname, age):
    self.name = name
    self.surname = surname
    self.age = age

  @property
  def complete_name(self):
    return "{} {}".format(self.name, self.surname)

  @complete_name.setter
  def complete_name(self, name_surname):
    name, surname = name_surname.split(" ")
    self.name = name
    self.surname = surname
```

Estamos repitiendo mucho código. Para ser exactos, la única diferencia entre ambas clases es el atributo `.is_adult`, que en `Children` vale `False` y en `Adult` vale `True`.

### Single Inheritance

Implica crear clases hijo que heredan atributos y métodos de una sola clase padre. Tomando las dos clases anteriores, `Children` y `Adult`, tenemos la clase `Person` que representa las partes comunes de las clases `Children` y `Adult`.

```python
class Person(object):

  def __init__(self, name, surname, age):
    self.name = name
    self.surname = surname
    self.age = age

  @property
  def complete_name(self):
    return "{} {}".format(self.name, self.surname)

  @complete_name.setter
  def complete_name(self, name_surname):
    name, surname = name_surname.split(" ")
    self.name = name
    self.surname = surname
```

De modo que ahora las clases `Children` y `Adult` pueden ser creadas como hijos de la clase padre `Person`

```python
class Children(Person):
  is_adult = False
```

```python
class Adult(Person):
  is_adult = True
```

```python
child = Children("Juan", "Sánchez", 6)
child.name
```

```
'Juan'
```

De este modo, la lógica del `.__init__()` solo se especifica una vez, haciendo mucho más sencillo el modificarlo en un futuro desde la clase padre. Del mismo modo, también será más sencillo crear subclases diferentes de la clase `Person`. Además, también es posible crear subclases de la ya subclase `Children`, como por ejemplo `Teenager` dependiendo del rango de edad dentro del intervalo \[0, 18).

![single inheritance](<../.gitbook/assets/image (3) (1).png>)

Así como hemos heredado de la clase que hemos creado, `Person`, podemos heredar de una clase ya existente en `Python`, como por ejemplo la clase `int`

```python
class MyInt(int):
  def is_divisible_by(self, divisor):
    return self % divisor == 0
```

```python
n = MyInt(27)
n.is_divisible_by(9)

#RESPUESTA
True
```

### **Sobreescribiendo métodos**

#### Con la herencia de clases, no solo podemos extender el comportamiento de clases más generales, sino que también podemos modificar algunos atributos o métodos heredados de la clase padre.

Supongamos que tenemos la clase `Person()`

```python
class Person(object):

  def __init__(self, name, surname, age):
    self.name = name
    self.surname = surname
    self.age = age

  @property
  def complete_name(self):
    return "{} {}".format(self.name, self.surname)

  @complete_name.setter
  def complete_name(self, name_surname):
    name, surname = name_surname.split(" ")
    self.name = name
    self.surname = surname
```

Pero que a la hora de introducir el nombre completo, tenemos problemas pues la persona tiene segundo nombre. Entonces podríamos crear una clase `SecondNamePerson` que tomase en consideración estos aspectos con respecto al nombre completo.

```python
class SecondNamePerson(Person):
  @property
  def complete_name(self):
    return "{} {}".format(self.name, self.surname)

  @complete_name.setter
  def complete_name(self, names_surname):
    names = names_surname.split(" ")
    self.surname = names[-1]
    if len(names) > 2:
      self.name = " ".join(names[:(len(names)-1)])
    elif len(names) == 2:
      self.name = names[0]
```

```python
person2 = SecondNamePerson("Juan", "Gomila", 32)
person2.complete_name = "Juan Gabriel Gomila"
print(person2.name)
print(person2.surname)

#RESPUESTA
Juan Gabriel
Gomila
```

#### **El método `.super()`**

El método `.super()` nos sirve para acceder a un método de la clase padre.

```python
class Person(object):

  def __init__(self, name, surname, age):
    self.name = name
    self.surname = surname
    self.age = age

  @property
  def complete_name(self):
    return "{} {}".format(self.name, self.surname)

  @complete_name.setter
  def complete_name(self, name_surname):
    name, surname = name_surname.split(" ")
    self.name = name
    self.surname = surname
  
  @property
  def introduction(self):
    print("Hola, mi nombre es {}".format(self.complete_name))
```

Supongamos que queremos crear una subclase para que una persona diga muchas más cosas a la hora de presentarse:

```python
class TalkativePerson(Person):

    @property
    def introduction(self):
        print("Hola, mi nombre es {}".format(self.complete_name))
        print("Un placer conocerte!")
```

```python
person3 = TalkativePerson("Paula", "Olivera", 16)
person3.introduction

#RESPUESTA
Hola, mi nombre es Paula Olivera
Un placer conocerte!
```

Lo hecho anteriormente es correcto, aunque estamos copiando la primera frase tal cual está en la clase `Person`. Para evitar dicha copia, lo que podemos hacer es utilizar el método `.super()`

```python
class TalkativePerson(Person):

    @property
    def introduction(self):
        super().introduction
        print("Un placer conocerte!")
```

```python
person4 = TalkativePerson("Marta", "Fernández", 16)
person4.introduction

#RESPUESTA
Hola, mi nombre es Marta Fernández
Un placer conocerte!
```

#### EJERCICIO 7:&#x20;

Dada la clase Point2D, vamos a crear la clase Point3D que hereda de Point2D.

Vamos a modificar todos los métodos y usar el método .super() donde sea necesario para poder usarlos con puntos de 3 dimensiones.

```python
class Point2D():
  
  def __init__(self, x, y):
    self.x = x
    self.y = y

  def __str__(self):
    return "({}, {})".format(self.x, self.y)

  @classmethod
  def zero(cls):
    return cls(0, 0)
```

```python
class Point3D(Point2D):

    def __init__(self, x, y, z):
        super().__init__(x, y)
        self.z = z

    def __str__(self):
        return super().__str__()[:-1] + ", {})".format(self.z)
    
    @classmethod
    def zero(cls):
        return cls(0, 0, 0)
```

### Multiple Inheritance

Implica crear clases hijo que heredan atributos y métodos de múltiples clases padre.

![multiple inheritance](<../.gitbook/assets/image (2).png>)

En este caso, además de la clase `Adult`, que hereda de la clase `Person`, vamos a tener la clase `Calendar`.

```python
class Person(object):

  def __init__(self, name, surname, age):
    self.name = name
    self.surname = surname
    self.age = age

  @property
  def complete_name(self):
    return "{} {}".format(self.name, self.surname)

  @complete_name.setter
  def complete_name(self, name_surname):
    name, surname = name_surname.split(" ")
    self.name = name
    self.surname = surname
  
  @property
  def introduction(self):
    print("Hola, mi nombre es {}".format(self.complete_name))

class Adult(Person):
  is_adult = True
```

```python
class Calendar(object):

  @staticmethod
  def new_event(title, day, hour, duration = "All day"):
    print("Reservado el día {} a las {} durante {} para {}".format(day, hour, duration, title))
```

Por último, vamos a crear una subclase que herede tanto de `Adult` como de `Calendar`, a la que llamaremos `Bussinessman` que no tendrá ningún método ni argumento adicional. Por tanto, tendremos que hacer uso de la instrucción `pass`

```python
class Bussinessman(Adult, Calendar):
  pass
```

```python
bussinessman = Bussinessman("Manuel", "Gómez", 38)
bussinessman.introduction
Bussinessman.new_event("Reunión", "30 de Septiembre", "16:30", "2 horas")

#RESPUESTA
Hola, mi nombre es Manuel Gómez
Reservado el día 30 de Septiembre a las 16:30 durante 2 horas para Reunión
```

#### **El método `.super()`**

Ahora que heredamos de más de una clase padre ¿qué ocurre cuando usamos el método `.super()`?

Si ninguna de las clases padres tiene algún método con el mismo nombre, entonces no hay ningún problema. No obstante, si nos encontramos en el caso contrario, donde hay uno o más métodos con el mismo nombre en ambas clases, entonces el método que va a ser usado al llamarlo con el método `.super()` es el perteneciente a la primera clase padre de la cual se hereda.

Veámoslo con un ejemplo: tenemos la clase `ClassAB` que heredará de las clases `ClassA` y `ClassB`

```python
class ClassA():

  def say_letter(self):
    print("Mi letrita es la A")

  
class ClassB(): 
  
  def say_letter(self):
    print("Mi letrita es la B")
```

```python
class ClassAB(ClassA, ClassB):

  def my_letter(self):
    print("A pesar de que heredo las letras A y B (así lo indica mi nombre)")
    super().say_letter()
    
#RESPUESTA
ab = ClassAB()

```

```python
ab.my_letter()

#RESPUESTA
A pesar de que heredo las letras A y B (así lo indica mi nombre)
Mi letrita es la A
```

```python
class ClassAB(ClassB, ClassA):

  def my_letter(self):
    print("A pesar de que heredo las letras A y B (así lo indica mi nombre)")
    super().say_letter()
```

```python
ab = ClassAB()
ab.my_letter()

#RESPUESTA
A pesar de que heredo las letras A y B (así lo indica mi nombre)
Mi letrita es la B
```

**Observación.** Esto no solo ocurre cuando usamos el método `.super()`, sino también cuando queremos acceder a un método cuyo nombre está presente en más de una clase padre.

```python
class ClassAB(ClassA, ClassB):
  pass
```

```python
ab = ClassAB()
ab.say_letter()

#RESPUESTA
Mi letrita es la A
```

```python
class ClassAB(ClassB, ClassA):
  pass
```

```python
ab = ClassAB()
ab.say_letter()

#RESPUESTA
Mi letrita es la B
```

#### EJERCICIO 8:&#x20;

Dadas las clases Triangle y Square, vamos a crear la clase Pyramid que hereda de las dos anteriores. Practicaremos la herencia múltiple.

Vamos a implementar el constructor, el método .area() y el método .volume() usando el método .super() donde sea necesario para poder construir una pirámide regular con base cuadrada y calcular correctamente el área y el volumen.

```python
class Square():
  def __init__(self, base):
    self.base = base

  @property
  def perimeter(self):
    return 4 * self.base

  @property
  def area(self):
    return self.base * self.base

class Triangle():
  def __init__(self, base, height):
    self.base = base
    self.height = height
  
  @property
  def area(self):
    return 0.5 * self.base * self.height
```

```python
import math

class Pyramid(Square, Triangle):
    def __init__(self, base, height):
        super().__init__(base)
        #Altura de la piramide.
        self.height = height

    def slang_height(self):
        return math.sqrt((self.base / 2) ** 2 + self.height ** 2)

    @property    
    def area(self):
        base_area = super().area
        base_perimeter = super().base_perimeter
        lateral_area = 0.5 * base_perimeter * self.slang_height
        return lateral_area + base_area

    @property
    def volume(self):
        base_area = super().area
        return base_area * self.height / 3
```

## Polimorfismo

**Polimorfismo.** Significa que una función con el mismo nombre se utiliza para diferentes tipos de objeto.

Un ejemplo perfecto es la función `len()` que sirve tanto para objetos de tipo `string` como listas.

```python
print(len("matematicas")) # Aplicada a string
print(len([1, 2, 3])) # Aplicada a lista

#RESPUESTA
11
3
```

En la programación orientada a objetos también nos encontramos con funciones que tienen el mismo nombre, pero pueden ser aplicadas a diferentes objetos.

```python
class Spain(): 
    def capital(self): 
        print("Madrid es la capital de España") 
  
    def language(self): 
        print("En España se habla el español") 

  
class Portugal(): 
    def capital(self): 
        print("Lisboa es la capital de Portugal.") 
  
    def language(self): 
        print("En Portugal se habla el portugués") 

  
spain = Spain() 
portugal = Portugal() 
for country in (spain, portugal): 
    country.capital() 
    country.language()
    print("") 
```

```
#RESPUESTA
Madrid es la capital de España
En España se habla el español

Lisboa es la capital de Portugal.
En Portugal se habla el portugués
```

Incluso cuando hablamos de herencia, también podemos encontrarnos con polimorfismos tal y como vimos por ejemplo con las clases `Person` y `SecondNamePerson`, donde ambas compartían el método `.complete_name()`

```python
class Person():

  def __init__(self, name, surname, age):
    self.name = name
    self.surname = surname
    self.age = age

  @property
  def complete_name(self):
    return "{} {}".format(self.name, self.surname)

  @complete_name.setter
  def complete_name(self, name_surname):
    name, surname = name_surname.split(" ")
    self.name = name
    self.surname = surname
```

```python
class SecondNamePerson(Person):
  @property
  def complete_name(self):
    return "{} {}".format(self.name, self.surname)

  @complete_name.setter
  def complete_name(self, names_surname):
    names = names_surname.split(" ")
    self.surname = names[-1]
    if len(names) > 2:
      self.name = " ".join(names[:(len(names)-1)])
    elif len(names) == 2:
      self.name = names[0]
```

```python
person2 = SecondNamePerson("Juan", "Gomila", 32)
person2.complete_name = "Juan Gabriel Gomila"
print(person2.name)
print(person2.surname)
```

```
Juan Gabriel
Gomila
```

### Variables privadas: Mangling

```python
class A:
    def __init__(self):
        self.__var = 123
        self.name = "Juan Gabriel"
    
    def printVar(self):
        print(self.__var)

    def __printName(self):
        print(self.name)
```

```python
x = A()
```

```python
x.printVar()
```

```
123
```

```python
x.__var
```

```
---------------------------------------------------------------------------

AttributeError                            Traceback (most recent call last)

<ipython-input-8-12498366ca10> in <module>()
----> 1 x.__var


AttributeError: 'A' object has no attribute '__var'
```

```python
x.name
```

```
'Juan Gabriel'
```

```python
x.__printName()
```

```
---------------------------------------------------------------------------

AttributeError                            Traceback (most recent call last)

<ipython-input-12-4332d910291d> in <module>()
----> 1 x.__printName()


AttributeError: 'A' object has no attribute '__printName'
```

```python
class Info:
    def __init__(self, iterate):
        self.list = []
        self.__generateData(iterate)

    def generateData(self, iterate):
        for item in iterate:
            self.list.append(item)

    __generateData = generateData


class InfoSubclass(Info):
    def generateData(self, keys, values):
        for i in zip(keys, values):
            self.list.append(i)
```

## REPASO

```python
#EJERCICIO 1: A lo largo de toda esta taraea vas a construir la clase Date. Empieza con el constructor, que recibe por
#parámetros el día (day), mes (month) y año (year). Los 3 parámetros son de tipo int y por defecto todos
#valen 1.

class Date():

    def __init__(self, d = 1, m = 1, y = 1):
        if type(d) == int and type(m) == int and type(y) == int:
            self.day = d
            self.month = m
            self.year = y
        else:
            print("Los datos suministrados deben ser números enteros.")
```

```python
#EJERCICIO 2: Configura el método .__str__() para que muestre la fecha en formato day / month / year. Si el valor
#del día o el mes son menores a 10, mostrar el valor con un 0 delante. Por ejemplo, si day = 8, month = 7 y
#year = 1998, entonces se debería mostrar 08 / 07 / 1998.
#En el caso del año, si el año es menor a 1000, mostrar con un cero delante; si es menor a 100, mostrar con 2
#ceros delante; y si es menor a 10, mostrar con 3 ceros delante.
#PISTA: Puedes crear una función que dado un número entero y el número de cifras que debe tener, rellene
#con ceros a la izquierda hasta completar el número de cifras indicado.

def add_left(num, cantidad):
    """
    Función que añade tantos ceros a la 
    izquierda del número (num) para alcanzar
    la cantidad solicitada.
    No es bonita pero funciona.
    """

    if num > cantidad:
        return str(num)
    else:
        b = 10
        while num * b < cantidad:
            b *= 10
        return str(b)[1:] + str(num)

class Date():
    
    def __init__(self, d = 1, m = 1, y = 1):
        if type(d) == int and type(m) == int and type(y) == int:
            self.day = d
            self.month = m
            self.year = y
        else:
            print("Los datos suministrados deben ser números enteros.")

    def __str__(self):
        return ("{} / {} / {}". format(add_left(self.day, 10), add_left(self.month, 10), add_left(self.year, 1000)))
```

```python
#EJERCICIO 3: Implementa el método de instancia .isLeap() que diga si el año es bisiesto o no.

def add_left(num, cantidad):
    """
    Función que añade tantos ceros a la 
    izquierda del número (num) para alcanzar
    la cantidad solicitada.
    No es bonita pero funciona.
    """
    if num > cantidad:
        return str(num)
    else:
        b = 10
        while num * b < cantidad:
            b *= 10
        return str(b)[1:] + str(num)
    
class Date():
    
    def __init__(self, d = 1, m = 1, y = 1):
        if type(d) == int and type(m) == int and type(y) == int:
            self.day = d
            self.month = m
            self.year = y
        else:
            print("Los datos suministrados deben ser números enteros.")

    def __str__(self):
        return ("{} / {} / {}". format(add_left(self.day, 10), add_left(self.month, 10), add_left(self.year, 1000)))

    def isLeap(self):
        if (self.year % 4 == 0 and self.year % 100 != 0) or (self.year % 4 == 0 and self.year % 100 == 0 and self.year % 400 == 0):
            return True
        else:
            return False
```

```python
#EJERCICIO 4: 
#Implementa un método de instancia .totalMonthDays() que diga el número de días del mes. Ten en
#cuenta que en los años bisiestos, Febrero tiene 29 días.
#Implementa el método de instancia .validDate() que determine si una fecha es válida. Modifica el
#constructor para que si la fecha introducida no es válida, devuelva un mensaje indicando “¡¡¡La fecha
#introducida no es una fecha válida!!!”

def add_left(num, cantidad):
    """
    Función que añade tantos ceros a la 
    izquierda del número (num) para alcanzar
    la cantidad solicitada.
    No es bonita pero funciona.
    """
    if num > cantidad:
        return str(num)
    else:
        b = 10
        while num * b < cantidad:
            b *= 10
        return str(b)[1:] + str(num)
    
class Date():
    
    def __init__(self, d = 1, m = 1, y = 1):
        if type(d) == int and type(m) == int and type(y) == int:
            self.day = d
            self.month = m
            self.year = y
        else:
            print("Los datos suministrados deben ser números enteros.")
        if self.validDate() == False:
            print("¡¡¡La fecha introducida no es una fecha válida!!!")

    def __str__(self):
        return ("{} / {} / {}". format(add_left(self.day, 10), add_left(self.month, 10), add_left(self.year, 1000)))

    def isLeap(self):
        if (self.year % 4 == 0 and self.year % 100 != 0) or (self.year % 4 == 0 and self.year % 100 == 0 and self.year % 400 == 0):
            return True
        else:
            return False

    def totalMonthDays(self):
        month_days = 0
        if self.month == 1 or self.month == 3 or self.month == 5 or self.month == 7 or self.month == 8 or self.month == 10 or self.month == 12:
            month_days = 31 
        elif self.month == 4 or self.month == 6 or self.month == 9 or self.month == 11:
            month_days = 30
        elif self.month == 2 and self.isLeap() == True:
            month_days = 29
        else:
            month_days = 28
        return month_days

    def validDate(self):
        if self.totalMonthDays() >= self.day and self.month <= 12:
            return True
        else:
            return False
```

```python
#EJERCICIO 5: Implementa la propiedad .monthName que devuelva el nombre del mes en inglés. Por ejemplo, si nuestra
#fecha es day = 8, month = 7 y year = 1998, la propiedad debe devolver July.
def add_left(num, cantidad):
    """
    Función que añade tantos ceros a la 
    izquierda del número (num) para alcanzar
    la cantidad solicitada.
    No es bonita pero funciona.
    """
    if num > cantidad:
        return str(num)
    else:
        b = 10
        while num * b < cantidad:
            b *= 10
        return str(b)[1:] + str(num)
    
class Date():
    
    months = ["January", "February", "March", "April", "May", "Juny", "July", "August", "September", "October", "November", "December"]

    def __init__(self, d = 1, m = 1, y = 1):
        if type(d) == int and type(m) == int and type(y) == int:
            self.day = d
            self.month = m
            self.year = y
        else:
            print("Los datos suministrados deben ser números enteros.")
        if self.validDate() == False:
            print("¡¡¡La fecha introducida no es una fecha válida!!!")

    def __str__(self):
        return ("{} / {} / {}". format(add_left(self.day, 10), add_left(self.month, 10), add_left(self.year, 1000)))

    def isLeap(self):
        if (self.year % 4 == 0 and self.year % 100 != 0) or (self.year % 4 == 0 and self.year % 100 == 0 and self.year % 400 == 0):
            return True
        else:
            return False

    def totalMonthDays(self):
        month_days = 0
        if self.month == 1 or self.month == 3 or self.month == 5 or self.month == 7 or self.month == 8 or self.month == 10 or self.month == 12:
            month_days = 31 
        elif self.month == 4 or self.month == 6 or self.month == 9 or self.month == 11:
            month_days = 30
        elif self.month == 2 and self.isLeap() == True:
            month_days = 29
        else:
            month_days = 28
        return month_days

    def validDate(self):
        if self.totalMonthDays() >= self.day and self.month <= 12:
            return True
        else:
            return False
    
    @property
    def monthName(self):
        return months[self.month + 1]
```

```python
#EJERCICIO 6: 
#• Implementa el método estático .areEqual(), que dadas dos fechas diga si son iguales.
#• Implementa el método estático .isLater(), que dadas dos fechas diga si la primera es posterior a la
#segunda.
#• Implementa el método estático .isPrevious(), que dadas dos fechas diga si la primera es anterior a
#la segunda.

def add_left(num, cantidad):
    """
    Función que añade tantos ceros a la 
    izquierda del número (num) para alcanzar
    la cantidad solicitada.
    No es bonita pero funciona.
    """
    if num > cantidad:
        return str(num)
    else:
        b = 10
        while num * b < cantidad:
            b *= 10
        return str(b)[1:] + str(num)
    
class Date():
    
    months = ["January", "February", "March", "April", "May", "Juny", "July", "August", "September", "October", "November", "December"]

    def __init__(self, d = 1, m = 1, y = 1):
        if type(d) == int and type(m) == int and type(y) == int:
            self.day = d
            self.month = m
            self.year = y
        else:
            print("Los datos suministrados deben ser números enteros.")
        if self.validDate() == False:
            print("¡¡¡La fecha introducida no es una fecha válida!!!")

    def __str__(self):
        return ("{} / {} / {}". format(add_left(self.day, 10), add_left(self.month, 10), add_left(self.year, 1000)))

    def isLeap(self):
        if (self.year % 4 == 0 and self.year % 100 != 0) or (self.year % 4 == 0 and self.year % 100 == 0 and self.year % 400 == 0):
            return True
        else:
            return False

    def totalMonthDays(self):
        month_days = 0
        if self.month == 1 or self.month == 3 or self.month == 5 or self.month == 7 or self.month == 8 or self.month == 10 or self.month == 12:
            month_days = 31 
        elif self.month == 4 or self.month == 6 or self.month == 9 or self.month == 11:
            month_days = 30
        elif self.month == 2 and self.isLeap() == True:
            month_days = 29
        else:
            month_days = 28
        return month_days

    def validDate(self):
        if self.totalMonthDays() >= self.day and self.month <= 12:
            return True
        else:
            return False
    
    @property
    def monthName(self):
        return months[self.month + 1]
    
    @staticmethod
    def areEqual(date1, date2):
        if date1.day == date2.day and date1.month == date2.month and date1.year == date2.year:
            return True
        else:
            return False
    
    @staticmethod
    def isLater(date1, date2):
        if date1.year > date2.year:
            return True
        elif date1.year == date2.year and date1.month > date2.month:
            return True
        elif date1.year == date2.year and date1.month == date2.month and date1.day > date2.day:
            return True
        else
            return False
    
    @staticmethod
    def isPrevious(date1, date2):
         if date1.year < date2.year:
            return True
        elif date1.year == date2.year and date1.month < date2.month:
            return True
        elif date1.year == date2.year and date1.month == date2.month and date1.day < date2.day:
            return True
        else
            return False
```

```python
#EJERCICIO 7: 
#• Implementa el método de clase .firstDayOfTheYear() que dado un año cree un objeto Date con la
#fecha correspondiente al primer día del año indicado.
#• Implementa el método de clase .lastDayOfTheYear() que dado un año cree un objeto Date con la
#fecha correspondiente al último día del año indicado.
#• Implementa el método de instancia .plusDay() que incremente un día la fecha. Ten en cuenta que si
#estamos en el último día del mes y añadimos un día, tendremos que cambiar de mes (pasar al siguiente).
#Y lo mismo si estamos en el último día del año (tendremos que pasar al siguiente año).
#• Implementa el método de instancia .minusDay() que decremente un día la fecha. Ten en cuenta que si
#estamos en el primer día del mes y restamos un día, tendremos que cambiar de mes (pasar al anterior).
#Y lo mismo si estamos en el primer día del año (tendremos que pasar al año anterior).

def add_left(num, cantidad):
    """
    Función que añade tantos ceros a la 
    izquierda del número (num) para alcanzar
    la cantidad solicitada.
    No es bonita pero funciona.
    """
    if num > cantidad:
        return str(num)
    else:
        b = 10
        while num * b < cantidad:
            b *= 10
        return str(b)[1:] + str(num)
    
class Date():
    
    months = ["January", "February", "March", "April", "May", "Juny", "July", "August", "September", "October", "November", "December"]

    def __init__(self, d = 1, m = 1, y = 1):
        if type(d) == int and type(m) == int and type(y) == int:
            self.day = d
            self.month = m
            self.year = y
        else:
            print("Los datos suministrados deben ser números enteros.")
        if self.validDate() == False:
            print("¡¡¡La fecha introducida no es una fecha válida!!!")

    def __str__(self):
        return ("{} / {} / {}". format(add_left(self.day, 10), add_left(self.month, 10), add_left(self.year, 1000)))

    def isLeap(self):
        if (self.year % 4 == 0 and self.year % 100 != 0) or (self.year % 4 == 0 and self.year % 100 == 0 and self.year % 400 == 0):
            return True
        else:
            return False

    def totalMonthDays(self):
        month_days = 0
        if self.month == 1 or self.month == 3 or self.month == 5 or self.month == 7 or self.month == 8 or self.month == 10 or self.month == 12:
            month_days = 31 
        elif self.month == 4 or self.month == 6 or self.month == 9 or self.month == 11:
            month_days = 30
        elif self.month == 2 and self.isLeap() == True:
            month_days = 29
        else:
            month_days = 28
        return month_days

    def validDate(self):
        if self.totalMonthDays() >= self.day and self.month <= 12:
            return True
        else:
            return False
    
    @property
    def monthName(self):
        return months[self.month + 1]
    
    @staticmethod
    def areEqual(date1, date2):
        if date1.day == date2.day and date1.month == date2.month and date1.year == date2.year:
            return True
        else:
            return False
    
    @staticmethod
    def isLater(date1, date2):
        if date1.year > date2.year:
            return True
        elif date1.year == date2.year and date1.month > date2.month:
            return True
        elif date1.year == date2.year and date1.month == date2.month and date1.day > date2.day:
            return True
        else:
            return False
    
    @staticmethod
    def isPrevious(date1, date2):
        if date1.year < date2.year:
            return True
        elif date1.year == date2.year and date1.month < date2.month:
            return True
        elif date1.year == date2.year and date1.month == date2.month and date1.day < date2.day:
            return True
        else:
            return False

    @classmethod
    def firstDayOfTheYear(cls, year):
        return cls(1, 1, year)

    @classmethod
    def lastDayOfTheYear(cls, year):
        return cls(31, 12, year)

    def plusDay(self):
        if self.day == self.totalMonthDays() and self.month == 12:
            self.day = 1
            self.month = 1
            self.year += 1
        elif self.day == self.totalMonthDays():
            self.day = 1
            self.month += 1
        else:
            self.day += 1
    
    def minusDay(self):
        if self.day == 1 and self.month == 1:
            self.day = 31
            self.month = 12
            self.year -= 1
        elif self.day == 1:
            self.month -= 1
            self.day = self.totalMonthDays()
        else:
            self.day -= 1
```

```python
#EJERCICIO 8: 
#• Implementa el método de clase .copy() que dado un objeto Date, devuelva otro objeto Date con los
#mismos atributos.
#• Implementea el método estático .difference() que dadas dos fechas devuelva el número de días que
#hay entre ellas.

def add_left(num, cantidad):
    """
    Función que añade tantos ceros a la 
    izquierda del número (num) para alcanzar
    la cantidad solicitada.
    No es bonita pero funciona.
    """
    if num > cantidad:
        return str(num)
    else:
        b = 10
        while num * b < cantidad:
            b *= 10
        return str(b)[1:] + str(num)
    
class Date():
    
    months = ["January", "February", "March", "April", "May", "Juny", "July", "August", "September", "October", "November", "December"]


    def __init__(self, d = 1, m = 1, y = 1):
        if type(d) == int and type(m) == int and type(y) == int:
            self.day = d
            self.month = m
            self.year = y
        else:
            print("Los datos suministrados deben ser números enteros.")
        if self.validDate() == False:
            print("¡¡¡La fecha introducida no es una fecha válida!!!")

    def __str__(self):
        return ("{} / {} / {}". format(add_left(self.day, 10), add_left(self.month, 10), add_left(self.year, 1000)))

    def isLeap(self):
        if (self.year % 4 == 0 and self.year % 100 != 0) or (self.year % 4 == 0 and self.year % 100 == 0 and self.year % 400 == 0):
            return True
        else:
            return False

    def totalMonthDays(self):
        month_days = 0
        if self.month == 1 or self.month == 3 or self.month == 5 or self.month == 7 or self.month == 8 or self.month == 10 or self.month == 12:
            month_days = 31 
        elif self.month == 4 or self.month == 6 or self.month == 9 or self.month == 11:
            month_days = 30
        elif self.month == 2 and self.isLeap() == True:
            month_days = 29
        else:
            month_days = 28
        return month_days

    def validDate(self):
        if self.totalMonthDays() >= self.day and self.month <= 12:
            return True
        else:
            return False
    
    @property
    def monthName(self):
        return months[self.month + 1]
    
    @staticmethod
    def areEqual(date1, date2):
        if date1.day == date2.day and date1.month == date2.month and date1.year == date2.year:
            return True
        else:
            return False
    
    @staticmethod
    def isLater(date1, date2):
        if date1.year > date2.year:
            return True
        elif date1.year == date2.year and date1.month > date2.month:
            return True
        elif date1.year == date2.year and date1.month == date2.month and date1.day > date2.day:
            return True
        else:
            return False
    
    @staticmethod
    def isPrevious(date1, date2):
        if date1.year < date2.year:
            return True
        elif date1.year == date2.year and date1.month < date2.month:
            return True
        elif date1.year == date2.year and date1.month == date2.month and date1.day < date2.day:
            return True
        else:
            return False

    @classmethod
    def firstDayOfTheYear(cls, year):
        return cls(1, 1, year)

    @classmethod
    def lastDayOfTheYear(cls, year):
        return cls(31, 12, year)

    def plusDay(self):
        if self.day == self.totalMonthDays() and self.month == 12:
            self.day = 1
            self.month = 1
            self.year += 1
        elif self.day == self.totalMonthDays():
            self.day = 1
            self.month += 1
        else:
            self.day += 1
    
    def minusDay(self):
        if self.day == 1 and self.month == 1:
            self.day = 31
            self.month = 12
            self.year -= 1
        elif self.day == 1:
            self.month -= 1
            self.day = self.totalMonthDays()
        else:
            self.day -= 1
    
    @classmethod
    def copy(cls):
        return cls()

    @staticmethod
    def difference(date1, date2):
        d = 0
        if date1.year < date2.year:
            print("Los días que han pasado no pueden ser negativos.")
        if date1.year > date2.year:
            y = date2.year 
            while y < date1.year:
                d += 365
                y += 1
        if date1.month > date2.month:
            m = date2.month
            while date2.month < date1.month:
                d += date2.totalMonthDays()
                date2.month += 1
            date2.month = m
        elif date2.month > date1.month:
            m = date2.month
            while date2.month > date1.month:
                d -= date2.totalMonthDays()
                date2.month -= 1
            date2.month = m
        d += date1.day - date2.day
        return d
```

```python
#EJERCICIO 9: Implementa el método de clase .randomDate() que cree una fecha aleatoria válida.

def add_left(num, cantidad):
    """
    Función que añade tantos ceros a la 
    izquierda del número (num) para alcanzar
    la cantidad solicitada.
    No es bonita pero funciona.
    """
    if num > cantidad:
        return str(num)
    else:
        b = 10
        while num * b < cantidad:
            b *= 10
        return str(b)[1:] + str(num)
    
class Date():
    
    months = ["January", "February", "March", "April", "May", "Juny", "July", "August", "September", "October", "November", "December"]

    def __init__(self, d = 1, m = 1, y = 1):
        if type(d) == int and type(m) == int and type(y) == int:
            self.day = d
            self.month = m
            self.year = y
        else:
            print("Los datos suministrados deben ser números enteros.")
        if self.validDate() == False:
            print("¡¡¡La fecha introducida no es una fecha válida!!!")

    def __str__(self):
        return ("{} / {} / {}". format(add_left(self.day, 10), add_left(self.month, 10), add_left(self.year, 1000)))

    def isLeap(self):
        if (self.year % 4 == 0 and self.year % 100 != 0) or (self.year % 4 == 0 and self.year % 100 == 0 and self.year % 400 == 0):
            return True
        else:
            return False

    def totalMonthDays(self):
        month_days = 0
        if self.month == 1 or self.month == 3 or self.month == 5 or self.month == 7 or self.month == 8 or self.month == 10 or self.month == 12:
            month_days = 31 
        elif self.month == 4 or self.month == 6 or self.month == 9 or self.month == 11:
            month_days = 30
        elif self.month == 2 and self.isLeap() == True:
            month_days = 29
        else:
            month_days = 28
        return month_days

    def validDate(self):
        if self.totalMonthDays() >= self.day and self.month <= 12:
            return True
        else:
            return False
    
    @property
    def monthName(self):
        return months[self.month + 1]
    
    @staticmethod
    def areEqual(date1, date2):
        if date1.day == date2.day and date1.month == date2.month and date1.year == date2.year:
            return True
        else:
            return False
    
    @staticmethod
    def isLater(date1, date2):
        if date1.year > date2.year:
            return True
        elif date1.year == date2.year and date1.month > date2.month:
            return True
        elif date1.year == date2.year and date1.month == date2.month and date1.day > date2.day:
            return True
        else:
            return False
    
    @staticmethod
    def isPrevious(date1, date2):
        if date1.year < date2.year:
            return True
        elif date1.year == date2.year and date1.month < date2.month:
            return True
        elif date1.year == date2.year and date1.month == date2.month and date1.day < date2.day:
            return True
        else:
            return False

    @classmethod
    def firstDayOfTheYear(cls, year):
        return cls(1, 1, year)

    @classmethod
    def lastDayOfTheYear(cls, year):
        return cls(31, 12, year)

    def plusDay(self):
        if self.day == self.totalMonthDays() and self.month == 12:
            self.day = 1
            self.month = 1
            self.year += 1
        elif self.day == self.totalMonthDays():
            self.day = 1
            self.month += 1
        else:
            self.day += 1
    
    def minusDay(self):
        if self.day == 1 and self.month == 1:
            self.day = 31
            self.month = 12
            self.year -= 1
        elif self.day == 1:
            self.month -= 1
            self.day = self.totalMonthDays()
        else:
            self.day -= 1
    
    @classmethod
    def copy(cls):
        return cls()

    @staticmethod
    def difference(date1, date2):
        d = 0
        if date1.year < date2.year:
            print("Los días que han pasado no pueden ser negativos.")
        if date1.year > date2.year:
            y = date2.year 
            while y < date1.year:
                d += 365
                y += 1
        if date1.month > date2.month:
            m = date2.month
            while date2.month < date1.month:
                d += date2.totalMonthDays()
                date2.month += 1
            date2.month = m
        elif date2.month > date1.month:
            m = date2.month
            while date2.month > date1.month:
                d -= date2.totalMonthDays()
                date2.month -= 1
            date2.month = m
        d += date1.day - date2.day
        return d

    @classmethod
    def randomDate(cls):
        import random
        day = random.randrange(1,31)
        month = random.randrange(1,13)
        year = random.randrange(1,2021)
        date1 = cls(day, month, year)
        while date1.totalMonthDays() < day:
            day = random.randrange(1,31)
        
        return cls(day, month, year)
```

```python
#EJERCICIO 10: Implementa el método de clase .toDate() que dado un string con el formato "01 January 0001" devuelva
#el objeto fecha correspondiente a day = 1, month = 1, year = 1. Por ejemplo, si se pasa por parámetro
#05 July 1985, el método debería devolver el objeto Date con los atributos day = 5, month = 7, year =
#1985

def add_left(num, cantidad):
    """
    Función que añade tantos ceros a la 
    izquierda del número (num) para alcanzar
    la cantidad solicitada.
    No es bonita pero funciona.
    """
    if num > cantidad:
        return str(num)
    else:
        b = 10
        while num * b < cantidad:
            b *= 10
        return str(b)[1:] + str(num)
    
class Date():

    months = ["January", "February", "March", "April", "May", "Juny", "July", "August", "September", "October", "November", "December"]
    
    def __init__(self, d = 1, m = 1, y = 1):
        if type(d) == int and type(m) == int and type(y) == int:
            self.day = d
            self.month = m
            self.year = y
        else:
            print("Los datos suministrados deben ser números enteros.")
        if self.validDate() == False:
            print("¡¡¡La fecha introducida no es una fecha válida!!!")

    def __str__(self):
        return ("{} / {} / {}". format(add_left(self.day, 10), add_left(self.month, 10), add_left(self.year, 1000)))

    def isLeap(self):
        if (self.year % 4 == 0 and self.year % 100 != 0) or (self.year % 4 == 0 and self.year % 100 == 0 and self.year % 400 == 0):
            return True
        else:
            return False

    def totalMonthDays(self):
        month_days = 0
        if self.month == 1 or self.month == 3 or self.month == 5 or self.month == 7 or self.month == 8 or self.month == 10 or self.month == 12:
            month_days = 31 
        elif self.month == 4 or self.month == 6 or self.month == 9 or self.month == 11:
            month_days = 30
        elif self.month == 2 and self.isLeap() == True:
            month_days = 29
        else:
            month_days = 28
        return month_days

    def validDate(self):
        if self.totalMonthDays() >= self.day and self.month <= 12:
            return True
        else:
            return False
    
    @property
    def monthName(self):
        return months[self.month + 1]
    
    @staticmethod
    def areEqual(date1, date2):
        if date1.day == date2.day and date1.month == date2.month and date1.year == date2.year:
            return True
        else:
            return False
    
    @staticmethod
    def isLater(date1, date2):
        if date1.year > date2.year:
            return True
        elif date1.year == date2.year and date1.month > date2.month:
            return True
        elif date1.year == date2.year and date1.month == date2.month and date1.day > date2.day:
            return True
        else:
            return False
    
    @staticmethod
    def isPrevious(date1, date2):
        if date1.year < date2.year:
            return True
        elif date1.year == date2.year and date1.month < date2.month:
            return True
        elif date1.year == date2.year and date1.month == date2.month and date1.day < date2.day:
            return True
        else:
            return False

    @classmethod
    def firstDayOfTheYear(cls, year):
        return cls(1, 1, year)

    @classmethod
    def lastDayOfTheYear(cls, year):
        return cls(31, 12, year)

    def plusDay(self):
        if self.day == self.totalMonthDays() and self.month == 12:
            self.day = 1
            self.month = 1
            self.year += 1
        elif self.day == self.totalMonthDays():
            self.day = 1
            self.month += 1
        else:
            self.day += 1
    
    def minusDay(self):
        if self.day == 1 and self.month == 1:
            self.day = 31
            self.month = 12
            self.year -= 1
        elif self.day == 1:
            self.month -= 1
            self.day = self.totalMonthDays()
        else:
            self.day -= 1
    
    @classmethod
    def copy(cls):
        return cls()

    @staticmethod
    def difference(date1, date2):
        d = 0
        if date1.year < date2.year:
            print("Los días que han pasado no pueden ser negativos.")
        if date1.year > date2.year:
            y = date2.year 
            while y < date1.year:
                d += 365
                y += 1
        if date1.month > date2.month:
            m = date2.month
            while date2.month < date1.month:
                d += date2.totalMonthDays()
                date2.month += 1
            date2.month = m
        elif date2.month > date1.month:
            m = date2.month
            while date2.month > date1.month:
                d -= date2.totalMonthDays()
                date2.month -= 1
            date2.month = m
        d += date1.day - date2.day
        return d

    @classmethod
    def randomDate(cls):
        import random
        day = random.randrange(1,31)
        month = random.randrange(1,13)
        year = random.randrange(1,2021)
        date1 = cls(day, month, year)
        while date1.totalMonthDays() < day:
            day = random.randrange(1,31)
        
        return cls(day, month, year)

    @classmethod
    def toDate(cls, str_date):
        d = int(str_date[:2])
        if str_date[3:-5] in months:
            m = months.index(str_date[3:-5]) + 1
        else:
            print("Mes mal escrito")
            print(str_date[:2], str_date[3:-5], str_date[-4:])
            return
        y = int(str_date[-4:])

        return cls(d, m, y)
```
