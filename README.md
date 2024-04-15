# Lab_3_Robotica

# Integrantes: 
-Joyner Stiven Caballero Abril.
-Juan Felipe Triana

# Descripcion:

El Laboratorio No. 3 de Robótica introduce al sistema operativo robótico ROS (Robot Operating System). Utilizando Ubuntu y MATLAB, se aprenden los conceptos básicos de ROS, se realizan conexiones entre nodos de ROS y MATLAB, y se manipulan motores Dynamixel. Además, se desarrollan habilidades en Python para controlar una tortuga virtual en el entorno turtlesim usando comandos de teclado. Este laboratorio combina teoría y práctica para reforzar la comprensión y aplicación de sistemas robóticos complejos en un contexto real.

# Objetivos:

Escribir un código que permita operar una tortuga del paquete turtlesim con el teclado, cumpliendo con las siguientes especificaciones:
• Movimiento hacia adelante y hacia atrás con las teclas W y S.
• Giros en sentido horario y antihorario con las teclas D y A.
• Retornar a la posición y orientación centrales con la tecla R.
• Giro de 180° con la tecla ESPACIO.

# Desarrollo:

# Comunicacion con matlab: 

Inicialmente, se establece la conexión con Matlab utilizando el código que se proporciona en la guía. A través de este proceso, se consigue controlar el movimiento de la tortuga, que responde cada vez que se ejecuta la tercera sección del script.

![image](https://github.com/JoyS06/Lab_3_Robotica/assets/105253521/e476beb0-fa7d-4a4c-8d83-86a42971339f)

El siguiente paso es escribir un código que permita operar una tortuga del paquete turtlesim con el teclado, cumpliendo con las siguientes especificaciones anteriormente descritas. 

# Comunicación con python:

La primera sección del código fue adaptada del ejemplo proporcionado en la guía, que a su vez se basa en el recurso disponible en el sitio web "Python For Fun: Get Key Press in Python". Este recurso se puede consultar directamente en http://python4fun.blogspot.com/2008/06/get-key-press-in-python.html. 

Este código incorpora una función diseñada para capturar las teclas presionadas en el sistema operativo Linux. Esta función se utiliza en lugar del objeto Keyboard común, que presenta incompatibilidades con este sistema operativo. Esta alternativa asegura una interacción fluida y efectiva sin los contratiempos que suele presentar el objeto Keyboard estándar en Linux.

![image](https://github.com/JoyS06/Lab_3_Robotica/assets/105253521/3c15d001-25bb-4482-bb2e-9f64983b1f9a)

Para mover la tortuga en el simulador de ROS, se ha implementado una función que lee las teclas presionadas por el usuario y envía comandos de velocidad al tópico cmd_vel. Además, se han creado dos objetos de tipo ServiceProxy que se conectan con los servicios TeleportAbsolute y TeleportRelative, permitiendo cambiar la posición y la orientación de la tortuga respectivamente. La función principal se encarga de inicializar el nodo de ROS y llamar a la función que detecta las teclas del teclado, proporcionando una interacción fluida y efectiva en el control de la simulación.

![image](https://github.com/JoyS06/Lab_3_Robotica/assets/105253521/6b59f843-d2b1-400f-9bba-21834545574f)

Dentro de un bucle while que se mantiene activo mientras ROS esté en funcionamiento, se ha configurado una función que captura el valor actual de la tecla presionada, representándolo como un número binario de 8 bits. Para asegurar que las interacciones anteriores no influyan en el comportamiento actual, se reinician los valores del mensaje a cero al inicio de cada iteración. Dependiendo de la tecla presionada, se ajusta la velocidad: si es 'w' o 's', la velocidad en el eje X se modifica a 1 o -1 respectivamente; si es 'a' o 'd', se altera la velocidad angular en el eje Z a 1 o -1. Además, si se presionan las teclas 'r' o la barra espaciadora (' '), se ejecuta el ServiceProxy establecido previamente: 'r' reinicia la posición de la tortuga, mientras que la barra espaciadora aplica una rotación relativa de pi.

![image](https://github.com/JoyS06/Lab_3_Robotica/assets/105253521/91a40aaf-b391-4edc-963a-9e51ecb18211)

La función principal, main, está encapsulada dentro de un bloque if que verifica si el script se ejecuta como programa principal. Esto se verifica mediante la condición if __name__ == '__main__'. Adicionalmente, el bloque main se encuentra dentro de una estructura try-except para manejar excepciones de manera efectiva. Esto asegura que cualquier error que ocurra durante la ejecución del programa, como interrupciones del teclado o errores en la conexión con ROS, se capture y se maneje adecuadamente.

# Resultados: 

A continuacion podemos ver el funcionamiento del codigo: 

![image](https://github.com/JoyS06/Lab_3_Robotica/assets/105253521/9fe424d8-3e07-4a12-a85d-c39f8be40fd9)

# Analisis:

- La utilización de las funciones de catkin, como catkin_make, requiere la instalación previa del paquete catkin dado que no es parte del conjunto de herramientas que se instalan por defecto con ROS. Este paquete se puede instalar de manera adicional para permitir la compilación y gestión de los paquetes de ROS dentro del entorno de desarrollo.

- Antes de poder ejecutar el script de Python MyTeleopKey, es necesario realizar una compilación con catkin build para asegurar que todos los archivos necesarios estén actualizados y cargados correctamente en el directorio creado por catkin_make. Sin esta compilación, el sistema podría no reconocer o ejecutar correctamente el script.

- Para establecer una conexión con MATLAB, especialmente si se opera desde una máquina virtual, puede ser útil implementar una comunicación por SSH. Es crucial verificar que la máquina virtual esté configurada para permitir la comunicación a través de este protocolo, lo cual facilitaría la integración y la transferencia de datos entre ROS y MATLAB.

- Adicionalmente, al trabajar con la simulación en turtlesim y el control de la tortuga mediante teclas, se evidencia la importancia de gestionar correctamente los mensajes y servicios de ROS. La correcta configuración y uso de ServiceProxy para los servicios de teleportación demuestra cómo ROS permite interactuar de forma avanzada con entidades simuladas

# Conclusiones:

- Integración efectiva de herramientas: Este laboratorio demostró la efectividad de integrar múltiples plataformas y herramientas, como ROS, MATLAB, y Python, en un entorno de desarrollo unificado. La capacidad para manejar estas herramientas en conjunto permite abordar problemas complejos de robótica de manera más eficiente y con mayor control sobre los componentes simulados.

- Desarrollo de habilidades prácticas: La experiencia práctica ganada al manipular la simulación de turtlesim a través de comandos específicos y la programación de funciones en Python y MATLAB ha reforzado las competencias técnicas necesarias para operar y desarrollar soluciones en el ámbito de la robótica. Este tipo de habilidades son fundamentales en el campo de la ingeniería mecatrónica.

- Comprensión profunda de ROS: La implementación de nodos, la gestión de publicadores y suscriptores, y la utilización de servicios de ROS como TeleportAbsolute y TeleportRelative proporcionaron un conocimiento detallado de cómo ROS maneja la comunicación entre procesos y la interacción con entidades robóticas. Este conocimiento es crucial para cualquier proyecto futuro que involucre sistemas robóticos avanzados.
