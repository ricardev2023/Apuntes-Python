---
description: >-
  Explicación de como establecer un modelo cliente-servidor utilizando la
  librería socket.
---

# Socket. Modelo cliente-servidor

## Explicación de la práctica

En esta práctica se van a utilizar conceptos básicos de Python así como módulos de Python preconstruidos (built-in) para desarrollar un servidor y un cliente que puedan enviar y recibir información mutuamente.

Vamos a utilizar cada uno de los siguientes módulos:

* `socket`: Es el módulo de Python encargado de gestionar las conexiones de red por el sistema socket.

{% embed url="https://docs.python.org/es/3/library/socket.html" %}

* `threading`: Es el módulo de Python encargado de gestionar la ejecución concurrente mediante hilos o threads.

{% embed url="https://docs.python.org/es/3/library/threading.html" %}

* `pickle`: Es el módulo que implementa protocolos binarios para serializar y deserializar una estructura de objetos Python. _«Pickling»_ es el proceso mediante el cual una jerarquía de objetos de Python se convierte en una secuencia de bytes, y el _«unpickling»_ es la operación inversa.

{% embed url="https://docs.python.org/es/3/library/pickle.html" %}

* `signal`: Este módulo proporciona mecanismos para usar gestores de señales en Python. Con él podemos controlar la respuesta ante determinados eventos como, por ejemplo, un Keyboard Interrupt.

{% embed url="https://docs.python.org/es/3/library/signal.html" %}

* `sys`: Este módulo provee acceso a algunas variables usadas o mantenidas por el intérprete y a funciones que interactúan fuertemente con el intérprete. Siempre está disponible.

{% embed url="https://docs.python.org/es/3/library/sys.html" %}

