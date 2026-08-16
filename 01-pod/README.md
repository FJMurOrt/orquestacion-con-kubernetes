# 01 - Pod

En este ejercicio creo un Pod con un contenedor de nginx.

## ¿Cómo aplicarlo?

```bash
kubectl apply -f pod.yaml
```

## ¿Cómo comprobarlo?

```bash
kubectl get pods
kubectl describe pod pod-nginx
kubectl logs pod-nginx
```
![1](./capturas/1)
## Acceder al pod

Los Pods no son accesibles desde fuera del clúster por defecto. Para probarlo se puede redirigir un puerto temporalmente:

```bash
kubectl port-forward pod/pod-nginx 8080:80
```

Y acceder en -> http://localhost:8080

![2](./capturas/2)

## Eliminar el pod

```bash
kubectl delete -f pod.yaml
```
