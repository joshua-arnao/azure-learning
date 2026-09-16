# Create and Manage Organizations

## Crear una organización

### Opción A: Crear una organización NUEVA (recomendada)
Perfil → **Your organizations** → **New organization**

### Opción B: Convertir tu cuenta personal en organización
Botón "Turn into an organization" — ⚠️ **IRREVERSIBLE**:
- Tu username pasa de cuenta personal a organización
- Todos tus repos pasan a pertenecer a la organización
- NO puedes volver a la cuenta personal anterior

## Planes de organización

| Plan | Precio | Incluye |
|:---|:---:|:---|
| **Free** | Gratis | 2,000 min/mes CI/CD (privados), ilimitado en públicos. 500 MB almacenamiento de paquetes (privados), ilimitado en públicos |
| **Team** | $4 USD/usuario/mes | Todo lo anterior + toggle on/off de: Codespaces, ramas protegidas, múltiples revisores en PR, draft PRs, Pages, Wikis. 3,000 min/mes CI/CD, 2 GB almacenamiento de paquetes |
| **Enterprise** | Desde $21 USD/usuario/mes | Gestión centralizada de política/facturación de varias organizaciones. SLA 99.9% uptime (máx. ~42 min de downtime/mes). Seguridad y cumplimiento avanzados |

> **GitHub Pages**: aloja un sitio web estático a partir de un repo
> (ej. cómo Microsoft Learn/Wiki alojan documentación).

## Enterprise — funciones de identidad avanzadas

- **Managed users**: la empresa posee y controla las cuentas de usuario
- **Provisioning desde IdP** (Identity Provider): username, perfil, organización y acceso a repos se gestionan desde el proveedor de identidad. Ejemplos de IdP: **AD FS, Entra ID, Okta, OneLogin, PingOne, Shibboleth**
- **SSO con SAML**: GitHub redirige al IdP para autenticar, y regresa
  autenticado a GitHub
- **Team sync**: sincroniza un equipo de GitHub con un equipo del IdP
  — actualizar en el IdP se refleja automáticamente en GitHub

> Detalle técnico si usas **Entra ID**: requiere rol Global o
> Privileged Administrator, con permisos habilitados de SSO SAML,
> lectura de membresías de grupo completas, lectura de perfiles de
> usuario completos, y sign-in/lectura de perfil.
>
> Okta y Entra ID están disponibles solo en tenants comerciales — NO
> en government cloud.

## Formas de hospedar Enterprise
- **GitHub Enterprise Cloud**: en internet, región específica, subdominio único
- **GitHub Enterprise Server**: self-hosted (tú lo alojas)

## Creando la organización — pasos
1. Elegir plan (ej. Free)
2. Nombre de la organización
3. Email de contacto
4. Indicar si pertenece a una cuenta personal o a una empresa/institución
   (y su nombre, si aplica)
5. Extras opcionales: ej. **GitHub Copilot Business**
6. Revisar y aceptar el Customer Agreement + Privacy Statement
7. (Opcional) Agregar miembros — buscar por username, nombre o email
   > Una organización admite miembros ilimitados, aunque puede haber
   > algo de lentitud pasando los 100,000 miembros.


## Configuración general de la organización (tab "General")
- Email público, redes sociales, sitio web, descripción
- Subir foto/logo
- **Danger Zone**: renombrar, archivar o **eliminar** la organización

> Visibilidad de settings: SOLO los **Owners** y **Billing managers**
> pueden ver TODOS los ajustes de la cuenta de organización.

## Límite importante
Una organización puede tener como máximo **100,000 repositorios**.

## Resumen en una línea
Crear una organización nueva (no convertir tu cuenta personal, que es irreversible) te da un espacio separado con planes escalables (Free/Team/Enterprise), y Enterprise agrega gestión de identidad centralizada (SSO/SAML, IdP, Team sync) para control corporativo real.