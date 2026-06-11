# Despligue en la nube


## Que es Elastic Beanstalk
Para desplegar la aplicacion en AWS, utilizaremos el servicio AWS Elastic Beanstalk (AWS EB), permite migrar, implementar y escalar fácilmente aplicaciones full stack. Gestiona las operaciones de infraestructura y aplicaciones, lo que nos ayudará a centrarnos en la lógica de negocio.

Gracias a EB se podremos desplegar fácilmente todas nuestras aplicaciones haciendo uso de `docker` y `docker compose`, y así nos olvidamos de cualquier cambio de entorno.

## Pre-requisitos
En este tutorial, partiremos de la aplicacion con [micro servicios](../springcloud/intro.md) y [dockerizada](../docker/installdocker.md).
Igual que vimos en [AWS CLI](./cli.md), instalaremos todo usando WSL.

## Instalacion EB CLI
Para poder desplegar la aplicacion, primero necesitaremos la CLI de Elastic Beanstalk, para ello necesitamos unos pasos previos.


1. Actualizar los paquetes de ubuntu.
```bash
sudo apt update
sudo apt upgrade -y
``` 

2. Instalar python.
```bash
sudo apt install -y python3 pip pipx python-is-python3 
``` 

3. Instalar virtualenv.
```bash
sudo pipx install virtualenv
```

4. Instalar EB CLI.
```bash
git clone https://github.com/aws/aws-elastic-beanstalk-cli-setup.git
python ./aws-elastic-beanstalk-cli-setup/scripts/ebcli_installer.py
```

5. Verificar que EB CLI se ha instalado correctamente.
```bash
eb --version
```

## Despligue de la aplicacion

Una vez instalada EB CLI, en la carpeta raiz donde esta nuestro docker compose y los proyectos, crearemos el contenedor en la nube y desplegaremos la aplicacion.

1. Inicializar el proyecto.
```bash
eb init -p docker docker-compose-tutorial --region eu-west-3
```
2. (Opcional) si queremos conectarnos a la instancia de EC2 por SSH, deberemos configurar un par de claves.
```bash
eb init
```
Aparecerá un mensaje parecido a este, simplemente seleccionaremos que clave queremos usar.
```
Do you want to set up SSH for your instances?
(y/n): y
Select a keypair.
1) my-keypair
2) [ Create new KeyPair ]

```
3. Creamos el entorno y desplegamos la aplicacion.
```bash
eb create docker-compose-tutorial
```
