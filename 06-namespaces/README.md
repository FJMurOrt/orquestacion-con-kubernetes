# 06 - Namespaces

En este ejercicio creo dos namespaces, desarrollo y produccion, y despliego la misma aplicación en ambos con distinto número de réplicas.

## ¿Para qué sirven? Por ejmplo

- Separar entornos (desarrollo, staging, producción) dentro del mismo clúster
- Evitar conflictos de nombres: dos objetos pueden llamarse igual si están en namespaces distintos
- Aplicar cuotas de recursos por entorno

## Namespaces por defecto

Todo clúster incluye varios de serie:

- default - donde se crean los recursos si no se indica otro
- kube-system - componentes internos de Kubernetes
- kube-public - recursos accesibles por todos

## ¿Cómo aplicarlo?

```bash
kubectl apply -f namespaces.yaml
kubectl apply -f deployment-desarrollo.yaml
kubectl apply -f deployment-produccion.yaml
```

## ¿Cómo comprobarlo?

```bash
kubectl get namespaces
kubectl get pods -n desarrollo
kubectl get pods -n produccion
```

En desarrollo deben aparecer 2 pods y en producción 4.

Sin indicar namespace, - kubectl get pods -  solo muestra los del namespace "default".

Para ver los pods de todos los namespaces:

```bash
kubectl get pods --all-namespaces
```

## Cambiar el namespace por defecto

Para no tener que escribir -n en cada comando:

```bash
kubectl config set-context --current --namespace=desarrollo
```

## Eliminar

Al eliminar un namespace se eliminan todos los recursos que contiene:

```bash
kubectl delete namespace desarrollo
kubectl delete namespace produccion
```