* `time`: Este módulo proporciona varias funciones relacionadas con el tiempo. Para la funcionalidad relacionada, consulte también los módulos [`datetime`](https://docs.python.org/es/3/library/datetime.html#module-datetime) y [`calendar`](https://docs.python.org/es/3/library/calendar.html#module-calendar).

{% embed url="https://docs.python.org/es/3/library/time.html" %}

## Modelo Cliente-Servidor

{% embed url="https://blog.infranetworking.com/modelo-cliente-servidor" %}
ampliar información
{% endembed %}

La **arquitectura cliente servidor** tiene dos partes claramente diferenciadas, por un lado la parte del servidor y por otro la parte de cliente o grupo de clientes.&#x20;

En esta arquitectura **el cliente suele ser estaciones de trabajo** que solicitan varios servicios al servidor, mientras que **un servidor es una máquina que actúa como depósito de datos** y funciona como un sistema gestor de base de datos, este **se encarga de dar la respuesta demandada por el cliente**.

![Modelo cliente-servidor](<../.gitbook/assets/image (3).png>)

Para entender este modelo vamos a nombrar y definir a continuación algunos conceptos básicos que lo conforman.

* **Red**: Una red es un conjunto de clientes, servidores y base de datos unidos de una manera física o no física en el que existen protocolos de transmisión de información establecidos.
* **Cliente**: El concepto de cliente hace referencia a un demandante de servicios, este cliente puede ser un ordenador como también una aplicación de informática, la cual requiere información proveniente de la red para funcionar.
* **Servidor**: Un servidor hace referencia a un proveedor de servicios, este servidor a su vez puede ser un ordenador o una aplicación informática la cual envía información a los demás agentes de la red.
* **Protocolo**: Un protocolo es un conjunto de normas o reglas y pasos establecidos de manera clara y concreta sobre el flujo de información en una red estructurada.
* **Servicios**: Un servicio es un conjunto de información que busca responder las necesidades de un cliente, donde esta información pueden ser mail, música, mensajes simples entre software, videos, etc.
* **Base de datos**: Son bancos de información ordenada, categorizada y clasificada que forman parte de la red, que son sitios de almacenaje para la utilización de los servidores y también directamente de los clientes.

## Desarrollo de la práctica

### Cliente-Servidor básico utilizando sockets

Para comenzar vamos a desarrollar el script básico sobre el que desarrollaremos el resto de utilidades.

#### Script servidor

```python
#importamos las librerías necesarias.
import socket
import threading
import pickle
import signal

#definir las constantes
PORT = 8080
    #para la práctica voy a utilizar varias instancias del host.
#SERVER = 192.168.0.1 #Es una posibilidad pero la de abajo es mejor.
SERVER = socket.gethostbyname(socket.gethostname()) #Automatiza obtener la host ip.
ADDR = (SERVER, PORT)

#comenzamos con el servidor:

#Esta función la tocaremos más adelante
def def_handler():
    pass
    
#Esta función la tocaremos más adelante
def handle_client():
    pass

#Función para iniciar el socket.       
def start():
    print("[STARTING] El servidor se está inicializando...")
    server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server.bind(ADDR)
    server.listen(5)
    print(f"[LISTENING] El servidor está a la escucha en {ADDR}")
    while True:
        client_socket, client_addr = server.accept()
        print(f"[CONNECTED] El servidor se ha conectado a {client_addr}")
        client_socket.send(bytes("Bienvenido al servidor!", "utf-8"))

def main():
    start()
    
#iniciamos la ejecución
if __name__ == "__main__":
    main()
```

```
#RESPUESTA

[STARTING] El servidor se está inicializando...
[LISTENING] El servidor está a la escucha en ('192.168.1.1', 8080)
[CONNECTED] El servidor se ha conectado a ('192.168.1.1', 55783)

#Continua en ejecución a la espera de más conexiones. 
```

A continuación vamos a analizar el código de la función start() paso por paso:

* `def start ()` -> Iniciamos la definición de la función start
* &#x20;`server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)` -> Es la manera de definir un objeto de la clase socket sobre el que trabajaremos. Estos objetos tienen dos parámetros obligatorios:
  * **Familia de Direcciones (Address Family)**: Identifica el formato de direcciones que se va a utilizar en el socket. Por defecto es `AF_INET` pero puede ser (los más importantes):
    * `AF_INET`: IPv4.
    * `AF_INET6`: IPv6.
    * `AF_BLUETOOTH`: Para protocolos de bluetooth.
  * **Tipo de Socket**: Identifica el tipo de transmisión de datos que se va a dar en el socket. Los más útiles parecen ser `SOCK_STREAM` y `SOCK_DGRAM`.
* `server.bind(ADDR)` -> Enlaza el socket a la dirección que debe ser una tupla `(str(IP), int(puerto))`. En el script lo teníamos ya definido en las constantes y la IP la hemos obtenido utilizando métodos de los objetos socket:
  * `socket.gethostname()`: Es un método que devuelve el nombre del host.
  * `socket.gethostbyname()`: Dado un nombre de host, devuelve la IP de dicho host.
* `server.listen(5)` -> Habilita el servidor para recibir conexiones. El parámetro es la cola de conexiones y define la cantidad de conexiones no aceptadas que permite el servidor antes de rechazar nuevas conexiones.
* `while True`: -> hace referencia a un bucle infinito que solo se para al interrumpir la ejecución del script.
* `client_socket, client_address = server.accept()` -> Esta es una condición de bloqueo. Al ejecutar esta instrucción el servidor queda a la espera de una solicitud de conexión y tras recibirla la acepta automáticamente, recibiendo dos variables:
  * `conn (client_socket`): Es un objeto socket que identifica el socket del cliente.
  * `addr (client_address)`: Es otra tupla `(str(IP), int(puerto))` con la información del cliente.
* `client_socket.send(bytes("Bienvenido al servidor", "utf-8"))` -> Envía "stream" de datos al cliente con los bytes codificados en utf-8 de la string que se muestra. Todo lo que enviemos al cliente debe ser codificado en bytes y decodificado a la llegada.

{% hint style="warning" %}
**IMPORTANTE**

Para enviar un "stream" de bytes al cliente con el método `socket.send()`, llamamos al socket del cliente que nos ha devuelto el método `socket.accept()`. Esto se debe a que el método `socket.send()` se define como "mandar datos AL socket".

Si lo intentamos hacer llamando a nuestro socket de salida, obtendremos una excepción lógica.
{% endhint %}

#### Script cliente

