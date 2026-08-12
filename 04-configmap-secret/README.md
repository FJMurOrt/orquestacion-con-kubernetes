# 04 - ConfigMap y Secret

ConfigMap y Secret me permiten separar la configuración del código, de forma que la misma imagen sirva para desarrollo, staging y producción cambiando solo los valores.

## Diferencia

- ConfigMap - Configuración no sensible: entorno, nivel de log, límites, URLs de servicios.
- Secret - Datos sensibles: contraseñas, tokens, claves de API.

## ¿Cómo aplicarlo?

```bash
kubectl apply -f configmap.yaml
kubectl apply -f secret.yaml
```

## ¿Cómo comprobarlos?

```bash
kubectl get configmaps
kubectl get secrets
kubectl describe configmap configuracion-app
```

Los valores de un Secret no se muestran con "describe", solo aparece su tamaño.

Para ver el contenido codificado:

```bash
kubectl get secret credenciales-app -o yaml
```

## ¿Cómo los consume un Pod?

Los valores se inyectan como variables de entorno en el contenedor:

```yaml
env:
  - name: ENTORNO
    valueFrom:
      configMapKeyRef:
        name: configuracion-app
        key: ENTORNO
  - name: DB_PASSWORD
    valueFrom:
      secretKeyRef:
        name: credenciales-app
        key: DB_PASSWORD
```

También pueden montarse como archivos dentro del contenedor mediante volúmenes.

## Eliminar

```bash
kubectl delete -f configmap.yaml
kubectl delete -f secret.yaml
```
