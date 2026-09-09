# Use Security Features like Dependabot

## Dónde vive todo esto
Pestaña **Security** del repositorio → vista general (Overview).

## Overview — qué muestra
- Alertas de seguridad activas
- Permite activar/desactivar/editar la **Security Policy** (un archivo `.md` para informar a los usuarios sobre el estado de seguridad del repo)

## Las 3 funciones principales bajo "Security"

| Función | Qué hace |
|:---|:---|
| **Private vulnerability reporting** | Permite que alguien reporte una vulnerabilidad a los owners/maintainers de forma PRIVADA (no pública, evita exponer el fallo antes de arreglarlo) |
| **Dependabot alerts** | Detecta vulnerabilidades en las **dependencias** de tu proyecto (librerías de las que depende tu código — ej. lo que está en `package.json`, `pom.xml`, etc.) |
| **Code scanning alerts** | Encuentra vulnerabilidades y errores EN TU PROPIO código (no en dependencias) que podrían ser explotados |
| **Secret scanning alerts** | Detecta si API keys, tokens o credenciales quedaron expuestas por error en el código |


## Dependabot — las 3 cosas que monitorea

Se activa desde: **Settings del repo → Advanced Security**

| Función | Qué hace | Requisito previo |
|:---|:---|:---|
| **Dependency graph** | Mapea y muestra las dependencias del proyecto | Base para las otras dos |
| **Dependabot alerts** | Avisa sobre vulnerabilidades conocidas en dependencias | Requiere Dependency graph activo |
| **Dependabot security updates** | Genera automáticamente PRs para actualizar dependencias vulnerables (se puede agrupar todo en un solo PR) | Requiere Dependency graph + Dependabot alerts activos |
| **Version updates** | Mantiene dependencias al día en general (no solo por seguridad) | — |


## Configuración fina de las alertas Dependabot
Ícono de rueda (⚙️) junto a Dependabot alerts, permite:
- **Descartar (dismiss)** alertas de bajo impacto (ej. solo relevantes para desarrollo, no para producción)
- **Excluir dependencias específicas** del escaneo, para reducir ruido
- **Crear reglas personalizadas**


## CodeQL (Code Scanning)
- Disponible para repos públicos y para repos de organizaciones con **GitHub Code Security** habilitado
- Dos modos:
    - **Default setup**: configuración lista para usar
    - **Advanced setup**: personalizar el workflow de escaneo
- También se puede correr vía **CLI** desde un sistema de CI externo
- Se pueden agregar herramientas de escaneo de terceros además de CodeQL
- **Copilot autofix**: corrección automática sugerida por Copilot, disponible tanto para alertas de CodeQL como de terceros
- Se puede ajustar la **severidad** que hace fallar el scan:
    - Default: `High or higher` para alertas de seguridad,
      `Errors only` para alertas estándar

## Secret Protection
- Activa la búsqueda de secretos expuestos en repos públicos
- Puede **bloquear commits** que contengan secretos detectados
- **Desactivado por defecto** — hay que activarlo manualmente

## Resumen en una línea
La pestaña Security centraliza 4 líneas de defensa: reportes privados de vulnerabilidades, Dependabot (vulnerabilidades en dependencias), Code Scanning/CodeQL (vulnerabilidades en tu propio código), y Secret Scanning (credenciales filtradas), la mayoría se configura y activa desde Settings → Advanced Security.