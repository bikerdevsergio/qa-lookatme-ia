# Casos de prueba — Closet digital

## CP-01 — Agregar prenda
**Pasos:** Home → agregar prenda → tomar foto (o galería) → elegir
categoría, color, tela, ocasión → guardar.
**Esperado:** La prenda aparece en el listado del closet con su
miniatura, sin recargar la app.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-01b — IA detecta tipo Y color al elegir la foto (E3-03)
**Pasos:** Agregar prenda nueva → tomar/elegir foto → esperar el análisis
(indicador de carga en el campo Color).
**Esperado:** Se prellenan Color Y Categoría con lo que detectó la IA
(antes solo detectaba color). Ambos campos siguen siendo editables.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-01c — Tipo de prenda personalizado (E3-05)
**Pasos:** En el dropdown de Categoría, elegir "+ Nuevo tipo..." y
escribir algo que no esté en la lista (ej. "chaqueta de cuero con
tachas") → guardar.
**Esperado:** Se guarda con ese texto exacto como categoría. Al volver a
abrir esa prenda para editar, el dropdown muestra "+ Nuevo tipo..."
seleccionado con el texto ya cargado (no se pierde ni se rompe por no
estar en la lista fija).

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-01d — Ocasión personalizada (E3-07)
**Pasos:** En el dropdown de Ocasión, elegir "+ Otra ocasión..." y
escribir algo como "cita amorosa" → guardar.
**Esperado:** Mismo comportamiento que CP-01c pero para ocasión. Intentar
guardar con "+ Otra ocasión..." seleccionado y el campo de texto vacío
debe bloquear con el error correspondiente.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-01e — Selector de color hexadecimal (E3-06) — ❌ NO CONSTRUIDO TODAVÍA
**Nota:** este caso queda para cuando se construya — hoy el color sigue
siendo un `TextField` simple, no un selector de color con recorte de la
foto. No marcar como fallo si no existe todavía, solo confirmar que
sigue pendiente en la matriz.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-02 — Editar prenda existente
**Pasos:** Abrir una prenda ya guardada → cambiar la foto y/o el tipo,
color → guardar.
**Esperado:** Los cambios se reflejan de inmediato en el listado y al
volver a abrir la prenda.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-03 — Eliminar prenda
**Pasos:** Abrir una prenda → eliminar → confirmar.
**Esperado:** Desaparece del listado. Verificar en Supabase Storage que el
archivo también se borró (no queda huérfano).

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-04 — Marcar como favorita
**Pasos:** Marcar una prenda como favorita, filtrar/ver solo favoritas.
**Esperado:** Se puede desmarcar igual de fácil; el filtro de favoritas
muestra solo las marcadas.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-05 — Closet sin límite
**Pasos:** Agregar más de 100 prendas (o simular con datos de prueba).
**Esperado:** No hay bloqueo ni mensaje de límite alcanzado (diferencial
explícito vs Acloset, que limita a 100 en su plan free).

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-06 — Listado usa miniatura, no foto full
**Pasos:** Con 20+ prendas cargadas, medir cuánto tarda en cargar el
listado del closet (o revisar en devtools de red qué tamaño de imagen se
está pidiendo).
**Esperado:** Se piden las miniaturas (`thumbnail_path`, ~40KB), no las
fotos full (~200KB) — importante para no agotar el plan Free de Supabase
antes de tiempo (ver `TODO:ESCALA` en el código).

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:**
