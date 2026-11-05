# Casos de prueba — Premium y cuotas

## CP-01 — Límite diario de outfits (free)
**Pasos:** Con un usuario free, generar 2 outfits en el mismo día
(incluyendo ajustes de un turno, ej. "quítale el cinturón" — cada ajuste
también cuenta).
**Esperado:** Las 2 primeras generaciones funcionan. La tercera responde
HTTP 402 con un mensaje claro (no un error genérico/técnico) invitando a
esperar al día siguiente o pasarse a premium.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 

## CP-02 — Límite diario de pruebas virtuales (free)
**Pasos:** Con un usuario free, hacer 1 prueba virtual en el mismo día y
luego intentar una segunda.
**Esperado:** La primera funciona, la segunda responde 402 con mensaje claro.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 

## CP-03 — Usuario premium: cupo mensual (no ilimitado)
**Pasos:** Con un usuario con `premium_until` futuro, superar los límites
free del día (más de 2 outfits y más de 1 prueba virtual).
**Esperado:** Las generaciones siguen funcionando hasta agotar el cupo
mensual premium (50 outfits, 20 pruebas virtuales); al superarlo responde
402 con mensaje claro.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 

## CP-04 — (ELIMINADO 2026-09-02) Otorgamiento automático a los primeros 50
Este caso ya no aplica: el product owner decidió eliminar el incentivo de
lanzamiento y el trigger asociado se borró de la base.

## CP-04b — Ningún usuario nuevo recibe premium automático
**Pasos:** Registrar un usuario nuevo cualquiera (completando el
onboarding) y revisar el campo `premium_until` en Supabase.
**Esperado:** `premium_until` queda `null` — entra como free sin
excepción, sin importar cuántos usuarios existan en la tabla.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 

## CP-06 — El contador se resetea al día siguiente
**Pasos:** Agotar la cuota free de outfits un día, esperar al día
siguiente (o cambiar fecha del sistema en un entorno de prueba), intentar
generar de nuevo.
**Esperado:** El límite se resetea, la generación funciona.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:**
