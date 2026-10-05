# Spec viva: cuentas y acceso

## Purpose

Permitir que una persona cree una cuenta, inicie y cierre sesión y vea su perfil, tanto a través de la API como desde las pantallas de acceso. Describe lo que el sistema hace hoy, no lo que debería hacer.

## Requirements

### Requirement: Registro de cuenta

El sistema SHALL crear una cuenta con `POST /api/v1/auth/signup` y devolver, envueltos en `data`, el usuario creado y un token de acceso, de modo que quien se registra queda con sesión iniciada.

#### Scenario: Registro correcto

- **WHEN** se envía nombre, un email válido y no registrado, una contraseña de entre 8 y 32 caracteres y una confirmación idéntica
- **THEN** la respuesta es satisfactoria y contiene `data.user` (con `id`, `fullName`, `email`, `createdAt`, `updatedAt` e `initials`) y `data.token`, y la respuesta no incluye la contraseña

### Requirement: Validación del email en el registro

El sistema SHALL rechazar con 422 un registro cuyo email no tenga formato de email, supere 254 caracteres, falte o ya pertenezca a otra cuenta.

#### Scenario: Email ya registrado

- **WHEN** se envía un registro con un email que ya tiene una cuenta, escrito exactamente igual
- **THEN** la respuesta es 422 con un error sobre el campo `email` y no se crea ninguna cuenta nueva

#### Scenario: Email mal formado

- **WHEN** se envía un registro cuyo email es `abc`
- **THEN** la respuesta es 422 con un error sobre el campo `email`

### Requirement: Validación de la contraseña en el registro

El sistema SHALL exigir en el registro una contraseña de entre 8 y 32 caracteres y una confirmación de la contraseña con ese mismo rango y con el mismo valor.

#### Scenario: Contraseña demasiado corta

- **WHEN** se envía un registro con una contraseña de 7 caracteres
- **THEN** la respuesta es 422 con un error sobre el campo de la contraseña

#### Scenario: Confirmación distinta

- **WHEN** se envía un registro cuya confirmación no coincide con la contraseña
- **THEN** la respuesta es 422 con un error sobre el campo de la confirmación

### Requirement: Nombre opcional pero presente en la petición

El sistema SHALL aceptar el nombre completo como texto o como `null` en el registro, y tratar la cadena vacía como `null`.

#### Scenario: Sin nombre

- **WHEN** se envía un registro válido con el nombre a `null` o a cadena vacía
- **THEN** la cuenta se crea y el usuario devuelto tiene `fullName` a `null`

#### Scenario: Clave del nombre ausente

- **WHEN** se envía un registro válido en el que la clave del nombre no aparece en el cuerpo
- **THEN** la respuesta es 422 con un error sobre el campo del nombre

### Requirement: Inicio de sesión

El sistema SHALL iniciar sesión con `POST /api/v1/auth/login` y devolver, envueltos en `data`, el usuario y un token nuevo.

#### Scenario: Credenciales correctas

- **WHEN** se envía el email y la contraseña de una cuenta existente
- **THEN** la respuesta es satisfactoria y contiene `data.user` y un `data.token` nuevo, distinto de los emitidos antes

### Requirement: Rechazo de credenciales incorrectas

El sistema SHALL responder 400, sin indicar qué campo falla, cuando el email no existe o la contraseña no corresponde a la cuenta.

#### Scenario: Contraseña equivocada

- **WHEN** se envía el email de una cuenta existente con una contraseña que no es la suya
- **THEN** la respuesta es 400 y no se emite ningún token

#### Scenario: Email desconocido

- **WHEN** se envía un email sin cuenta
- **THEN** la respuesta es 400 con el mismo tipo de error que con una contraseña equivocada

### Requirement: Validación de forma en el inicio de sesión

El sistema SHALL exigir en el inicio de sesión un email con formato válido y una contraseña no vacía, sin aplicar límites de longitud a la contraseña.

#### Scenario: Faltan datos

- **WHEN** se envía un inicio de sesión sin contraseña o con la contraseña vacía
- **THEN** la respuesta es 422 con un error sobre el campo de la contraseña

### Requirement: Consulta del perfil

El sistema SHALL devolver con `GET /api/v1/account/profile` el usuario de la sesión, y SHALL responder 401 si la petición no lleva un token válido en la cabecera `Authorization: Bearer`.

#### Scenario: Con sesión

- **WHEN** se pide el perfil con el token obtenido al registrarse o iniciar sesión
- **THEN** la respuesta contiene en `data` el id, el nombre, el email, las fechas de creación y actualización y las iniciales, sin la contraseña

#### Scenario: Sin sesión

- **WHEN** se pide el perfil sin token, con un token inventado o con un token ya revocado
- **THEN** la respuesta es 401

