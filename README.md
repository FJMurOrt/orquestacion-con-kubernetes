# Orquestación con Kubernetes

Ejercicios prácticos de Kubernetes en los que voy cubriendo conceptos fundamentales, desde lo más básico hasta las mejores prácticas.

Cada carpeta contiene los archivos YAML y un README explicando qué hace cada uno de ellos, cómo aplicarlos y cómo deshacerlos.

## Ejercicios

| # | Ejercicio | Contenido |
|---|-----------|-----------|
| 01 | [Pod](./01-pod) | La unidad mínima de despliegue en Kubernetes |
| 02 | [Deployment](./02-despliegue) | Réplicas, autohealing y actualizaciones progresivas |
| 03 | [Service](./03-servicio) | Exposición de los pods mediante una dirección estable |
| 04 | [ConfigMap y Secret](./04-configmap-secret) | Separar la configuración y las credenciales del código |
| 05 | [Volúmenes](./05-volumenes) | Almacenamiento persistente con PVC |
| 06 | [Namespaces](./06-namespaces) | División lógica del clúster por entornos |

## Requisitos

- Un clúster de Kubernetes (estos ejercicios están pensados para Minikube)
- kubectl instalado y configurado

## Uso

Entra en cada carpeta y aplica cada uno de ellos:

```bash
kubectl apply -f XXXX.yaml
```

Para eliminar los recursos creados:

```bash
kubectl delete -f XXXX.yaml
```

## Tecnologías

- Kubernetes
- Minikube
- kubectl
