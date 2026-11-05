# Casos de prueba — Generador de outfits (Módulo 3)

## CP-01 — Modo automático
**Pasos:** Ir al generador, elegir modo automático, seleccionar ocasión +
clima + ánimo, generar.
**Esperado:** Se muestra una imagen del outfit compuesto con prendas
reales del closet del usuario (no genéricas) + consejo de moda en texto,
específico a esas prendas (no un consejo genérico tipo "combina bien los
colores").

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-02 — Modo manual
**Pasos:** Modo manual, seleccionar prendas específicas (ej. una camisa y
un pantalón puntuales), generar.
**Esperado:** El outfit generado usa exactamente esas prendas
seleccionadas, no otras del closet.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-03 — Ajuste de un turno (no es chat abierto)
**Pasos:** Tras generar un outfit, usar la opción de ajuste (ej. "quítale
el cinturón" o similar, desde una opción cerrada de la UI, no un campo de
texto libre).
**Esperado:** Se regenera solo con ese ajuste aplicado. **No debe existir
un campo de texto libre estilo chat** — la interacción es por opciones
cerradas (regla de producto: la app no es un chat de
propósito general).

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-04 — El outfit usa el avatar/cuerpo real del usuario
**Pasos:** Generar un outfit con un usuario que tiene foto corporal
cargada.
**Esperado:** La imagen resultante corresponde reconociblemente al cuerpo
del usuario, no a una figura genérica.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-05 — Filtros afectan el resultado
**Pasos:** Generar un outfit para "trabajo" + clima frío, luego otro para
"salida" + clima cálido, mismo closet.
**Esperado:** Las combinaciones son visiblemente distintas y coherentes
con cada filtro.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-06 — Historial evita repetir "el uniforme"
**Pasos:** Generar varios outfits seguidos en modo automático con el
mismo closet.
**Esperado:** No repite exactamente la misma combinación de forma
consecutiva de manera obvia.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-07 — Límite de cuota (ver también `premium-y-cuotas.md`)
**Pasos:** Ver CP-01 de `premium-y-cuotas.md`.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:**
