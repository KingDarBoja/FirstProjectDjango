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

Con ello deberia aparecer una carpeta llamada _migrations_ en nuestra carpeta _polls_ donde el archivo _0001_initial.py_ contiene nuestros modelos.

[1]: https://tutorial.djangogirls.org/es/
[2]: http://librosweb.es/libro/django_1_0/capitulo_5/el_patron_de_diseno_mtv.html