### Requirement: Cierre de sesión en la API

El sistema SHALL revocar, con `POST /api/v1/account/logout`, únicamente el token con el que se hace la petición, y SHALL responder 401 si no hay sesión.

#### Scenario: Cierre correcto

- **WHEN** se llama al cierre de sesión con un token válido
- **THEN** la respuesta es un mensaje de éxito sin el envoltorio `data`, y desde ese momento ese token recibe 401 en el perfil

#### Scenario: Otras sesiones de la misma cuenta

- **WHEN** una cuenta tiene dos tokens y se cierra la sesión con uno de ellos
- **THEN** el otro token sigue siendo válido

### Requirement: Duración de los tokens

El sistema SHALL mantener válido un token hasta que se revoque, sin que caduque por el paso del tiempo.

#### Scenario: Token antiguo

- **WHEN** se usa un token emitido hace mucho tiempo y nunca revocado
- **THEN** la petición se acepta

### Requirement: Respuestas siempre en JSON

El sistema SHALL responder en JSON a todas las peticiones, incluidos los errores, aunque la petición pida otro formato.

#### Scenario: Petición que pide HTML

- **WHEN** se hace una petición con `Accept: text/html` a una ruta protegida sin token
- **THEN** el cuerpo de la respuesta de error es JSON

### Requirement: Iniciales del usuario

El sistema SHALL calcular las iniciales a partir del nombre si existe y, si no, del email: las dos primeras iniciales de las dos primeras palabras separadas por un espacio, o las dos primeras letras si solo hay una palabra, en mayúsculas.

#### Scenario: Nombre de varias palabras

- **WHEN** el usuario se llama «Ada Byron Lovelace»
- **THEN** sus iniciales son `AB`

#### Scenario: Sin nombre

- **WHEN** el usuario no tiene nombre y su email es `grace@correo.com`
- **THEN** sus iniciales son `GR`

### Requirement: Pantalla de registro

El sistema SHALL ofrecer en `/register`, a quien no tiene sesión, un formulario con nombre completo (marcado como opcional), email, contraseña (con la pista «Entre 8 y 32 caracteres.») y repetición de la contraseña, y un enlace a «Inicia sesión».

#### Scenario: Registro desde la pantalla

- **WHEN** una persona sin sesión rellena el formulario con datos válidos y pulsa «Crear cuenta»
- **THEN** el botón muestra «Creando cuenta…» y queda deshabilitado mientras dura el envío, y al terminar la persona queda con sesión iniciada y ve su perfil

### Requirement: Contraseñas distintas detectadas antes de enviar

El sistema SHALL, al pulsar «Crear cuenta» con contraseña y repetición distintas, mostrar bajo la repetición «Las contraseñas no coinciden.» sin enviar nada al servidor.

#### Scenario: Repetición distinta

- **WHEN** la persona escribe contraseñas distintas y pulsa «Crear cuenta»
- **THEN** aparece el mensaje bajo la repetición y no se hace ninguna petición

### Requirement: Nombre vacío en la pantalla de registro

El sistema SHALL enviar el nombre sin espacios sobrantes en los extremos, y como `null` si queda vacío.

#### Scenario: Nombre solo con espacios

- **WHEN** la persona deja el nombre con solo espacios y registra la cuenta
- **THEN** el perfil muestra «Sin nombre»

### Requirement: Errores del servidor en las pantallas de acceso

El sistema SHALL mostrar en castellano los errores del servidor: bajo su campo cuando el campo está en pantalla y, si no, en un aviso general encima del formulario.

#### Scenario: Email ya registrado

- **WHEN** la persona se registra con un email ya usado
- **THEN** bajo el email aparece «Ese email ya está registrado. Inicia sesión en su lugar.»

#### Scenario: Servidor inaccesible

- **WHEN** la persona envía el formulario y no hay conexión con el servidor
- **THEN** el aviso general dice «No se pudo conectar con el servidor. Comprueba que el backend está arrancado.»

#### Scenario: Error inesperado del servidor

- **WHEN** el servidor responde con un error que no es de validación ni de credenciales
- **THEN** el aviso general dice «Algo ha ido mal en el servidor. Inténtalo de nuevo en un momento.»

### Requirement: Pantalla de inicio de sesión

El sistema SHALL ofrecer en `/login`, a quien no tiene sesión, un formulario con email y contraseña, un botón «Entrar» y un enlace «Crea una» hacia el registro.

#### Scenario: Inicio correcto

- **WHEN** la persona introduce credenciales correctas y pulsa «Entrar»
- **THEN** el botón muestra «Entrando…» y queda deshabilitado durante el envío, y al terminar ve su perfil

