# Understand the Principles of DevOps

---

## 1. ¿Qué es DevOps?

**DevOps = Development + Operations.** Es un conjunto de prácticas que permite la **entrega de software** de forma más rápida, confiable y colaborativa, uniendo dos áreas que tradicionalmente trabajaban separadas: quienes desarrollan el código y quienes lo operan/mantienen en producción.

## 2. Los 4 pilares/principios de DevOps

| Principio                            | Qué significa                                                                                                                                                                                                 |
|:-------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Colaboración**                     | Un equipo con un **objetivo compartido**, con visibilidad de las prioridades de todos, no equipos aislados trabajando en silos.                                                                               |
| **Automatización**                   | Automatizar tareas como **pruebas, implementación (deployment) y supervisión (monitoring)** — las hace más rápidas y más precisas que hacerlas manualmente. En GitHub, esto se logra con **GitHub Actions**.  |
| **Integración Continua (CI)**        | Fusionar cambios de código en un **repositorio compartido** frecuentemente, permitiendo **construir (build)** el proyecto y **ejecutar pruebas (test)** de forma constante.                                   |
| **Entrega/Despliegue Continuo (CD)** | Preparar los cambios de código para que avancen fluidamente de **desarrollo → pruebas → producción**.                                                                                                         |

### Por qué "Commits más frecuentes" es una práctica recomendada

> Commits pequeños y frecuentes permiten **detectar errores más rápido** y **reducen el rango de código donde puede estar el error** — si rompes algo con un commit gigante que toca 50 archivos, es mucho más difícil encontrar la causa que si cada commit es pequeño y aislado.

## 3. Beneficios de aplicar DevOps

- Mejora la **colaboración**
- Aumenta la **eficacia**
- Mejora las **pruebas**, la **fiabilidad**, la **calidad** y la **seguridad**
- **Acelera** la puesta a disposición del software para los usuarios finales

---

## 4. El Ciclo de Vida de DevOps (DevOps Lifecycle)

```
1. PLAN         →  ¿Qué vas a hacer?
2. CODE         →  Creas tu código
3. BUILD        →  Se construye el proyecto (parte de CI)
4. TEST         →  Se ejecutan pruebas (parte de CI)
5. RELEASE      →  Se libera la versión (parte de CI)
6. DEPLOY       →  Se despliega a producción (parte de CD)
7. OPERATE      →  El software funciona en producción
8. MONITOR      →  Se supervisa el comportamiento en producción
```

**Agrupación conceptual del ciclo:**

| Fase                       | Bloque al que pertenece                 |
|:---------------------------|:----------------------------------------|
| Plan → Code                | Trabajo de desarrollo individual/equipo |
| Build → Test → Release     | **Continuous Integration (CI)**         |
| Deploy → Operate → Monitor | **Continuous Delivery/Deployment (CD)** |

> El ciclo es **continuo y circular**, lo que se aprende en "Monitor" retroalimenta la siguiente fase de "Plan", por eso DevOps suele representarse como un símbolo de infinito (∞), no como una línea recta.

## Resumen visual (infinito DevOps)

```
        PLAN ──── CODE
        ╱                ╲
  MONITOR                BUILD
      │                    │
   OPERATE              TEST
       ╲                ╱
        DEPLOY ──── RELEASE
```

## Punto clave para el examen

**CI (Continuous Integration)** cubre: **Build + Test + Release** — es decir, todo lo relacionado con integrar y validar el código.
**CD (Continuous Delivery/Deployment)** cubre: **Deploy + Operate + Monitor** — todo lo relacionado con llevar ese código validado hasta el usuario final y mantenerlo funcionando.

Esta distinción CI vs CD es la base para entender **GitHub Actions**, que se ve en el siguiente tema de esta sección.