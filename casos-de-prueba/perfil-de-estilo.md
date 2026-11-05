# Casos de prueba — Perfil de estilo (E4)

Diseño en documentos internos del proyecto; el rediseño de fusión +
catálogo + E4-02/E4-03 surgió del informe `look006` (2026-09-04).

**Nota:** CP-01 a CP-07 (abajo) prueban el flujo que YA existe. CP-08 en
adelante prueban lo nuevo del rediseño (catálogo, fusión de los dos
botones de Perfil, E4-02, E4-03) — no probar hasta que esté construido.

## CP-01 — Crear el perfil por primera vez (E4-01, E4-04, E4-05)
**Pasos:** Perfil → "Mi perfil de estilo" (con un usuario que todavía no
tiene uno) → subir una foto de referencia (un outfit que te guste, no
necesariamente tu cuerpo) → esperar el análisis.
**Esperado:** Aparece un borrador editable en formato markdown corto
("Estilo general", "Colores predominantes", "Patrón notado"). El botón
"Guardar" solo persiste después de que lo revises/edites y confirmes —
nunca se guarda automático.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-02 — La foto de referencia no se guarda
**Pasos:** Después de CP-01, revisar Supabase Storage.
**Esperado:** No debe existir ningún archivo nuevo correspondiente a esa
foto — es efímera, se analiza y se descarta (igual que la foto de prenda
externa en prueba virtual).

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-03 — Actualizar estilo con opciones guiadas (E4-01)
**Pasos:** Con un perfil ya creado, en "Mi perfil de estilo" elegir un
chip de dirección ("Más formal", "Más streetwear", "Más a la moda", "Más
elegante").
**Esperado:** Aparece un nuevo borrador propuesto, distinto al actual,
coherente con la dirección elegida. No se guarda hasta confirmar.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-04 — Dirección personalizada con texto corto (E4-01)
**Pasos:** Elegir "Otra..." y escribir algo corto como "quiero verme más
poderoso" o "voy a una fiesta, quiero impresionar" → Proponer cambio.
**Esperado:** El borrador propuesto refleja esa dirección específica, no
un cambio genérico.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-05 — El perfil de estilo influye en el consejo de moda
**Pasos:** Con un perfil de estilo guardado (ej. "gótico, tonos oscuros"),
generar un outfit (Módulo 3) y leer el consejo.
**Esperado:** El tono/estética del consejo es coherente con el perfil
guardado — no genérico ni contradictorio con lo que dice el perfil.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-06 — El perfil de estilo influye en qué prendas elige el modo automático
**Pasos:** Con el mismo perfil de estilo marcado, generar un outfit en
modo automático varias veces.
**Esperado:** Las prendas elegidas tienden a ser coherentes con el estilo
guardado (si el closet tiene variedad), no aleatorias sin relación.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-07 — Consistencia entre generaciones (el problema original que motivó esto)
**Pasos:** Generar 2-3 outfits o consejos seguidos, mismo usuario, mismo
closet, sin cambiar el perfil de estilo entre medio.
**Esperado:** La IA no "cambia de opinión" sobre el estilo del usuario
entre una generación y otra (ej. no lo trata como gótico en un consejo y
como formal en el siguiente sin que nada haya cambiado).

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-08 — Un solo punto de entrada en Perfil (E4-07)
**Pasos:** Ir a Perfil.
**Esperado:** Existe UN SOLO botón relacionado con estilo ("Mi estilo")
— ya no hay dos botones separados ("Cambiar mi estilo" y "Mi perfil de
estilo"). Toca a ese único botón y lleva al flujo completo (catálogo +
foto/texto + IA).

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 

## CP-09 — Catálogo de estilos navegable y con buscador (E4-06)
**Pasos:** Entrar a "Mi estilo" → revisar la primera pantalla.
**Esperado:** Se ve una grilla con los estilos del catálogo (imagen +
nombre, ej. Streetwear, Minimalista, Boho, Old Money...), con un campo
de búsqueda/filtro arriba que funciona escribiendo parte del nombre.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 

## CP-10 — Elegir un estilo del catálogo es opcional
**Pasos:** En la pantalla del catálogo, sin tocar ningún estilo, buscar
la forma de continuar solo con foto y/o texto (como ya funciona hoy).
**Esperado:** Se puede saltar el catálogo sin elegir nada y seguir el
flujo igual que antes (foto de referencia y/o chips de dirección).

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 

## CP-11 — Elegir un estilo del catálogo influye en el borrador
**Pasos:** Tocar un estilo del catálogo (ej. "Old Money"), sin subir
foto ni escribir texto, avanzar.
**Esperado:** El borrador propuesto por la IA refleja claramente ese
estilo elegido (lujo silencioso, prendas atemporales, sin logos).

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 

## CP-12 — Elegir un estilo actualiza style_preference
**Pasos:** Elegir un estilo del catálogo, completar el flujo y guardar.
Revisar en Supabase la tabla `profiles`.
**Esperado:** `style_preference` queda con el nombre del estilo elegido
del catálogo, además de `style_profile` con el texto en markdown.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 

## CP-13 — Sugerencia de prendas del closet que combinan (E4-02)
**Pasos:** Con un closet que tenga prendas que calcen con el estilo
propuesto, llegar a la pantalla de revisión del borrador.
**Esperado:** Debajo/al lado del borrador aparece una grilla con esas
prendas del closet del usuario — no genéricas, prendas reales que ya
tiene.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 

## CP-14 — Generar imagen del avatar si no hay match en el closet (E4-03)
**Pasos:** Con un closet SIN ninguna prenda que combine con el estilo
propuesto, llegar a la pantalla de revisión.
**Esperado:** En vez de la grilla de CP-13, aparece un botón para
generar una imagen mostrando cómo se vería el usuario con ese estilo —
la imagen muestra al PROPIO usuario (su avatar), nunca una foto de otra
persona ni una imagen genérica bajada de internet.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 

## CP-15 — Cuota mensual de la generación de imagen (E4-03)
**Pasos:** Repetir CP-14 una segunda vez en el mismo mes calendario, con
una cuenta free.
**Esperado:** La segunda vez no genera una imagen nueva, muestra un
aviso de límite mensual alcanzado (1 vez/mes en plan free). Con una
cuenta premium, no hay límite.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 
