# 03 - Service

Para mandar el tráfico necesito un Service ya que los Pods tienen IPs internas que cambian cada vez que se recrean, y lo que se necesita es una dirección estable que no cambie a la que llegue el tráfico y éste a su vez lo reparta hacia los Pods.

En este ejercicio expongo el Deployment de nginx que había creado anteriormente mediante un Service de tipo NodePort.

## ¿Por qué con NodePort? Hay 3 tipos

- **ClusterIP** — Solo accesible desde dentro del clúster, es decir, no me vale si lo que quiero es exponerlo hacia fuera.
- **NodePort** — Abre un puerto en el nodo para permitir acceso desde fuera. Útil para pruebas en entornos locales.
- **LoadBalancer** — Un balanceador de carga del proveedor clen la nube.

## Los tres puertos

| Puerto | Dónde vive | Función |
|--------|-----------|---------|
| `nodePort` | En el nodo | Puerto de entrada desde fuera del clúster (30000-32767) |
| `port` | En el Service | Puerto por el que se accede al Service dentro del clúster |
| `targetPort` | En el contenedor | Puerto donde escucha la aplicación |

El recorrido de una petición sería: nodePort → port → targetPort → contenedor.

## ¿Cómo aplicarlo?

Requiere tener aplicado antes el Deployment del ejercicio 02.

```bash
kubectl apply -f ../02-despliegue/deployment.yaml
kubectl apply -f service.yaml
```

## ¿Cómo comprobar que funciona?

```bash
kubectl get services
kubectl describe service servicio-nginx
```

En `describe` aparecen los Endpoints, que son las IPs de los pods a los que el Service está enviando tráfico.

## Para acceder al Service

Con Minikube:

```bash
minikube service servicio-nginx --url
```

## Eliminar el Service

```bash
kubectl delete -f service.yaml
```