#### Scenario: Credenciales incorrectas

- **WHEN** la persona introduce credenciales que el servidor rechaza
- **THEN** un aviso general dice «El email o la contraseña no son correctos.» y la persona sigue en la pantalla

#### Scenario: Campos vacíos

- **WHEN** la persona pulsa «Entrar» con el email vacío
- **THEN** bajo el email aparece «Falta rellenar el email.» y el navegador no muestra su propia validación

### Requirement: Pantalla de perfil

El sistema SHALL mostrar en `/profile` las iniciales, el nombre (o «Sin nombre»), el email y la fecha de alta como «Miembro desde» en formato largo en español.

#### Scenario: Perfil de usuario con nombre

- **WHEN** una persona con sesión y nombre abre su perfil
- **THEN** ve sus iniciales, su nombre, su email y su fecha de alta, por ejemplo «4 de octubre de 2026»

### Requirement: Cierre de sesión desde la pantalla

El sistema SHALL, al pulsar «Cerrar sesión», dejar a la persona sin sesión y llevarla al inicio de sesión de inmediato, aunque el servidor no responda o rechace la petición.

#### Scenario: Cierre con el servidor caído

- **WHEN** la persona pulsa «Cerrar sesión» y el servidor no responde
- **THEN** el botón muestra «Cerrando sesión…», la persona llega a la pantalla de inicio de sesión y no ve ningún error

### Requirement: Rutas privadas

El sistema SHALL llevar a `/login` a quien no tenga sesión y pida el perfil, y SHALL mostrar una pantalla de carga, sin redirigir, mientras se comprueba una sesión guardada.

#### Scenario: Perfil sin sesión

- **WHEN** una persona sin sesión abre `/profile`
- **THEN** acaba en `/login`

### Requirement: Rutas solo para anónimos

El sistema SHALL llevar a `/profile` a quien ya tenga sesión y abra `/login` o `/register`.

#### Scenario: Login con sesión

- **WHEN** una persona con sesión abre `/login`
- **THEN** acaba en `/profile`

### Requirement: Rutas desconocidas

El sistema SHALL llevar cualquier dirección desconocida a `/profile`, y de ahí a `/login` si no hay sesión.

#### Scenario: Dirección inexistente

- **WHEN** una persona sin sesión abre `/cualquier-cosa`
- **THEN** acaba en `/login`

### Requirement: La sesión sobrevive a la recarga

El sistema SHALL conservar la sesión en el navegador entre recargas y SHALL comprobarla contra el servidor al arrancar antes de darla por válida.

#### Scenario: Recarga con sesión

- **WHEN** una persona con sesión recarga la página en su perfil
- **THEN** ve la pantalla de carga y después su perfil, sin pasar por el inicio de sesión

### Requirement: Sesión caducada o revocada

El sistema SHALL, si el servidor rechaza la sesión guardada, olvidarla, llevar a la persona al inicio de sesión y explicarle el motivo en el aviso general.

#### Scenario: Token rechazado al arrancar

- **WHEN** una persona abre la aplicación con una sesión guardada que el servidor ya no reconoce
- **THEN** llega al inicio de sesión con el aviso «Tu sesión ha caducado. Vuelve a iniciar sesión.»

### Requirement: Sesión guardada con el servidor caído

El sistema SHALL, si al arrancar no puede comprobar la sesión por un fallo de conexión o del servidor, llevar a la persona al inicio de sesión con el motivo, pero conservar la sesión guardada para poder restaurarla al recargar con el servidor de vuelta.

#### Scenario: Servidor caído al recargar

- **WHEN** una persona con sesión recarga la página mientras el servidor no responde
- **THEN** llega al inicio de sesión con un aviso, y al recargar de nuevo con el servidor activo vuelve a su perfil sin escribir sus credenciales

---

## Parte B

### 1. Requisitos escritos y comprobados

- Requisitos escritos por el agente: 25
- Requisitos comprobados por mí abriendo el código: 1

### 2. Incoherencias que aparecieron al escribirla

- Si el servidor rechaza la sesión, se olvida; si no contesta, la persona acaba igual en el inicio de sesión pero la sesión sigue guardada en el navegador. Se ve al recargar con el servidor caído, en el requisito «Sesión guardada con el servidor caído».

### 3. Lo que no supe decidir si era un bug o el contrato

- No sé si llevar al login y aun así conservar la sesión es lo que se quería, para recuperarla al recargar, o si la pantalla está diciendo que la sesión se perdió cuando en el navegador sigue ahí.

Lo único que abrí fue ese requisito: el arranque de la sesión en el frontend y el aviso de la pantalla de login. El 401 sí borra lo guardado; el fallo de conexión no. No paré el servidor para verlo.
