Mi primer proyecto en Django
===================

Este repositorio está destinado a aprender Django desde cero, con un conocimiento previo (básico) de Python. La aplicación desarrollada esta basada en el curso **_A begginners Guide to Django!_** impartido por **_Avinash Jain_**, el cual se encuentra disponible en **_Udemy_**.

Requerimientos
============

1. Instalación de Python 3.5 o superior. Lo puedes descargar en **[Python.org](https://www.python.org/)**.
2. Instalación de un IDE _(Integrated Development Environment )_ para facilitar la programación con python. El más recomendado es **[PyCharm](https://www.jetbrains.com/pycharm/)** que cuenta con su versión gratuita.

Creando el entorno virtual
=====

Para comenzar a utilizar Django, primero creamos nuestro proyecto en la carpeta que queramos y en la terminal de PyCharm, escribimos el siguiente código:

`pip3 install virtualenv`

El cual instala un entorno virtual que nos permite instalar Django una sola vez en vez de tener que hacerlo en cada aplicación que desarrollemos y asi ahorramos espacio en nuestro equipo.

A continuación, creamos un entorno virtual mediante el siguiente comando (para Windows): 

`C:\Python36\python -m venv myvenv`

Donde `C:\Python36\python` es la ruta donde esta instalado Python en tu computadora y `myvenv` el nombre de tu entorno virtual (o `venv`).

Por último, procedemos a activar (o ejecutar) nuestro entorno virtual _myvenv_ con el siguiente código: 

`myvenv\Scripts\activate` 

El cual será exitoso si en nuestra ruta de proyecto en la Terminal aparece _(env)_. En caso de tener problemas o estar utilizando otro sistema operativo, recomiendo leer el tutorial en [Django Girls][1].

Una vez finalizado este paso, es necesario configurar el interprete utilizado por PyCharm a nuestro entorno virtual. Para ello, vamos a `file -> settings -> Project Interpreter` y seleccionamos la ruta de nuestro _myvenv_ en el proyecto.

Instalando Django
====

Una vez terminada la creación y configuración de nuestro entorno virtual en PyCharm, solo resta instalar Django mediante el siguiente comando:

`pip install django`

Y listo! Ya podemos trabajar en tu propia aplicación web con Django. **Nota:** la instalación puede demorar un poco, asi que ten paciencia. Aparte de Django, tambien se instala el módulo _pytz_ que permite el manejo de las zonas horarias.

Creando el proyecto
====

Una vez instalado Django, procedemos a crear el proyecto mediante el siguiente comando:

`django-admin startproject mysite`

El cual creará un nuevo directorio donde trabajaremos en nuestro proyecto. Este directorio llamado _mysite_ tendrá una subcarpeta homónima y otros archivos.

- **Manage.py:** Se encarga de la comunicación entre la terminal y Django.
- **mysite/\_\_init\_\_.py:** Un archivo vacio que permite decirle a Python que trate el directorio como paquetes (_Python package directories_).
- **mysite/settings.py:** El archivo de configuración de nuestra app.
- **mysite/urls.py:** Maneja todas las rutas o _URLs_ de nuestro sitio.
- **mysite/wsgi.py:** Se encarga de desplegar la página en un servidor.

Antes de seguir, cabe mencionar la forma en que un proyecto esta estructurado en Django. Esto se le conoce como el patrón de arquitectura de software, siendo Django basado en el _MTV_ (Modelo, Plantilla, Vista). Para profundizar sobre ello, leer el siguiente [enlace][2].

Creando la primera App
====

Con los previos conceptos sobre el patrón _MTV_, procedemos a crear nuestra primera app; Para ello, necesitamos ubicarnos en la carpeta de nuestro proyecto mediante el comando `cd mysite` y luego escribimos el siguiente comando en la terminal:

`python manage.py startapp polls`

Mediante este comando, se crea un nuevo directorio llamado *_polls_* dentro de nuestra carpeta *_mysite_*. Dentro de este nuevo directorio, encontraremos varios archivos que se encargan de tareas especificas en nuestro patrón _MTV_.

Ahora para probar que todo funciona correctamente, ejecutamos el comando `python manage.py runserver` el cual nos arroja una dirección para abrir en el navegador, la cual despliega una página funcional con unos cuantos titulos felicitandonos por ello. ¡Buen trabajo!

Creando la base de datos
====

La forma en que Django crea la base de datos y la surte de información es a tráves de la programación orientada a objetos, la cual se maneja en el archivo _models.py_ de nuestra app.

Dentro de este archivo, creamos las clases con los campos deseados para nuestras "tablas" de la base de datos. Una vez finalizado, incluimos nuestra app en el archivo _settings.py_ del directorio _mysite_ agregando debajo de los campos en **_INSTALLED\_APPS_** nuestra app `polls`. 

Ya con ello, ejecutamos las _migraciones_ mediante el comando:

`python manage.py makemigrations polls`

¡Y listo! Ya se han creado nuestros modelos de la app *polls*. Para finalizar, le decimos a Python que realice la migración a la base de datos mediante el comando:

`python manage.py migrate` 

Con ello deberia aparecer una carpeta llamada _migrations_ en nuestra carpeta _polls_ donde el archivo _0001_initial.py_ contiene nuestros modelos. Por último, para el guardado de datos, necesitamos crear un superusuario o _admin_ con el comando `python manage.py createsuperuser` el cual nos pedirá un nombre de usuario, email y contraseña.
**Nota:** La terminal no muestra la contraseña asi que tomense su tiempo para escribirla sin errores. Una vez finalizada la creación, ejecute el servidor y agreguen a la URL la palabra **_/admin_** de esta manera: `http://127.0.0.1:8000/admin`. Ingrese su usuario y contraseña para proceder con el panel de administración. 

:tada: ¡Felicidades! Ya puede obtener datos desde la base de datos y mostrarla en el navegador.

En este panel de administración podrá visualizar los modelos y agregar datos siempre y cuando incluya los modelos en el archivo _admin.py_ de su aplicación _polls_.

Agregando las plantillas (Templates)
====

Django permite separar tanto la programación del lado del **cliente** como del lado del **servidor**, es decir, la experiencia de usuario de la administración del sitio y la gestión de bases de datos. En nuestro caso, HTML se encarga exclusivamente de todo lo relacionado al diseño de nuestra página web mientras que Python gestiona
todo lo del servido (mediante Django por supuesto). Esto se debe a que un documento web (HTML) no puede leer un código Python, por lo que la manera de hacerlo es a tráves de plantillas (o _Templates_).

En este proyecto, creamos un nuevo directorio llamado _templates_ dentro de nuestra aplicación _polls_ y luego dentro de ese directorio, creamos otro directorio llamado _polls_. Aunque parezca algo redundante, la finalidad de este directorio es separar cualquier archivo de una _Third party app_ o aplicación de terceros,
que contengan un archivo _index.html_ y evitar así conflictos entre nuestra aplicación y la de terceros.

Para crear un archivo html, solo basta con hacer click derecho en el directorio `polls -> new -> html file` y nombrarlo _index.html_. Ahora, como necesitamos una plantilla para nuestro proyecto, ya sea con el sistema de plantillas DTL o Jinja2 (lease la documentación [aquí](https://docs.djangoproject.com/en/2.0/topics/templates/)),
se debe utilizar _template tags_ o etiquetas de plantilla en el documento HTML. Estos comienzan y terminan con llaves y signos de porcentaje así: `{% condicionales aquí %}`, los cuales permiten transferir cosas de Python como cosas en HTML, mejorando así la facilidad y rapidez en desarrollar sitios web dinámicos.

**Nota:** La explicación a continuación tiene en cuenta que ya ha llegado hasta este punto del curso (Sección 4: URLs y Vistas) y ya conoce de antemano la funcionalidad de los archivos _views.py_ y _models.py_.

Con ello, en nuestro documento _index.html_ incluimos el siguiente código:

`
{% if latest_questions %}
    <ul>
        {% for question in latest_questions %}
            <li><a href='/polls/{{question.id}}'><b> {{ question.question_text }}</b></a></li>
        {% endfor %}
    </ul>
{% else %}
    <p> No tienes ninguna pregunta. Agrega más. </p>
{% endif %}
`

Donde se revisa si existen elementos en nuestro objeto **Question** (creado en el archivo models.py) el cual es inspeccionado al cargar la página (en la definición de index dentro de views.py). Si hay preguntas almacenadas en nuestra base de datos, itera cada uno de los elementos en dicho objeto y los incluye en el _index.html_
como una lista sin ordenar. 

**Para que estas etiquetas funcionen es necesario referenciar el documento html a al archivo de vistas (views.py) de la aplicación.**

**Correción de error:** Debido a cambios en las versiones Django 1.11 o superiores, el método _.render()_ solo necesita como entrada un diccionario, a diferencia del curso donde se usa una función _RequestContext_ para generar el contexto adecuado.

[1]: https://tutorial.djangogirls.org/es/
[2]: http://librosweb.es/libro/django_1_0/capitulo_5/el_patron_de_diseno_mtv.html
