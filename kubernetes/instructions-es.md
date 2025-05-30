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

Como todo cluster de Kubernetes, Minikube también viene con un dashboard de análisis. Para acceder a el, hay que ejecutar el siguiente comando en una terminal nueva:
```bash
$ minikube dashboard
```

Por último, podemos conectarnos al cluster de minikube mediante shh. Eso lo hacemos con este simple comando:
```bash
$ minikube ssh
```

Esto nos arrojará una URL por donde podremos acceder

## Algunos comandos básicos
La instalación de Docker viene con el cliente CLI de Kubernetes (kubectl). Este cliente nos permite realizar acciones para obtener información del cluster. Algunos de los comandos más utilizados son:
```bash
# Obtiene los pods actualmente en ejecución
$ kubectl get pods

# Obtiene información de los nodos
$ kubectl get nodes

# Obtiene los namespaces del cluster
$ kubectl get ns

# Obtiene los volumenes persistentes creados
$ kubectl get pvc

# Tambien uno puede agregar flags para filtrar información
$ kubectl -n NAMESPACE_NAME get pods

# Permite ejecutar comandos dentro de un pod
$ kubectl exec

# Muestra los logs de un pod
$ kubectl logs
```

## Instalación de Jenkins en Minikube

Primero hay que crear un espacio de nombre (namespace) para separar jenkins y cualquier otra herramienta de nuestros deploys. Para eso, ejecutamos el siguiente comando.
```bash
kubectl create namespace devops-tools
```

Luego, debemos crear una cuenta de servicio. Esto lo haremos con el archivo [jenkins-service-account.yaml](jenkins-service-account.yaml). Este archivo contiene las definiciones de un rol de cluster (ClusterRole), de una cuenta de servicio (para permitir la conexión dentro del cluster) y el vínculo entre ambas.

Este archivo lo enviamos al cluster de Minikube para aplicar la configuración.
```bash
kubectl apply -f serviceAccount.yaml
```

Posteriormente, debemos crear un volumen para persistir la información de los pipelines de jenkins. Esto lo hacemos con el archivo [jenkins-volume.yaml](jenkins-volume.yaml). Este archivo de configuración crea una clase de almacenamiento [StorageClass](https://kubernetes.io/docs/concepts/storage/storage-classes/), un volumen persistente [PersistentVolume]() que define los recursos del volumen en cuestion, y un [PersistenVolumeClaim](), que indica quien puede hacer uso

```bash
$ kubectl create -f jenkins-volume.yaml
```

En caso que el pod sea eliminado o reiniciado, la información se mantendrá intacta dentro del cluster. Sin embargo, si se elimina el nodo, la información también se eliminara. Por lo mismo, en soluciones futuras, se debe buscar una forma de alojar la información mediante un servicio dedicado.

