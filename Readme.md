# Pruebas de la API Urban Grocers mediante una lista de comprobación

Descripción: Este ejercicio fue mi primer acercamiento práctico a las pruebas automatizadas el objetivo del mismo es aprender a estructurar correctamente las pruebas automatizadas siguiendo las mejores prácticas. Es decir:
1. Que cada técnica debe centrarse en una única funcionalidad o aspecto.
2. Que eviten depender de datos específicos que puedan cambiar con el tiempo.
3. Que cada prueba debe de ser capaz de ejecutarse de forma independiente, sin depender del resultado de otras pruebas.

## Tabla de contenidos
- Introducción
- Requisitos previos
- Uso
- Estructura del proyecto
- Lista de comprobación
- Lista de pruebas
- Tecnologías y técnicas utilizadas

## Introducción

Este código se enfoca en realizar pruebas para el parámetro "firstName" al crear un/a usuario/a a través de una API, misma que otorga TripleTen.

Esta experiencia me permitió consolidar mis habilidades en Python, Git, Github, PyCharm.

## Requisitos previos

Se requiere la instalación de las librerías:
- selenium
- pytest

## Uso

Para correr las pruebas basta con escribir el comando 'pytest tests/' en la terminal.

## Estructura del proyecto

`configuration.py`: Contiene URL y rutas necesarias que serán utilizadas por las funciones del archivo "sender_stand_request.py".
`data.py`: Contiene los datos necesarios que serán importados por las funciones para ser utilizados en las pruebas.
`sender_stand_request.py`: Contiene la función que crea al usuario con base a los datos en "data.py" y la función que corrobora que se ha creado correctamente.
`create_user_test.py`: Contiene las funciones que actualizan los datos de "data.py", funciones que confirman que la respuesta de una prueba sea positiva o negativa (según sea el caso) y funciones que dan estructura a la suite de pruebas automatizadas (10).

## Lista de comprobación

La siguiente lista de comprobación fue en la que me he basado para crear las pruebas que se encuentran en el archivo "create_user_test.py":

### Lista de comprobación y resultados de la prueba para la API de Urban Grocers.
| No. | Descripción                                                                                                                                                               | Resultado Esperado                                                                                                                                                                                                                                 |
|-----|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1   | **El número permitido de caracteres (2)** body: {"firstName": "Aa","phone": "+1234567890","address": "123 Elm Street, Hilltop"}                                           | **1.** El código de respuesta y el estado: 201 Created **2.** El parámetro "authToken" contiene un token generado recientemente **3.** La tabla "Users" contiene valores pasados                                                                   |
| 2   | **El número permitido de caracteres (15):** body: {"firstName": "Aaaaaaaaaaaaaaa","phone": "+1234567890","address": "123 Elm Street, Hilltop"}                            | **1.** El código de respuesta y el estado: 201 Created **2.** El parámetro "authToken" contiene un token generado recientemente **3.** La tabla "Users" contiene valores pasados                                                                   |
| 3   | **El número de caracteres que es menor a la cantidad permitida (1)** body: {"firstName": "A","phone": "+1234567890","address": "123 Elm Street, Hilltop"}                 | **1.** El código de respuesta y el estado: 400 Bad Request **2.** {"code": 400, "message": "Has introducido un nombre de usuario no válido. El nombre solo puede contener letras del alfabeto latino, la longitud debe ser de 2 a 15 caracteres."} |
| 4   | **El número de caracteres que es menor a la cantidad permitida (16)** body: {"firstName": "Аааааааааааааааа","phone": "+1234567890","address": "123 Elm Street, Hilltop"} | **1.** El código de respuesta y el estado: 400 Bad Request **2.** {"code": 400, "message": "Has introducido un nombre de usuario no válido. El nombre solo puede contener letras del alfabeto latino, la longitud debe ser de 2 a 15 caracteres."} |
| 5   | **No se permiten espacios** body: {"firstName": "A Aaa","phone": "+1234567890","address": "123 Elm Street, Hilltop"}                                                      | **1.** El código de respuesta y el estado: 400 Bad Request **2.** {"code": 400, "message": "Has introducido un nombre de usuario no válido. El nombre solo puede contener letras del alfabeto latino, la longitud debe ser de 2 a 15 caracteres."} |
| 6   | **No se permiten caracteres especiales** body: {"firstName": "№%@","phone": "+1234567890","address": "123 Elm Street, Hilltop"}                                           | **1.** El código de respuesta y el estado: 400 Bad Request **2.** {"code": 400, "message": "Has introducido un nombre de usuario no válido. El nombre solo puede contener letras del alfabeto latino, la longitud debe ser de 2 a 15 caracteres."} |
| 7   | **No se permiten números** body: {"firstName": "123","phone": "+1234567890","address": "123 Elm Street, Hilltop"}                                                         | **1.** El código de respuesta y el estado: 400 Bad Request **2.** {"code": 400, "message": "Has introducido un nombre de usuario no válido. El nombre solo puede contener letras del alfabeto latino, la longitud debe ser de 2 a 15 caracteres."} |
| 8   | **El parámetro no se pasa en la solicitud** body: {"phone": "+1234567890","address": "123 Elm Street, Hilltop"}                                                           | **1.** El código de respuesta y el estado: 400 Bad Request  **2.**  {"code": 400, "message": "No se han aprobado todos los parámetros requeridos"}                                                                                                 |
| 9   | **Se ha pasado un valor de parámetro vacío** body: {"firstName": "","phone": "+1234567890","address": "123 Elm Street, Hilltop"}                                          | **1.** El código de respuesta y el estado: 400 Bad Request **2.** {"code": 400, "message": "No se han aprobado todos los parámetros requeridos"}                                                                                                   |
| 10  | **Se ha pasado otro tipo de parámetro "firstName": número** body: {"firstName": 12,"phone": "+1234567890","address": "123 Elm Street, Hilltop"}                           | **1** El código de respuesta y el estado: 400 Bad Request **2.** {"code": 400, "message": "No se han aprobado todos los parámetros requeridos"}                                                                                                    |

