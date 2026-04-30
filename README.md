# App Demo System - Helm Chart

Este Helm Chart permite desplegar de forma sencilla el ecosistema de **App Demo**, compuesto por un Frontend, una API (Backend) y una base de datos MySQL.

## Estructura del Sistema

- **Frontend**: Imagen `yurbendock/clientes-front/front`. Expuesto vía LoadBalancer.
- **Backend (API)**: Imagen `yurbendock/clientes-backend`. Se comunica con MySQL internamente.
- **Base de Datos**: MySQL 8.0 oficial.

---

## Comandos de Gestión

### 1. Instalación (Release)
Para desplegar todo el sistema por primera vez:
```powershell
helm install app-demo-release .
```

### 2. Actualización
Si realizas cambios en `values.yaml` o en los templates, usa este comando para aplicar los cambios:
```powershell
helm upgrade app-demo-release .
```

### 3. Verificar el Estado
Para ver los pods creados y los servicios:
```powershell
kubectl get pods
kubectl get services
```

### 4. Desinstalación
Para borrar todos los recursos creados por este chart:
```powershell
helm uninstall app-demo-release
```

---

## Configuración (values.yaml)

Puedes personalizar el despliegue editando el archivo `values.yaml`:

| Variable | Descripción | Valor por Defecto |
| :--- | :--- | :--- |
| `replicaCount` | Número de réplicas para Front y API | `1` |
| `frontend.env.apiUrl` | URL de conexión para el Front | `http://api-service:8080/api` |
| `api.env.dbPassword` | Contraseña de la base de datos | `password123` |
| `api.image` | Tag de la imagen de la API | `latest` |

### Ejemplo: Cambiar réplicas desde la consola
```powershell
helm upgrade app-demo-release . --set replicaCount=3
```

---

## Requisitos Previos
- Tener `helm` instalado.
- Un cluster de Kubernetes activo (Minikube, Docker Desktop, AKS, etc.).
- Las imágenes de Docker deben estar disponibles en Docker Hub o en tu registro local.
