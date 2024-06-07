# Despliegue continuo utilizando Jenkins, Docker y Kubernetes

## Herramientas y recursos necesarios
- Instalar Docker.
- Crear una cuenta en [Docker Hub](https://hub.docker.com).
- Entorno de Kubernetes. Pueden utilizar [Minikube](./03-kubernetes-instructions-es.md).

## Configuración Previa

1. En Jenkins, es necesario instalar el plugin "CloudBees Docker Build and Publish".

2. Para este caso, es necesario que las 


## Configuración de Pipeline

0. Si es una aplicación nueva, crear un pipeline desde 0. Pueden utilizar [esta guia](./01-Jenkins-ci-instructions-es.md) como referencia.

1. Entrar a las configuraciones del pipeline. En las opciones de Ejecución, agregamos el paso de "Docker Build and Publish", y se deben rellenar los datos correspondientes.