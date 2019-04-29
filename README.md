# Flask + Docker: App mínima
App mínima de Flask configurada con Docker.

Este repositorio contiene código fuente de Python del [flask.pocoo.org quickstart](http://flask.pocoo.org/docs/1.0/quickstart/#a-minimal-application), configurado con Docker en base a la imagen [tiangolo/uwsgi-nginx-flask](https://github.com/tiangolo/uwsgi-nginx-flask-docker), un buen punto de partida para explorar Flask creando tus primeras aplicaciones, APIs o simplemente probando funcionalidades descritas en la [Documentación oficial de Flask](http://flask.pocoo.org/docs/).

## Prerrequisitos

<a href="https://docs.docker.com/v17.09/engine/installation/" target="_blank" title="Install Docker">Docker</a> y <a href="https://docs.docker.com/compose/install/" target="_blank" title="Install Docker Compose">Docker Compose</a> son esenciales para ejecutar nuestra App mínima.

## Despliegue de App con Docker Compose

**Nota**: Antes de ejecutar cualquier comando de Docker Compose asegúrate de estar ubicado en el directorio principal del proyecto.

* Construye la imagen del contenedor de la app:

```bash
docker-compose build
```

* Luego inicia el servicio de la app:

```bash
docker-compose up -d
```

La App construida con Docker, deberá estar disponible en: http://localhost o en la dirección de IP o dominio del servidor donde realices el despliegue.

Para revisar los logs del servicio, ejecuta:

```bash
docker-compose logs flask-app
```

## Desarrollo en modo interactivo
Para que el servicio de docker en estado de ejecución tome los cambios que realices en tu equipo, debes ejecutar el servicio en modo interactivo.

Primero debes asegúrarte de editar el archivo `docker-compose.override.yml` de la siguiente manera:

* No interactivo
```
version: '2'
# services:
#   flask-app:
#     volumes:
#       - './flask-app/app:/app'    
#     command: bash -c "while true; do sleep 1; done"
#     environment:
#       - FLASK_APP=app/main.py
#       - FLASK_ENV=development
#       - FLASK_DEBUG=1
#       - 'RUN=flask run --host=0.0.0.0 --port=80'
``` 

* Modo interactivo
```
version: '2'
services:
  flask-app:
    volumes:
      - './flask-app/app:/app'    
    command: bash -c "while true; do sleep 1; done"
    environment:
      - FLASK_APP=app/main.py
      - FLASK_ENV=development
      - FLASK_DEBUG=1
      - 'RUN=flask run --host=0.0.0.0 --port=80'
``` 

Luego, inicia el servicio:

```bash
docker-compose up -d
```

... y entonces debes entrar al servicio con:

```bash
docker-compose exec flask-app bash
```

Deberías ver algo como:

```
root@773468e59e26:/app#
```

Esto significa que estas en una sesión de `bash` dentro del servicio, como un usuario `root`, bajo el directorio `/app`.

Por último ejecuta la App con:

```bash
$RUN
```

La App construida con Docker, deberá estar disponible para acceder y todos los cambios realizados al código serán tomados por el servicio de forma automática mientras la App esté en ejecución.

## License

Este proyecto está licenciado bajo los términos de la licencia MIT.
