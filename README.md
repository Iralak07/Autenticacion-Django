# Autenticacion-Django
Este repositorio explica el uso del sistema de autenticación de Django

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
            
                is_anonymous¶
            
                    Atributo de sólo lectura que siempre es False. Esta es una forma de diferenciar objetos Usery AnonymousUserobjetos. Generalmente, debería preferir utilizar is_authenticatedeste atributo.




      - last_login: Una fecha y hora del último inicio de sesión del usuario.

      - date_joined: Una fecha y hora que indica cuándo se creó la cuenta. Se establece en la fecha/hora actual de forma predeterminada cuando se crea la cuenta.

    