```python
#importamos las librerías necesarias.
import socket
import threading
import pickle
import signal

#definir las constantes
PORT = 8080
    #para la práctica voy a utilizar varias instancias del host.
#SERVER = 192.168.0.1 #Es una posibilidad pero la de abajo es mejor.
SERVER = socket.gethostbyname(socket.gethostname()) #Automatiza obtener la host ip.
ADDR = (SERVER, PORT)

#comenzamos con el cliente:

#Esta función la tocaremos más adelante
def def_handler():
    pass
    
def connect():
    print("[CONNECTING] cliente conectando al servidor...")
    client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    client.connect(ADDR)
    print(f"[CONNECTED] cliente conectado al servidor en {ADDR}")
    msg = client.recv(1024)
    print("[RECEIVING] recibiendo mensaje del servidor")
    print("[RECEIVED] ", msg.decode("utf-8"))
    client.close()
    
def main():
    connect()

#iniciamos la ejecución
if __name__ == "__main__":
    main()
```

```
#RESPUESTA

[CONNECTING] cliente conectando al servidor...
[CONNECTED] cliente conectado al servidor en ('192.168.1.1', 8080)
[RECEIVING] recibiendo mensaje del servidor
[RECEIVED]  Bienvenido al servidor!
```

A continuación vamos a analizar el código de la función connect() paso por paso:

* `client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)` -> De la misma manera que en el servidor, es necesario definir un objeto de la clase socket para el cliente.
* `client.connect(ADDR)` -> Conecta el socket con un socket remoto en la dirección marcada. Recordar que ADDR es una tupla de la forma: `(str(IP), int(puerto))`
* `msg = client.recv(1024)` -> introduce en la variable `msg` un "stream" de bytes recibido del socket remoto con una longitud máxima de mensaje de 1024 bytes.
* print("\[RECEIVED] ", msg.decode("utf-8")) ->  Descodificamos los bytes de `msg` para obtener la información de origen.
* client.close() -> Para evitar conflictos en el futuro, es importante cerrar la conexión antes de finalizar la ejecución.

### Incluimos Headers

Hasta ahora todo funciona perfectamente pero; ¿Qué pasa si queremos enviar un mensaje más largo que 1024 bytes?

Para evitar este problema vamos a recurrir a la técnica de los **Headers**. Esto es, básicamente, añadir a todos los mensajes que se envían una cabecera donde (para hacerlo lo más sencillo posible) veremos la longitud del mensaje a recibir en bytes.

#### Explicación del Header

```python
#Extracto de código con el desarrollo de los headers.

#SERVIDOR
HEADERLENGTH = 10
def send(msg, client_socket):
    message = msg.encode("utf-8")
    msg_length = len(message)
    #print("[msg_length]", msg_length)
    send_length = str(msg_length).encode("utf-8")
    #print("[send_length]", send_length)
    send_length += b" " * (HEADERLENGTH - len(send_length))
    client_socket.send(send_length)
    #print("[send_length]", send_length)
    client_socket.send(message)
    #print("[message]", message)

#CLIENTE
HEADERLENGTH = 10

def receive(client):
    msg_length = client.recv(HEADERLENGTH).decode("utf-8")
    msg_length = int(msg_length)
    print(f"[HEADER] {msg_length}")
    msg = client.recv(msg_length).decode("utf-8")	
    print(f"[RECEIVED] {msg}") 
```

Empezando por el Servidor:

* `HEADERLENGTH = 10` -> Es una constante que marca la longitud de nuestro Header. Notese que como el Header solo contiene la cantidad de caracteres que vamos a enviar, con un HEADERLENGTH de 10, podemos abarcar hasta 9.999.999.999 bytes por mensaje.
* `def send(msg, client_socket)` -> Definimos una nueva función que automatice el envío de mensajes con Header. Para ello necesitamos pasarle como argumentos el mensaje a enviar y el socket del cliente.
* `message = msg.encode("utf-8")` -> Con esta línea ya tenemos el mensaje en formato bytes.
* `msg_length = len(message)` -> Ahora ya sabemos cuantos bytes tiene el mensaje a enviar.
* `send_length = str(msg_length).encode("utf-8")` -> Ahora como queremos enviar la longitud, lo pasamos a string y lo codificamos en bytes.
* `send_length += b" " * (HEADERLENGTH - len(send_length))` -> Hay que colocar los números a la izquierda del Header que tiene 10 bytes de capacidad y para ello llenamos de espacios (b" " es la representación en bytes del carácter espacio) lo que queda de Header. En este caso, tenemos: `b" " * 10- len(23)` por lo tanto se añadirán 8 espacios.
* A partir de aquí solo queda mandar primero el Header y despues el mensaje para que el cliente lo reciba correctamente.

Ahora el cliente:

