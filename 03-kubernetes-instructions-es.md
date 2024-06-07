# Kubernetes con Minikube
[Minikube](https://minikube.sigs.k8s.io/docs/) es una aplicación que nos permite configurar un Cluster sencillo de Kubernetes en nuestros dispositivos, con el fin de realizar pruebas.

## Herramientas y recursos necesarios

- Instalar Docker

## Pasos a seguir para la instalación
Primero, debemos instalar minikube ejecutando el siguiente comando (en Linux o WSL):
```bash
$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
$ sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
```

Luego, para iniciar Minikube, hay que asegurarse que se está ejecutando Docker, y ejecutar lo siguiente:
```bash
$ minikube start --driver=docker
```

## Algunos comandos básicos
La instalación de Docker viene con el cliente CLI de Kubernetes (kubectl). Este cliente nos permite realizar acciones para obtener información del cluster. Algunos de los comandos más utilizados son:

- kubectl get pods
- kubectl get nodes
- kubectl get ns
- kubectl exec
- kubectl logs
- kubectl (-n namespace_name)