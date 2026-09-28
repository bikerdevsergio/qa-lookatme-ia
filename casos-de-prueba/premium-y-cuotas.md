# Casos de prueba — Premium y cuotas

## CP-01 — Límite diario de outfits (free)
**Pasos:** Con un usuario free, generar 5 outfits en el mismo día
(incluyendo ajustes de un turno, ej. "quítale el cinturón" — cada ajuste
también cuenta).
**Esperado:** Las primeras 5 generaciones funcionan. La sexta responde
HTTP 402 con un mensaje claro (no un error genérico/técnico) invitando a
esperar al día siguiente o pasarse a premium.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-02 — Límite diario de pruebas virtuales (free)
**Pasos:** Con un usuario free, hacer 2 pruebas virtuales en el mismo día.
**Esperado:** Las primeras 2 funcionan, la tercera responde 402 con
mensaje claro.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-03 — Usuario premium sin límite
**Pasos:** Con un usuario con `premium_until` futuro, generar más de 5
outfits y más de 2 pruebas virtuales en el mismo día.
**Esperado:** Todas las generaciones funcionan, sin bloqueo.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-04 — (ELIMINADO 2026-09-02) Otorgamiento automático a los primeros 50
Este caso ya no aplica — el trigger `grant_launch_premium` se borró de la
base (Sergi decidió priorizar ingresos reales sobre el incentivo de
lanzamiento). Ver `../../01-requisitos/05-monetizacion.md` y CLAUDE.md >
Plan de lanzamiento cerrado.

## CP-04b — Ningún usuario nuevo recibe premium automático
**Pasos:** Registrar un usuario nuevo cualquiera (completando el
onboarding) y revisar el campo `premium_until` en Supabase.
**Esperado:** `premium_until` queda `null` — entra como free sin
excepción, sin importar cuántos usuarios existan en la tabla.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-06 — El contador se resetea al día siguiente
**Pasos:** Agotar la cuota free de outfits un día, esperar al día
siguiente (o cambiar fecha del sistema en un entorno de prueba), intentar
generar de nuevo.
**Esperado:** El límite se resetea, la generación funciona.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:**
