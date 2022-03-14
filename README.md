# Dockerizar aplicación Django-React y Hacer Deploy de Docker-compose en local:

-1- Clonar el repositorio del código de la dirección:

   -  https://github.com/Greys5/docker-django-react.git/
            
-2- Instalar Docker/ docker compose para poder ejecutar los comandos desde local:

<a href="https://docs.docker.com/engine/install/" target="_blank">Docker</a>

<a href="https://docs.docker.com/compose/install/" target="_blank">Docker Compose</a>

-3- Una vez instalado , verificar la instalación: 

    Ejecutar:
    
       > docker --version 
       
       > docker-compose --version


-4- Revisar y/o modificar el archivo .env en el cuál se encuentran las variables con los valores para la base de datos -en este caso postgreSql-, de puertos para los servicios y settings del back.

-5- Una vez realizada la verificación y/o modificación de variables necesarias, (ubicados en el path: docker-app/django-app ) ejecutar el comando : 
      
      > docker compose config
    
  El comando ejecutará una revisión de la configuración del archivo docker-compose.yaml y se visualizará en el terminal la configuración con las         variables indicadas o en su caso si hace falta alguna variable requerida.
Luego ejecutamos:

        > docker-compose build
    
   *Dicho comando hace el Build los servicios indicados en el docker-compose.yaml que son: el dockerfile ubicado en el folder back, dockerfile ubicado en el folder front y levantará el servicio de la DB indicada en el docker-compose.yaml*

-6- Una vez creadas las imagenes de los servicios, ejecutar el comando:

        > docker-compose up
        
   *El cuál puede ir con el flag -d (docker-compose up -d) para ejecutarse en background y no quedé atado a la terminal*

-7- Verificar el funcionamiento de los servicios desde la dirección local en el navegador:

        https://localhost:puerto



*Se puede verificar el ingreso correcto a la base de datos ejecuntando en consola con el DB_USER y DB_NAME indicados:
    Ejemplo:
        > docker-compose exec db psql --username=postgres --dbname=postgres*


# Launch EC2 Instance

-1- Seleccionar la instancia en este caso (free tier) Amazon Linux 2 AMI  >
t2 micro.

-2- En la sección de Configure Instance Details > Advanced Details > User data seleccionamos "As file" y adjuntamos el archivo script.sh que tenemos en el repo.

-3- Selecccionar o crear el security group para permitir el acceso por medio de la IP externa.


-4-Una vez inicia la instancia, la seleccionamos y damos a connect, dentro del terminal de la instancia ejecutamos los siguientes comandos:

        > git clone https://github.com/Greys5/docker-django-react.git

        > cd docker-django-react/

        > docker-compose up --build -d

-5- Se crea una Elastic Ip, y se asocia con la instancia en la cuál quedaron corriendo los servicios levantados de Docker.

-6- Se configuran las reglas de firewall y security group para poder ingresar desde la IP externa.

-7- Verificamos el funcionamiento del servicio desde ip-externa:puerto o desde la consola"

    -(En este caso):

        - curl 54.242.0.118:8000
        - curl 54.242.0.118:3000