## Lista de pruebas

| №  | Prueba                                                                          | Descripción                                                                                                                  |
|----|---------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| 1  | **def test_create_user_2_letter_in_first_name_get_success_response():**         | Solicita la creación de un nuevo usuario/a con 2 caracteres y corrobora que la respuesta sea positiva.                       |
| 2  | **def test_create_user_15_letter_in_first_name_get_success_response():**        | Solicita la creación de un nuevo usuario/a con 15 caracteres y corrobora que la respuesta sea positiva.                      |
| 3  | **def test_create_user_1_letter_in_first_name_get_error_response():**           | Solicita la creación de un nuevo usuario/a con 1 caracteres y corrobora que la respuesta sea negativa.                       |
| 4  | **def test_create_user_16_letter_in_first_name_get_error_response():**          | Solicita la creación de un nuevo usuario/a con 16 caracteres y corrobora que la respuesta sea negativa.                      |
| 5  | **def test_create_user_has_space_in_first_name_get_error_response():**          | Solicita la creación de un nuevo usuario/a con un espacio dentro del nombre y corrobora que la respuesta sea negativa.       |
| 6  | **def test_create_user_has_special_symbol_in_first_name_get_error_response():** | Solicita la creación de un nuevo usuario/a con caracteres especiales y corrobora que la respuesta sea negativa.              |
| 7  | **def test_create_user_has_number_in_first_name_get_error_response():**         | Solicita la creación de un nuevo usuario/a con un string numérico y corrobora que la respuesta sea negativa.                 |
| 8  | **def test_create_user_no_first_name_get_error_response():**                    | Solicita la creación de un nuevo usuario/a eliminando el parámetro "firstName" y corrobora que la respuesta sea negativa.    |
| 9  | **def test_create_user_empty_first_name_get_error_response():**                 | Solicita la creación de un nuevo usuario/a dejando vacío el parámetro "firstName" y corrobora que la respuesta sea negativa. |
| 10 | **def test_create_user_number_type_first_name_get_error_response():**           | Solicita la creación de un nuevo usuario/a con caracteres numéricos y corrobora que la respuesta sea negativa.               |

## Tecnologías y técnicas utilizadas

### Tecnologías

`Python` `Git` `Github` `PyCharm`

### Técnicas

- Creación de funciones.
- Creación de asserts.
- Creación de archivos.
- Instalación de librerías.
- Importación de librerías.
- Importación de datos entre archivos.
- Depuración de código.
- Control de versiones con Git (Clonar, Fusionar, Actualización, Extracción).
- Navegación en ramificaciones Git.