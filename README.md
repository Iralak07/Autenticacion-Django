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

            - AuthenticationForm: hereda los atributos y métodos de forms.Form, la clase base para la construcción de formularios en Django.

Ahora que hemos importado lo necesario para construir nuestra vista de autenticacion y cierre de sesion, veamos paso a paso como construirlo.

                  # Importación de módulos necesarios
                  from django.shortcuts import render, redirect  # Para renderizar plantillas y redireccionar
                  from django.contrib.auth import login, logout  # Para gestionar la autenticación de usuarios
                  from .forms import AuthenticationForm  # Importar un formulario personalizado

                  # Aqui creamos la funcion para llamar a nuestra pagina principal 'home.html',a la cual nos redirigira nuestra pagina de inicio de sesion, una vez                               autenticado nuestro usuario
                  def homeView(request):
                      template = 'home.html'
                      return render(request, template)
                        
                  # Seguidamente creamos nuestra funcion que mostrara nuestra pagina de inicio de sesion con el formulario correspondiente
                  def loginView(request):
                      template = 'login.html'

                      # comprobamos en primer lugar si el metodo de solicitud es 'POST', en caso de ser afirmativo, nos quiere decir que estamos enviando datos a traves de                         los formularios existentes en dicha pagina
                      if request.method == 'POST':
                          # Aqui creamos una instancia de AuthenticationForm, pasandole como paramentros el request, y los datos enviados a traves de la solicitud POST
                          # Esto a fin de que pueda verificar la solicutd realizada y los datos enviados en el mismo
                          form = AuthenticationForm(request, data=request.POST)
                          # Seguidamente verificamos con el metodo is_valid() heredado de forms.Form, el cual se encarga de corroborar que se han enviados datos y que los                              mismos no contienene ningun error, devolviendo un False o True
                          if form.is_valid():
                              # Auqui paso algo particular, el is_valid() no unicamente se limita a verificar si los campos de los formularios son validos, sino que tambien                                 verifica si el user y password existen en la base de datos, en tal caso lo podemos extraer de form.user_cache
                              user = form.user_cache
                              # luego iniciamos sesion con el usuario actual
                              login(request, user)
                              # finalmente nos redirige a la pagina principal
                              return redirect('loginApp:home')
                          else:
                              # En el caso que los campos de formulario no sea valido en en el caso de que el usuario no se encuentre registrado, nos devuelve el formulario,                                pero en este caso con un error, que lo podemos ver en nuestra plantilla html con {{form.errors}}
                              return render(request, template, {'form': form})


                      # En el caso que la peticion no sea 'POST', nos envia la plantilla template y el formulario para que podamos iniciar sesion.
                      form = AuthenticationUserForm()
                      return render(request, template, {'form': form})

Con esto ya es suficiente para crear una funcion para autenticar e iniciar sesion con un usuario, ahora bien, en el caso de que ya nos hemos verificado e iniciado sesion, y nos dirigamos por ejemplo en una nueva pestana del navegador sin haber cerrado sesion previamente, esto nos deberia autorizar a ingresar a la pagina principal sin necesidad de autenticarnos nuevamente gracias a login(), por lo tanto tendremos que verificar previamente en nuestra vista actualmente se encuentra abierta una seseion de usuario. 

Para esta tarea utilizaremos un decorador llamado login_required(), el cual lo importamos de "from django.contrib.auth.decorators import login_required".

                        # Este decorador se encarga de verificar existe una sesion abierta por un usuario, en caso de que no existe y se quiera acceder a la pagina principal                          esto lo redirige a la pagina de autenticacion de usuario, en caso contrario lo redirige a la pagina principal
                        @login_required(login_url='loginApp:login')
                        def homeView(request):
                            template = 'home.html'
                            return render(request, template)
                        
                        
                        def loginView(request):
                            template = 'login.html'

                            # Para la pagina de login, utilizaremos el metodo .is_authenticated, que devuelve un True o False dependiendo si existe un usuario que haya                                     inciado seseion y se encuentra abierto actualmente, con este condicional en caso de True lo envia directamente a la pagina principal, para asi                               evitar volver a iniciar sesion
                            if request.user.is_authenticated:
                                return redirect('loginApp:home')
                        
                            if request.method == 'POST':
                                form = AuthenticationUserForm(request, data=request.POST)
                                if form.is_valid():
                                    user = form.user_cache
                                    login(request, user)
                                    return redirect('loginApp:home')
                                else:
                                    return render(request, template, {'form': form})
                        
                            form = AuthenticationUserForm()
                            return render(request, template, {'form': form})



Finalmente, necesitamos cerrar la sesion, para ello crearemos una funcion nueva que se encargara de cerrar la sesion, una vez que nos situemos en la pagina principal. En este caso queda a eleccion de cada uno, de crear un boton que al pulsar llame a la funcion que crearemos en nuestra vista de cierre de sesion.

                        # Definición de la función para cerrar sesión
                        def logOutView(request):
                            # Cerrar la sesión del usuario
                            logout(request)
                            # Redirigir al usuario a la página de inicio de sesión
                            return redirect('loginApp:login')


