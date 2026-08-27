# Implement CI/CD Pipelines

## 1. Plantillas de Continuous Integration (CI)

Al usar una plantilla de CI, puedes:
- **Construir (build), probar (test) y desplegar (deploy)** código
- Hacer **revisiones de código**
- Gestionar **ramas**
- Hacer **triaging** de problemas

### Lenguajes/frameworks con plantillas de CI disponibles

Go · Java (con **Ant, Gradle o Maven**) · .NET · Node.js · PowerShell · Python · Rust · Swift · Xamarin — entre otros.

> **Dato práctico:** GitHub detecta automáticamente el lenguaje del repo y suele **sugerir** las plantillas más relevantes primero, aunque el orden puede variar ("parece un poco aleatorizado").

## 2. Anatomía de un Workflow de CI (ejemplo .NET)

### Sección `on` (triggers)

Adicional a lo ya visto (push, pull_request en `main`),:

- **fork** — cuando se bifurca el repo
- **label** — cuando se crea, abre o etiqueta un tag/label
- **issues** — cuando se abren o cierran issues
- **comentarios** — cuando se crean o modifican
- **workflow_run** — cuando se ejecuta otro workflow

### Sección `jobs` — ejemplo concreto: job "build" en .NET

| Paso                               | Qué hace                                                                          |
|:-----------------------------------|:----------------------------------------------------------------------------------|
| `actions/setup-dotnet` (u similar) | Configura la versión de .NET a usar (ej. versión 8)                               |
| Restaurar dependencias             | Equivalente a `dotnet restore`                                                    |
| `dotnet build`                     | Comandos que se ejecutan directamente en el entorno .NET — construyen el proyecto |
| `dotnet test`                      | Ejecuta las pruebas del proyecto                                                  |

**Resultados de las pruebas:** los resultados pueden **añadirse/mostrarse directamente en el Pull Request** — es decir, el estado del CI queda visible ahí mismo, sin tener que ir a buscarlo aparte.

### Condicionales dentro del workflow

Se pueden agregar **condiciones** usando `if` — por ejemplo, ejecutar un paso solo **si es un repositorio determinado**.

### Extensibilidad

Puedes agregar **acciones adicionales desde el Marketplace** dentro del mismo workflow, combinando pasos propios con acciones ya publicadas por la comunidad.

## 3. Plantillas de Deployment (CD)

Se puede desplegar hacia distintos destinos, combinando lenguaje/framework + plataforma de destino:

### Lenguajes/frameworks soportados para despliegue
Node.js · Python · Java · .NET · PHP · Docker — entre otros.

### Destinos de despliegue disponibles

| Destino                                    |
|:-------------------------------------------|
| **Azure App Service**                      |
| **Azure Static Web App**                   |
| **Azure Kubernetes Service (AKS)**         |
| **Google Kubernetes Engine**               |
| **Amazon Elastic Container Service (ECS)** |


## 4. Ejemplo concreto: Deploy Node.js → Azure Web App

### Triggers de este workflow de ejemplo

- **push** a la rama principal, **o**
- **workflow_dispatch** (activación **manual**)

### Estructura de Jobs: Build + Deploy

```yaml
jobs:
  build:
    # ... pasos de construcción
  deploy:
    # ... pasos de despliegue
```


## 5. El punto MÁS importante de esta sección: controlar el orden de ejecución con `needs`

Por defecto, los jobs de un workflow se ejecutan **en paralelo** (al mismo tiempo), no secuencialmente.

**El problema:** en un pipeline de CI/CD, esto es un riesgo real — **no puedes desplegar (deploy) código que todavía no terminó de construirse (build)**. Si ambos jobs corren en paralelo, el deploy podría intentar ejecutarse antes de que el build termine.

**La solución — la palabra clave `needs`:**

```yaml
jobs:
  build:
    # ...
  deploy:
    needs: build     # ← esto fuerza que "deploy" espere a que "build" termine
    # ...
```

`needs` establece una **dependencia explícita** entre jobs — el job que la usa **no comenzará hasta que el job referenciado haya terminado exitosamente**.


## Puntos clave

1. GitHub ofrece **plantillas listas para usar** de CI y CD según lenguaje y destino de despliegue — no siempre hay que escribir el YAML desde cero.
2. Los **resultados de tests pueden integrarse visualmente en el Pull Request**.
3. **`needs`** es la palabra clave que controla el orden/dependencia entre jobs — sin ella, todos los jobs corren en paralelo por defecto.
4. Los destinos de despliegue más comunes que reconoce GitHub Actions de forma nativa: **Azure App Service, Azure Static Web App, AKS, GKE y Amazon ECS**.