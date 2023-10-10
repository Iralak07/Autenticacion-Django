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

      - user_permissions:

    Relación de muchos a muchos conPermission

is_staff¶

    Booleano. Designa si este usuario puede acceder al sitio de administración.

is_active¶

    Booleano. Designa si esta cuenta de usuario debe considerarse activa. Le recomendamos que establezca esta bandera en Falseen lugar de eliminar cuentas; de esa manera, si sus aplicaciones tienen claves externas para los usuarios, las claves externas no se romperán.

    Esto no controla necesariamente si el usuario puede iniciar sesión o no. Los servidores de autenticación no están obligados a verificar la is_activebandera, sino el servidor predeterminado ( ModelBackend) y RemoteUserBackendhacerlo. Puede utilizar AllowAllUsersModelBackendo AllowAllUsersRemoteUserBackendsi desea permitir que usuarios inactivos inicien sesión. En este caso, también querrás personalizar el AuthenticationFormutilizado por el LoginView, ya que rechaza a los usuarios inactivos. Tenga en cuenta que los métodos de verificación de permisos, como has_perm()la autenticación en el administrador de Django, regresan Falsepara los usuarios inactivos.

is_superuser¶

    Booleano. Designa que este usuario tiene todos los permisos sin asignarlos explícitamente.

last_login¶

    Una fecha y hora del último inicio de sesión del usuario.

date_joined¶

    Una fecha y hora que indica cuándo se creó la cuenta. Se establece en la fecha/hora actual de forma predeterminada cuando se crea la cuenta.

    