* `HEADERLENGTH = 10` -> Igual que en el servidor, es necesario que lo tengan igual.
* `msg_length = client.recv(HEADERLENGTH).decode("utf-8)` -> El cliente recibe el Header y lo decodifica. (Recordemos que era un string codificado en bytes).
* `msg_length = int(msg_length)` -> Ahora lo transformamos a Integer.
* `msg = client.recv(msg_lenght).decode("utf-8")` -> Con la longitud anterior ya sabemos cuanto tenemos que esperar del mensaje final.

#### Script Servidor

```python
#importamos las librerías necesarias.
import socket
import threading
import pickle
import signal

#definir las constantes
PORT = 8080
    #para la práctica voy a utilizar varias instancias del host.
#SERVER = 192.168.0.1 #Es una posibilidad pero la de abajo es mejor.
SERVER = socket.gethostbyname(socket.gethostname()) #Automatiza obtener la host ip.
ADDR = (SERVER, PORT)
HEADERLENGTH = 10

#comenzamos con el servidor:
#Esta función la tocaremos más adelante
def def_handler():
    pass
    
#Esta función la tocaremos más adelante
def handle_client():
    pass

#Función para iniciar el socket.       
def start():
    print("[STARTING] El servidor se está inicializando...")
    server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server.bind(ADDR)
    server.listen(5)
    print(f"[LISTENING] El servidor está a la escucha en {ADDR}")
    while True:
        client_socket, client_addr = server.accept()
        print(f"[CONNECTED] El servidor se ha conectado a {client_addr}")
        msg = "Bienvenido al servidor!"
        send(msg, client_socket)
        #client_socket.send(bytes("Bienvenido al servidor!", "utf-8"))

def send(msg, client_socket):
    message = msg.encode("UTF-8")
    msg_length = len(message)
    #print("[msg_length]", msg_length)
    send_length = str(msg_length).encode("utf-8")
    #print("[send_length]", send_length)
    send_length += b" " * (HEADERLENGTH - len(send_length))
    client_socket.send(send_length)
    #print("[send_length]", send_length)
    client_socket.send(message)
    #print("[message]", message)

def main():
    start()
    
#iniciamos la ejecución
if __name__ == "__main__":
    main()
```

```
#RESPUESTA

[STARTING] El servidor se está inicializando...
[LISTENING] El servidor está a la escucha en ('192.168.1.1', 8080)
[CONNECTED] El servidor se ha conectado a ('192.168.1.1', 52286)
```

#### Script Cliente

```python
#importamos las librerías necesarias.
import socket
import threading
import pickle
import signal

#definir las constantes
PORT = 8080
    #para la práctica voy a utilizar varias instancias del host.
#SERVER = 192.168.0.1 #Es una posibilidad pero la de abajo es mejor.
SERVER = socket.gethostbyname(socket.gethostname()) #Automatiza obtener la host ip.
ADDR = (SERVER, PORT)
HEADERLENGTH = 10

#comenzamos con el cliente:

#Esta función la tocaremos más adelante
def def_handler():
    pass
    
def connect():
    print("[CONNECTING] cliente conectando al servidor...")
    client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    client.connect(ADDR)
    print(f"[CONNECTED] cliente conectado al servidor en {ADDR}")
    receive(client)
    client.close()
    
def receive(client):
    msg_length = client.recv(HEADERLENGTH).decode("utf-8")
    #print(msg_length)
    msg_length = int(msg_length)
    print(f"[HEADER] {msg_length}")
    msg = client.recv(msg_length).decode("utf-8")	
    print(f"[RECEIVED] {msg}")
    
def main():
    connect()

if __name__ == "__main__":
    main()
```

```
#RESPUESTA

[CONNECTING] cliente conectando al servidor...
[CONNECTED] cliente conectado al servidor en ('192.168.1.1', 8080)
23
[HEADER] 23
[RECEIVED] Bienvenido al servidor!
```

### Mandamos objetos

Hasta ahora nuestro Modelo cliente-servidor funciona a la perfección pero solo es capaz de enviar y recibir streams de bytes. Esto complica que se puedan enviar objetos de Python por este medio. Sin embargo, con el módulo `pickle` podemos hacerlo muy facilmente:

#### Módulo pickle

