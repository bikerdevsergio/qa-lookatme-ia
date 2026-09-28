# Informes de error — LookAtMe.ia

20 bugs reales encontrados durante pruebas manuales en dispositivo (Honor X7), entre 2026-09-05 y 2026-09-11. Todos corregidos y verificados. Clasificados por severidad y trazables a su caso de prueba.

**Resumen por severidad:** 2 críticos · 4 altos · 13 medios · 1 cosmético — 20/20 corregidos.

---

## Críticos

### [lookatmeia005] `consent_records` no guarda versión y fecha
**Caso relacionado:** CP-04 — legal-y-consentimiento
**Esperado:** Existe una fila con `policy_version` y `accepted_at` poblados para ese usuario.
**Encontrado:** En Supabase no existía ningún registro del consentimiento aceptado.
**Pasos:** Completar el consentimiento con un usuario de prueba, revisar la tabla `consent_records` en Supabase.
**Por qué importa:** Es un requisito legal/de compliance (consentimiento informado) — si no queda registrado, la app no puede demostrar que el usuario aceptó los términos.
**Estado:** Corregido (mismo día).

### [lookatmeia020] Ajuste de un turno se comporta como chat abierto
**Caso relacionado:** CP-03 — generador-outfits
**Esperado:** La interacción de ajuste es por opciones cerradas de UI, no un campo de texto libre estilo chat (regla de producto explícita: la app no es un chatbot de propósito general).
**Encontrado:** Al pedir "agrega el pantalón que recomiendas" en texto libre, la IA no ejecutó la acción — solo cerró la chaqueta.
**Pasos:** Tras generar un outfit, usar la opción de ajuste desde una opción cerrada de la UI.
**Por qué importa:** Bug de comportamiento de IA que rompe una regla de diseño de producto explícita, no solo un glitch visual.
**Estado:** Corregido.

---

## Altos

### [lookatmeia001] Orden del flujo de onboarding incorrecto
**Caso relacionado:** CP-06 — auth-onboarding
**Esperado:** privacidad → foto de estilo → foto corporal → pantalla de pregunta de estilo → formulario de registro.
**Encontrado:** El flujo saltaba directo de foto corporal al formulario de registro, sin la pantalla de pregunta de estilo.
**Estado:** Corregido.

### [lookatmeia003] Modo automático del generador de outfits — opciones cerradas y "sorpréndeme" de más
**Caso relacionado:** CP-01 — generador-outfits
**Encontrado:** Las opciones de ocasión debían sugerir pero también aceptar entrada personalizada (igual clima y ánimo); el interruptor "sorpréndeme" sobraba en modo automático.
**Estado:** Corregido — dio origen a los fixes de lookatmeia004/006/007.

### [lookatmeia015] Camino sin referencia no deja elegir una dirección con la IA
**Caso relacionado:** CP-03 — perfil-de-estilo
**Encontrado:** Se había eliminado la opción de interactuar con la IA sobre lo que el usuario buscaba.
**Estado:** Corregido.

### [lookatmeia019] Ajuste de turno no sostiene cambios previos
**Caso relacionado:** CP-03 — generador-outfits
**Encontrado:** Al pedir un segundo ajuste (cambiar los zapatos), se perdía el ajuste anterior (el pantalón elegido) en vez de mantenerse.
**Estado:** Corregido.

---

## Medios (13) — resumen

| Código | Módulo | Título |
|---|---|---|
| lookatmeia002 | auth-onboarding | Pantalla "cuál es tu estilo" se veía después del registro, no antes |
| lookatmeia004 | generador-outfits | Modo manual — ocasión/clima/ánimo sin opción de texto personalizado |
| lookatmeia006 | perfil-y-cuenta | Cambiar foto corporal no reemplazaba la anterior (quedaba huérfana en Storage) |
| lookatmeia007 | generador-outfits | Faltaban sugerencias de clima y estado de ánimo |
| lookatmeia008 | perfil-de-estilo | Naming y copy inconsistentes con la épica (mezclaba textos de onboarding) |
| lookatmeia009 | perfil-de-estilo | Copy de "actualizar estilo" no correspondía a la épica |
| lookatmeia010 | perfil-de-estilo | Catálogo de estilos no visible ni explicado |
| lookatmeia011 | perfil-de-estilo | Catálogo pasó a obligatorio cuando debía ser opcional |
| lookatmeia012 | perfil-de-estilo | No se podía avanzar sin elegir estilo del catálogo (requisito corregido a obligatorio) |
| lookatmeia014 | perfil-de-estilo | Orden visual confuso en "Cambiar estilo" |
| lookatmeia016 | perfil-de-estilo | Botón "Guardar este estilo" mal posicionado |
| lookatmeia017 | perfil-de-estilo | La IA no mantenía el concepto de estilo original al afinar con un ajuste corto |
| lookatmeia018 | closet | Faltaba filtro de favoritos (se podían marcar pero no filtrar) |

---

## Cosméticos

### [lookatmeia013] Botón flotante duplicado en closet vacío
**Encontrado:** Dos botones para la misma acción ("Agrega tu primera prenda" central + botón flotante).
**Estado:** Corregido.

---

*Todos los bugs fueron reportados con plantilla estructurada (caso de prueba relacionado, esperado vs. real, pasos de reproducción, dispositivo, severidad) y quedaron registrados en el sistema interno de gestión de QA de RaccoonDev antes de pasar a corrección.*
