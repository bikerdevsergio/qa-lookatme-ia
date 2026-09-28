# QA en LookAtMe.ia — Case Study

> Evidencia del proceso de QA manual que diseñé y ejecuté para **LookAtMe.ia**, una app móvil de moda personal con IA (Flutter + Supabase + backend en Cloud Run), producto propio en desarrollo activo de **RaccoonDev**.
>
> ⚠️ Este repositorio contiene únicamente artefactos de QA (casos de prueba, checklist, informes de error). El código fuente de la app es privado por tratarse de un producto comercial en desarrollo — lo que se comparte aquí es el **proceso y la evidencia de calidad**, no la propiedad intelectual del producto.

## El problema

LookAtMe.ia es una app en desarrollo activo, con releases frecuentes de APKs de prueba a testers reales. Muy temprano en el proyecto, una versión (v1.4) "compiló exitosamente" y aun así **se cerraba sola al abrir en el teléfono** — compilar no es lo mismo que funcionar. Ese incidente fue el disparador para formalizar un proceso de QA manual obligatorio antes de cualquier entrega, en vez de confiar en que "si compila, funciona".

## Mi rol

Diseñé y ejecuté el proceso de QA completo para este proyecto, como parte del proceso de desarrollo de 5 etapas de RaccoonDev (Requisitos → Diseño → Desarrollo → **QA** → Producción):

- Definí un **smoke test obligatorio** (5 minutos, checklist fijo) que corre antes de entregar cualquier APK a un tester — si algo falla, el APK no sale, sin excepción.
- Diseñé **casos de prueba estructurados** por módulo (pasos, resultado esperado), trazables a los requisitos de la matriz del proyecto.
- Ejecuté rondas de pruebas manuales en dispositivo real (Honor X7) — no solo revisión de código ni emulador.
- Reporté cada hallazgo con una plantilla formal: qué esperabas, qué pasó, pasos para reproducir, severidad, dispositivo.

## Estrategia de testing

**Por qué manual y no automatizado en este proyecto:** LookAtMe.ia depende fuertemente de resultados generados por IA (outfits, detección de prendas, recomendaciones de estilo) que varían por diseño — validar "¿tiene sentido esta recomendación de moda?" requiere juicio humano, no solo comparar un resultado esperado fijo. El proceso automatiza lo que sí es determinístico (smoke test de build, checklist de regresión) y deja la validación de UX/IA a pruebas manuales estructuradas y trazables.

**Cobertura:** 14 sprints de QA, ~83 casos de prueba documentados, sobre 9 módulos: autenticación/onboarding, closet digital, generador de outfits, prueba virtual, perfil de estilo, perfil y cuenta, premium/cuotas, legal y consentimiento, y monetización (AdMob).

## Resultados

**20 bugs encontrados y corregidos** en pruebas de dispositivo real, clasificados por severidad:

| Severidad | Cantidad | Ejemplo |
|---|---|---|
| 🔴 Crítico | 2 | Registro de consentimiento legal no se guardaba en base de datos |
| 🟠 Alto | 4 | Orden de pantallas de onboarding incorrecto; la IA no sostenía ajustes previos al generar outfits |
| 🟡 Medio | 13 | Filtros faltantes, copy inconsistente con la épica, catálogo no visible |
| ⚪ Cosmético | 1 | Botón duplicado en estado vacío |

Ver el detalle completo, con pasos de reproducción y trazabilidad a cada caso de prueba, en [`informes-de-error/bugs-encontrados.md`](informes-de-error/bugs-encontrados.md).

Dos ejemplos que muestran el tipo de bug que este proceso está diseñado para atrapar — no solo errores visuales, sino fallas de comportamiento y de cumplimiento:

- **[lookatmeia005 — Crítico]** El consentimiento informado se aceptaba en la UI pero **nunca quedaba registrado en la base de datos** (`consent_records` vacía). Sin este hallazgo, la app no habría podido demostrar que el usuario aceptó los términos — un problema legal, no solo técnico.
- **[lookatmeia020 — Crítico]** Una regla de producto explícita dice que la app **no es un chatbot de propósito general** — los ajustes deben ser por opciones cerradas de UI. En pruebas, pedir un ajuste en texto libre hizo que la IA ejecutara una acción distinta a la solicitada, violando esa regla de diseño.

## Cómo se organiza este repositorio

```
casos-de-prueba/       casos de prueba por módulo (pasos + resultado esperado)
informes-de-error/     los 20 bugs encontrados, con severidad y trazabilidad
checklist-comprobacion.csv   checklist de verificación por requisito
smoke-test.md           gate obligatorio antes de entregar un APK
```

## Herramientas y proceso

- Documentación estructurada en Markdown, versionada junto al proceso de desarrollo.
- Plantilla fija de informe de error (caso relacionado, esperado vs. real, pasos, dispositivo, severidad) para que cada bug sea reproducible por cualquiera del equipo, no solo por quien lo encontró.
- Registro y seguimiento en un sistema de gestión interno construido por el equipo (proceso de 5 etapas: Requisitos → Diseño → Desarrollo → QA → Producción).

## Próximos pasos

- Incorporar automatización con **Playwright/Selenium** para los flujos deterministas (autenticación, navegación, checklist de regresión), dejando la validación de resultados de IA a QA manual estructurado.
- Agregar evidencia visual (capturas/GIFs) a los informes de error.
- Integrar CI/CD con GitHub Actions para las pruebas automatizadas que se incorporen.

---

*Sergio Ávila — QA Automation Engineer · [github.com/bikerdevsergio](https://github.com/bikerdevsergio)*