El modulo `pickle` implementa protocolos binarios para serializar y deserializar una estructura de objetos Python. _**«Pickling»**_ es el proceso mediante el cual una jerarquía de objetos de Python se convierte en una secuencia de bytes, y el _**«unpickling»**_ es la operación inversa, mediante la cual una secuencia de bytes de un archivo binario (binary file) ó un objeto tipo binario (bytes-like object) es convertido nuevamente en una jerarquía de objetos.

Este mismo proceso se podría realizar serializando los objetos en un documento JSON pero es más complejo de realizar. Sin embargo JSON tiene una serie de ventajas sobre pickle, principalmente la interoperabilidad y la característica de ser legible por humanos. Además es más seguro.

{% hint style="success" %}
Para obtener más información sobre serialización y deserialización en JSON pueden visitar:

[**https://docs.python.org/es/3/library/json.html#module-json**](https://docs.python.org/es/3/library/json.html#module-json)****
{% endhint %}

El uso básico del módulo pickle es muy sencillo, solo necesitamos pickle.dumps(msg) para serializar el mensaje y pickle.loads(msg) para deserializarlo y volver a tener el objeto de python que habíamos enviado.

Por tanto, vamos a tener que realizar muy pocos cambios en nuestros scripts:

#### Script Servidor

Vamos a cambiar el mensaje por un diccionario de Python para demostrar que se envía y mantiene sus propiedades.

```python
#importamos las librerías necesarias.
import socket
import threading
import pickle
import signal

#definir las constantes
PORT = 8080
    #para la práctica voy a utilizar varias instancias del host.
#SERVER = 192.168.0.1 #Es una posibilidad pero la de abajo es mejor.
SERVER = socket.gethostbyname(socket.gethostname()) #Automatiza obtener la host ip.
ADDR = (SERVER, PORT)
MSG = {1: "Hola", 2: "Bienvenido", 3: "Al", 4: "Servidor"}
HEADERLENGTH = 10

#comenzamos con el servidor:
#Esta función la tocaremos más adelante
def def_handler():
    pass
    
#Esta función la tocaremos más adelante
def handle_client():
    pass

#Función para iniciar el socket.       
def start():
    print("[STARTING] El servidor se está inicializando...")
    server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server.bind(ADDR)
    server.listen(5)
    print(f"[LISTENING] El servidor está a la escucha en {ADDR}")
    while True:
        client_socket, client_addr = server.accept()
        print(f"[CONNECTED] El servidor se ha conectado a {client_addr}")
        send(MSG, client_socket)
        #client_socket.send(bytes("Bienvenido al servidor!", "utf-8"))

def send(msg, client_socket):
    #NUEVO
    print("[TYPE]", type(msg))
    print("[MESSAGE]", msg)
    message = pickle.dumps(msg)
    print("[TYPE PICKLED]", type(message))
    print("[MESSAGE PICKLED]", message)
    #NO CAMBIA
    msg_length = len(message)
    #print("[msg_length]", msg_length)
    send_length = str(msg_length).encode("utf-8")
    #print("[send_length]", send_length)
    send_length += b" " * (HEADERLENGTH - len(send_length))
    client_socket.send(send_length)
    #print("[send_length]", send_length)
    client_socket.send(message)
    #print("[message]", message)

def main():
    start()
    
#iniciamos la ejecución
if __name__ == "__main__":
    main()
```

```
[STARTING] El servidor se está inicializando...
[LISTENING] El servidor está a la escucha en ('192.168.1.1', 8080)
[CONNECTED] El servidor se ha conectado a ('192.168.1.1', 62945)
[TYPE] <class 'dict'>
[MESSAGE] {1: 'Hola', 2: 'Bienvenido', 3: 'Al', 4: 'Servidor'}
[TYPE PICKLED] <class 'bytes'>
[MESSAGE PICKLED] b'\x80\x04\x951\x00\x00\x00\x00\x00\x00\x00}\x94(K\x01\x8c\x04Hola\x94K\x02\x8c\nBienvenido\x94K\x03\x8c\x02Al\x94K\x04\x8c\x08Servidor\x94u.'
```

#### Script Cliente

```python
#importamos las librerías necesarias.
import socket
import threading
import pickle
import signal

#definir las constantes
PORT = 8080
    #para la práctica voy a utilizar varias instancias del host.
#SERVER = 192.168.0.1 #Es una posibilidad pero la de abajo es mejor.
SERVER = socket.gethostbyname(socket.gethostname()) #Automatiza obtener la host ip.
ADDR = (SERVER, PORT)
HEADERLENGTH = 10

#comenzamos con el cliente:

#Esta función la tocaremos más adelante
def def_handler():
    pass
    
def connect():
    print("[CONNECTING] cliente conectando al servidor...")
    client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    client.connect(ADDR)
    print(f"[CONNECTED] cliente conectado al servidor en {ADDR}")
    receive(client)
    client.close()
    
def receive(client):
    #NO CAMBIA
    msg_length = client.recv(HEADERLENGTH).decode("utf-8")
    #print(msg_length)
    msg_length = int(msg_length)
    print(f"[HEADER] {msg_length}")
    #NUEVO
    msg = client.recv(msg_length)	
    print(f"[RECEIVED PICKLED] {msg}")
    msg = pickle.loads(msg)
    print(f"[RECEIVED UNPICKLED] {msg}")
    
def main():
    connect()

if __name__ == "__main__":
    main()
```

```
[CONNECTING] cliente conectando al servidor...
[CONNECTED] cliente conectado al servidor en ('192.168.1.1', 8080)
[HEADER] 60
[RECEIVED PICKLED] b'\x80\x04\x951\x00\x00\x00\x00\x00\x00\x00}\x94(K\x01\x8c\x04Hola\x94K\x02\x8c\nBienvenido\x94K\x03\x8c\x02Al\x94K\x04\x8c\x08Servidor\x94u.'
[RECEIVED UNPICKLED] {1: 'Hola', 2: 'Bienvenido', 3: 'Al', 4: 'Servidor'}
```

### Trabajo concurrente

Ya podemos mandar cualquier tipo de objeto de Python pero seguimos teniendo el problema de que solo puede existir una conexión al mismo tiempo, es decir, solo puede haber un cliente conectado.

Para conseguir que varios clientes se conecten a la vez tenemos que recurrir a técnicas de trabajo concurrente. En este caso vamos a recurrir a los `Threads`.&#x20;

#### Módulo threading

Un hilo es una línea de ejecución de un proceso. Todo proceso parte inicialmente con un único hilo principal, aunque el sistema operativo ofrece llamadas al sistema que permiten al programador crear y destruir hilos. Por tanto, un proceso está compuesto por uno o más hilos.

El módulo threading proporciona una interfaz de hilado de alto nivel para Python. Aunque el concepto es muy técnico, el módulo permite a los programadores de Python trabajar con hilos de manera inmediata.

{% hint style="danger" %}
Esto solo debe hacerse en el servidor pues se entiende que en el equipo cliente no se van a ejecutar varias instancias cliente.
{% endhint %}

Para ello, vamos a crear objetos de la clase threading.Thread tal que:

`threading.Thread(group=None, target=None, name=None, args=(), kwargs={}, *, daemon=None)`_:_

* `group`: Debe ser None o dejarse en blanco. Está pensado para nuevas versiones.
* `target`: Es el objetivo invocable. Normalmente la función que gestiona el proceso individual.
* `name`: Es el nombre del hilo. Por defecto se le asigna un nombre único.
* `args`: Los argumentos que se le deben pasar al objeto invocable. Tipo Tupla.
* `kwargs`: Diccionario de argumentos de palabra clave para el objetivo invocable. por defecto {}.
* `daemon`: Si no es none, establece explícitamente que el hilo es daemon, es decir, se ejecuta en segundo plano.

Una vez hecho eso, solo tendremos que iniciar el hilo con `thread.start()`.

Por último, habrá que cerrar el proceso cuando salgamos para que los hilos mueran con el proceso.

#### Script Servidor

```python
import socket
import threading
import pickle
import signal
import sys
import time

PORT = 8080
SERVER = socket.gethostbyname(socket.gethostname()) #Automatiza obtener la host ip.
ADDR = (SERVER, PORT)
MSG = {1: "Hola", 2: "Bienvenido", 3: "Al", 4: "Servidor"}
HEADERLENGTH = 10

def def_handler():
    pass

def handle_client(client_socket, client_addr):
    print(f"[CONNECTED] El servidor se ha conectado a {client_addr}")
    send(MSG, client_socket)

#Función para iniciar el socket.       
def start(server):
    server.listen()
    print(f"[LISTENING] El servidor está a la escucha en {ADDR}")
    while True:
        client_socket, client_addr = server.accept()
        #NUEVO
        thread = threading.Thread(target=handle_client, args=(client_socket, client_addr))
        thread.start()
        print(f"[ACTIVE CONNECTIONS] {threading.active_count() -1}")

def send(msg, client_socket):
    #NUEVO para mantener la conexion viva el servidor envía el 
    #mismo mensaje cada 60 s
    while True:
        print("[TYPE]", type(msg))
        print("[MESSAGE]", msg)
        message = pickle.dumps(msg)
        print("[TYPE PICKLED]", type(message))
        print("[MESSAGE PICKLED]", message)
        #NO CAMBIA
        msg_length = len(message)
        print("[msg_length]", msg_length)
        send_length = str(msg_length).encode("utf-8")
        print("[send_length]", send_length)
        send_length += b" " * (HEADERLENGTH - len(send_length))
        client_socket.send(send_length)
        print("[send_length]", send_length)
        client_socket.send(message)
        print("[message]", message, "\n")
        time.sleep(60)

def main():
    #NUEVO
    print("[STARTING] El servidor se está inicializando...")
    server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server.bind(ADDR)
    #NO CAMBIA
    start(server)
    
#iniciamos la ejecución
if __name__ == "__main__":
    main()
```

```
[STARTING] El servidor se está inicializando...
[LISTENING] El servidor está a la escucha en ('192.168.1.1', 8080)
[CONNECTED] El servidor se ha conectado a ('192.168.1.1', 64992)
[ACTIVE CONNECTIONS] 1
[TYPE] <class 'dict'>
[MESSAGE] {1: 'Hola', 2: 'Bienvenido', 3: 'Al', 4: 'Servidor'}
[TYPE PICKLED] <class 'bytes'>
[MESSAGE PICKLED] b'\x80\x04\x951\x00\x00\x00\x00\x00\x00\x00}\x94(K\x01\x8c\x04Hola\x94K\x02\x8c\nBienvenido\x94K\x03\x8c\x02Al\x94K\x04\x8c\x08Servidor\x94u.'
[msg_length] 60
[send_length] b'60'
[send_length] b'60        '
[message] b'\x80\x04\x951\x00\x00\x00\x00\x00\x00\x00}\x94(K\x01\x8c\x04Hola\x94K\x02\x8c\nBienvenido\x94K\x03\x8c\x02Al\x94K\x04\x8c\x08Servidor\x94u.'

[CONNECTED] El servidor se ha conectado a ('192.168.1.1', 64993)
[TYPE] <class 'dict'>
[MESSAGE] {1: 'Hola', 2: 'Bienvenido', 3: 'Al', 4: 'Servidor'}
[TYPE PICKLED] <class 'bytes'>
[MESSAGE PICKLED] b'\x80\x04\x951\x00\x00\x00\x00\x00\x00\x00}\x94(K\x01\x8c\x04Hola\x94K\x02\x8c\nBienvenido\x94K\x03\x8c\x02Al\x94K\x04\x8c\x08Servidor\x94u.'
[msg_length] 60
[ACTIVE CONNECTIONS] 2
[send_length] b'60'
[send_length] b'60        '
[message] b'\x80\x04\x951\x00\x00\x00\x00\x00\x00\x00}\x94(K\x01\x8c\x04Hola\x94K\x02\x8c\nBienvenido\x94K\x03\x8c\x02Al\x94K\x04\x8c\x08Servidor\x94u.'

[CONNECTED] El servidor se ha conectado a ('192.168.1.1', 64994)
[ACTIVE CONNECTIONS] 3
[TYPE] <class 'dict'>
[MESSAGE] {1: 'Hola', 2: 'Bienvenido', 3: 'Al', 4: 'Servidor'}
[TYPE PICKLED] <class 'bytes'>
[MESSAGE PICKLED] b'\x80\x04\x951\x00\x00\x00\x00\x00\x00\x00}\x94(K\x01\x8c\x04Hola\x94K\x02\x8c\nBienvenido\x94K\x03\x8c\x02Al\x94K\x04\x8c\x08Servidor\x94u.'
[msg_length] 60
[send_length] b'60'
[send_length] b'60        '
[message] b'\x80\x04\x951\x00\x00\x00\x00\x00\x00\x00}\x94(K\x01\x8c\x04Hola\x94K\x02\x8c\nBienvenido\x94K\x03\x8c\x02Al\x94K\x04\x8c\x08Servidor\x94u.'
```

### Control + C

Como todos somos muy asiduos a utilizar Control + C para hacer break a los scripts que se estan ejecutando, vamos a utilizar el módulo `signal` para hacerlo de manera controlada.

#### signal.SIGINT()

el módulo `signal` permite definir gestores personalizados que serán ejecutados cuando una señal es recibida.

En concreto `signal.SIGINT` es el resultado de una señal `KeyboardInterrupt`. Podemos editar esta señal para que diga lo que nosotros queramos y genere una salida correcta del script. por tanto:

```python
def def_handler():
    print("\n\n[!] SALIENDO!!")
    sys.exit(-1)

signal.signal(signal.SIGINT, def_handler)
```

De esta manera ya tenemos los scripts completamente funcinales.

## RESULTADO FINAL

### SERVIDOR

```python
import socket
import threading
import pickle
import signal
import sys
import time

PORT = 8080
SERVER = socket.gethostbyname(socket.gethostname()) #Automatiza obtener la host ip.
ADDR = (SERVER, PORT)
MSG = {1: "Hola", 2: "Bienvenido", 3: "Al", 4: "Servidor"}
HEADERLENGTH = 10

def def_handler():
    print("\n\n[!] SALIENDO!!")
    sys.exit(-1)

signal.signal(signal.SIGINT, def_handler)

def handle_client(client_socket, client_addr):
    print(f"[CONNECTED] El servidor se ha conectado a {client_addr}")
    send(MSG, client_socket)

#Función para iniciar el socket.       
def start(server):
    server.listen()
    print(f"[LISTENING] El servidor está a la escucha en {ADDR}")
    while True:
        client_socket, client_addr = server.accept()
        #NUEVO
        thread = threading.Thread(target=handle_client, args=(client_socket, client_addr))
        thread.start()
        print(f"[ACTIVE CONNECTIONS] {threading.active_count() -1}")

def send(msg, client_socket):
    #NUEVO
    while True:
        print("[TYPE]", type(msg))
        print("[MESSAGE]", msg)
        message = pickle.dumps(msg)
        print("[TYPE PICKLED]", type(message))
        print("[MESSAGE PICKLED]", message)
        #NO CAMBIA
        msg_length = len(message)
        print("[msg_length]", msg_length)
        send_length = str(msg_length).encode("utf-8")
        print("[send_length]", send_length)
        send_length += b" " * (HEADERLENGTH - len(send_length))
        client_socket.send(send_length)
        print("[send_length]", send_length)
        client_socket.send(message)
        print("[message]", message, "\n")
        time.sleep(60)

def main():
    #NUEVO
    print("[STARTING] El servidor se está inicializando...")
    server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server.bind(ADDR)
    #NO CAMBIA
    start(server)
    
#iniciamos la ejecución
if __name__ == "__main__":
    main()
```

### CLIENTE

```python
import socket
import pickle
import signal
import sys

#definir las constantes
PORT = 8080
    #para la práctica voy a utilizar varias instancias del host.
#SERVER = 192.168.0.1 #Es una posibilidad pero la de abajo es mejor.
SERVER = socket.gethostbyname(socket.gethostname()) #Automatiza obtener la host ip.
ADDR = (SERVER, PORT)
HEADERLENGTH = 10

#comenzamos con el cliente:

def def_handler():
    print("\n\n[!] SALIENDO!!")
    sys.exit(-1)

signal.signal(signal.SIGINT, def_handler)
    
def connect():
    print("[CONNECTING] cliente conectando al servidor...")
    client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    client.connect(ADDR)
    print(f"[CONNECTED] cliente conectado al servidor en {ADDR}")
    receive(client)
    #client.close()
    
def receive(client):
    #NO CAMBIA
    while True:
        msg_length = client.recv(HEADERLENGTH).decode("utf-8")
        print(msg_length)
        msg_length = int(msg_length)
        print(f"[HEADER] {msg_length}")
        #NUEVO
        msg = client.recv(msg_length)	
        print(f"[RECEIVED PICKLED] {msg}")
        msg = pickle.loads(msg)
        print(f"[RECEIVED UNPICKLED] {msg}")
    
def main():
    connect()

if __name__ == "__main__":
    main()
```
