# CODE REVIEWS — MEJORES PRÁCTICAS

## 1. Tamaño del Pull Request (PR)
Preferir PRs PEQUEÑOS.
> ¿Qué resuelve? Un PR chico se revisa más rápido y con más
> atención real. Un PR gigante invita a revisiones superficiales
> ("looks good to me" sin leer a fondo) porque revisar 2000 líneas
> cansa y dispersa el foco del revisor.

## 2. Descripción clara del PR
El PR debe indicar QUÉ hace el cambio (no solo el título del ticket).
> Sin contexto, el revisor tiene que reconstruir la intención leyendo
> solo el diff — más lento y más propenso a que se le escape algo.

## 3. Criterios a evaluar al revisar código
Una checklist de aspectos a considerar en cada revisión:

| Aspecto                  | Pregunta que responde                                      |
|:-------------------------|:-----------------------------------------------------------|
| Seguridad                | ¿Introduce alguna vulnerabilidad?                          |
| Rendimiento              | ¿Es eficiente o agrega cuellos de botella?                 |
| Mantenibilidad           | ¿Otro dev lo puede entender/modificar después?             |
| Compatibilidad           | ¿Rompe algo existente (versiones, APIs)?                   |
| Escalabilidad            | ¿Aguanta crecer en uso/datos?                              |
| Usabilidad               | ¿Es claro de usar (API, función, endpoint)?                |
| Accesibilidad            | ¿Es usable por personas con discapacidad (si aplica a UI)? |
| Localización             | ¿Soporta distintos idiomas/regiones si es necesario?       |
| Legalidad y cumplimiento | ¿Cumple normativas/licencias/regulación?                   |
| Testeabilidad            | ¿Se puede probar fácilmente (unit/integration tests)?      |
| Documentación            | ¿Está documentado según lo que pide el equipo?             |

> Puede convertirse en una checklist fija adjunta a la plantilla del
> PR, para no depender de que cada revisor "se acuerde" de todo.

## 4. Rol del revisor
- Debe dar SUGERENCIAS, no solo señalar errores.
- Debe señalar problemas de forma clara y accionable.

## 5. ¿Quién revisa?
- **QA (Quality Assurance)**: útil emparejar un dev con alguien de
  QA — QA no necesariamente tiene mucha experiencia de código, pero
  aporta la mirada de calidad/casos de borde.
- **Devs Senior**: revisan código de devs junior — mentoría +
  control de calidad al mismo tiempo.
- **Equipos grandes**: puede haber VARIOS revisores en paralelo
  sobre el mismo PR, cada uno mirando ángulos distintos.