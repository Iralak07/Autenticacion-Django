# Autenticacion-Django
Este repositorio explica el uso del sistema de autenticación de Django, mas especificamente el objeto User y nos limitares a explicar sus atributos y los metodos necesarios que utiliza django para autenticarse y registrarse como nuevo usuario.

La autenticación de Django proporciona autenticación y autorización juntas y generalmente se la denomina sistema de autenticación, ya que estas características están de alguna manera acopladas.

## El Objeto User

Este objeto es el núcleo del sistema de autenticación. Por lo general, representan a las personas que interactúan con su sitio y se utilizan para permitir cosas como restringir el acceso, registrar perfiles de usuario, asociar contenido con creadores, etc. 

El objeto User es una instancia de la clase User definida en el módulo django.contrib.auth.models y cuyos atributos se describen a continuacion:


      - username: 150 caracteres o menos. Los nombres de usuario pueden contener caracteres alfanuméricos, unicamente acepta caracteres de 150 o menos. Si necesitas mas                           caracteres debes personalizarlo. -

      - first_name: es una campo opcional, el atributo (blank=True), es decir puede estar este campo en blanco. 150 caracteres o menos.

      - last_name: es una campo opcional, el atributo (blank=True), es decir puede estar este campo en blanco. 150 caracteres o menos.

      -  email: es una campo opcional, el atributo (blank=True), es decir puede estar este campo en blanco. Direccion de correo electronico.

      - password: es requerido, es decir no puede enviar este campo vacio. Un hash y metadatos sobre la contraseña. (Django no almacena la contraseña sin formato). Las                 contraseñas sin formato pueden ser arbitrariamente largas y contener cualquier carácter. Consulte la documentación de contraseña .

      - groups:  Relación de muchos a muchos con grupos.

      - user_permissions:  Relación de muchos a muchos con permisos determinados. -

      - is_staff: Designa si este usuario puede acceder al sitio de administración.

      - is_active: Designa si esta cuenta de usuario debe considerarse activa. Le recomendamos que establezca esta bandera en False en lugar de eliminar cuentas; de esa                   manera, si sus aplicaciones tienen claves externas para los usuarios, las claves externas no se romperán. La razón detrás de esto es que, si tienes claves externas             que hacen referencia a la cuenta de usuario (por ejemplo, en otras tablas de tu base de datos), eliminar la cuenta podría romper esas claves externas y causar                  problemas en la integridad de los datos. Al marcar una cuenta como "desactivada", mantienes la integridad de las claves externas y evitas problemas de referencia.

           Supongamos que tienes un usuario llamado "Pepe22" que ha realizado varios comentarios en tu aplicación. Si decides eliminar la cuenta de "Pepe22" de forma                      permanente, esto podría causar problemas si la cuenta está relacionada con esos comentarios. La eliminación de la cuenta de "Pepe22" rompería las referencias de                clave externa en la tabla de comentarios, lo que podría generar errores o problemas de integridad en la base de datos.


      - is_superuser: Designa que este usuario tiene todos los permisos sin asignarlos explícitamente.


      `#` is_authenticated:  Atributo de solo lectura que es siempre True(en contraposición a AnonymousUser.is_authenticated que es siempre False). Esta es una forma de saber             si el usuario ha sido autenticado. Esto no implica ningún permiso y no verifica si el usuario está activo o tiene una sesión válida. Aunque normalmente comprobará              este atributo request.user para saber si ha sido completado por AuthenticationMiddleware(que representa al usuario que ha iniciado sesión actualmente), debe saber               que este atributo es True para cualquier instancia de User.
            
       `# `is_anonymous:  Atributo de sólo lectura que siempre es False. Esta es una forma de diferenciar objetos Usery AnonymousUser. Generalmente, debería preferir utilizar             is_authenticated.


      - last_login: Una fecha y hora del último inicio de sesión del usuario.

      - date_joined: Una fecha y hora que indica cuándo se creó la cuenta. Se establece en la fecha/hora actual de forma predeterminada cuando se crea la cuenta.


Ahora bien, seguidamente veremos como utilizando el objeto User y sus atributos para podemos iniciar sesion y cerrarla.

      1 - Iniciaremos sesion con un nombre de unsuario y contrasena que previamente hemos creado.
      2 - Una vez que hemos iniciado sesion, nuestra vista nos redirigira a la pagina de inicio de la aplicacion.
      3 - La pagina de incio, solo permitira a usuarios que han iniciado sesion.
      4 - Finalmente, cerraremos sesion y el cual no redirigira a la pagina de login nuevamente.

Partiremos que ya tenemos un proyecto creado y una aplicacion loginApp con las configuraciones necesarias para su funcionamiento, por lo tanto la app tendria los siguientes archivos.

      1 - archivo login.html
      2 - archivo home.html
      3 - la configuracion del archivo urls.py

Trabajaremos exclusivamente en el archivo views de nuestra app creada previamente. Primeramente necesitaremos importar los modulos necesarios para renderizar nuestra plantilla y realizar el redireciconamiento.

      from django.shortcuts import render, redirect 

- render: es una función de Django que se utiliza comúnmente en las vistas para generar una respuesta HTTP que representa una página HTML renderizada a partir de                   una plantilla de Django.
- redirect: Se utiliza para redirigir al navegador del cliente a otra página web.

        from django.contrib.auth import login

Luego importamos la funcion login, que utilizaremos para gestionar la autenticacion del usuario. Para iniciar sesión como usuario, desde una vista, se utiliza la funcion login(). Se necesita un HttpRequest y un User. La funcion login guarda la ID del usuario en la sesión, utilizando el marco de sesión de Django.

Funcionamiento: la funcion login, no realiza la verificación de las credenciales del usuario (nombre de usuario y contraseña). En su lugar, se utiliza para establecer la sesión de usuario una vez que las credenciales ya han sido verificadas y se ha determinado que el usuario está autenticado.

La verificación de las credenciales, es decir, la comprobación de que el nombre de usuario y la contraseña son correctos, generalmente se realiza en otra parte de tu código. Esto suele ser parte de la lógica de tu vista de inicio de sesión antes de llamar a la función login.

   La función login realiza las siguientes acciones:
              - Crea una sesión de usuario para la solicitud actual.
              - Almacena información sobre el usuario autenticado en la sesión.
              - Establece una cookie en el navegador del cliente para rastrear la sesión del usuario.
              - El usuario ahora se considera autenticado y puede acceder a las partes protegidas de la aplicación que requieren autenticación.


            from .django.contrib.auth.forms import AuthenticationForm 




            


