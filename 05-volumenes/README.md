# 05 - Volúmenes

Para aplicaciones en las que se necesite conservar datos, como una base de datos, hace falta almacenamiento persistente y aquí es donde entra en juego lo siguiente.

## Los dos objetos que necesitamos

- **PersistentVolumeClaim (PVC)** — La petición. La aplicación solicita el almacenamiento que necesita.
- **PersistentVolume (PV)** — El almacenamiento real: una carpeta del nodo, un disco del proveedor cloud, un NFS.

## Modos de acceso

| Modo | Significado |
|------|-------------|
| `ReadWriteOnce` | Un solo nodo puede montarlo en lectura y escritura |
| `ReadOnlyMany` | Varios nodos pueden montarlo en solo lectura |
| `ReadWriteMany` | Varios nodos pueden montarlo en lectura y escritura |

## ¿Cómo aplicarlo?

```bash
kubectl apply -f pvc.yaml
kubectl apply -f pod-con-volumen.yaml
```

## ¿Cómo comprobarlo?

```bash
kubectl get pvc
kubectl describe pvc almacenamiento-datos
```

El estado del PVC debe ser "Bound", lo que significa que se le ha asignado almacenamiento.

## Probar la persistencia

Escribir un archivo dentro del volumen:

```bash
kubectl exec pod-con-almacenamiento -- sh -c "echo 'Hola!' > /usr/share/nginx/html/index.html"
```

Eliminar el pod y volver a crearlo:

```bash
kubectl delete pod pod-con-almacenamiento
kubectl apply -f pod-con-volumen.yaml
```

Comprobar que el archivo sigue ahí:

```bash
kubectl exec pod-con-almacenamiento -- cat /usr/share/nginx/html/index.html
```

## Eliminar

```bash
kubectl delete -f pod-con-volumen.yaml
kubectl delete -f pvc.yaml
```
