# Casos de prueba — Auth y Onboarding (E1)

Es el bloque más crítico: si esto falla, nadie más puede usar la app.
Dividido en sprints de prueba, cada uno con su ronda de informes de
error. El diseño del flujo (documento interno del proyecto) tuvo 4
revisiones a partir de estos hallazgos.

---

## Sprint 1 — 2026-09-03, orden original del onboarding

Primera ronda de pruebas, contra el orden implementado originalmente
(consentimiento → formulario nombre/edad/contraseña → fotos → medidas
en pantalla separada). Resultado: **2 informes de error**
(`look001`, `look002`) — el orden no era el que el product owner esperaba (fotos
antes del formulario, medidas y talla en el mismo formulario que la
cuenta). Ver `plantilla-informe-error look001.md` y `...look002.md`.

Esta ronda llevó a la Revisión 2 del diseño (orden corregido) — los
casos de prueba específicos de esta ronda quedaron reemplazados por
los de Sprint 2 abajo, ya no se repiten acá.

**Resultado del sprint:** ❌ bloqueante, no se pudo seguir probando
hasta corregir el orden.

---

## Sprint 2 — 2026-09-04 (mañana), orden corregido (Revisión 2)

**Orden probado:** login (pantalla de entrada) → Registrarte →
consentimiento → **foto de estilo (obligatoria)** → **foto de avatar
(obligatoria)** → **formulario único** (nombre, edad, email, contraseña,
medidas, talla — acá se crea la cuenta) → estilo preferido → tutorial →
commit final → home.

### CP-01 — Login es la pantalla de entrada (E1-01)
**Pasos:** Abrir la app sin sesión activa (desinstalar y reinstalar, o
cerrar sesión primero).
**Esperado:** La primera pantalla que se ve es "Iniciar sesión" (email +
contraseña + botón "Entrar"), NO una pantalla de bienvenida ni de
registro.

**Resultado:** [x] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado (confirmado 2026-09-02)

**Código del informe de error:** 

### CP-02 — Registro es la acción secundaria, lleva a consentimiento (E1-02)
**Pasos:** Desde la pantalla de login, tocar "¿No tienes cuenta?
Regístrate".
**Esperado:** Lleva a la pantalla de consentimiento (privacidad).

**Resultado:** [x] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado (confirmado 2026-09-03)

**Código del informe de error:** 

### CP-03 — Después de aceptar privacidad, pide la foto de estilo (no el formulario) — CORRIGE look001
**Pasos:** Aceptar el consentimiento.
**Esperado:** La siguiente pantalla es "Sube una foto de referencia de tu
estilo" — NO el formulario de registro. No hay botón "Omitir" (es
obligatoria).

**Resultado:** [x] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado (confirmado 2026-09-03)

**Código del informe de error:** 

### CP-04 — Después de la foto de estilo, pide la foto de avatar
**Pasos:** Subir/tomar la foto de estilo, esperar el análisis, revisar/
confirmar el borrador y guardar.
**Esperado:** La siguiente pantalla es "Tu foto corporal" (avatar) — no
hay botón "Omitir", es obligatoria.

**Resultado:** [x] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado (confirmado 2026-09-03)

**Código del informe de error:** 

### CP-05 — Formulario único con medidas y talla — CORRIGE look002
**Pasos:** Subir la foto de avatar y continuar.
**Esperado:** La siguiente pantalla es UN SOLO formulario largo con, en
este orden: Nombre, Edad, Email, Contraseña, y luego "Tus medidas"
(pecho, cintura, cadera, estatura, peso — los 5 obligatorios) y "Tu
talla habitual" (un campo opcional por cada categoría: camisa,
pantalón, vestido, zapatos, accesorio, otro). Todo en la misma
pantalla, con scroll — no en pantallas separadas.

**Resultado:** [x] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado (confirmado 2026-09-03)

**Código del informe de error:** 

### CP-06 — El formulario único es donde se crea la cuenta
**Pasos:** Completar el formulario del CP-05 y tocar "Registrarme".
**Esperado:** Recién acá se crea la cuenta (o se envía el correo de
confirmación si aplica). La siguiente pantalla es "¿Cuál es tu estilo?"
(la lista fija: casual/formal/urbano/etc.).

**Resultado:** [ ] Pasa &nbsp;&nbsp; [x] Falla &nbsp;&nbsp; [ ] No probado (2026-09-04)

**Código del informe de error:** look003 — corregido en Sprint 3, ver CP-14

### CP-07 — Nada se guarda hasta terminar todo el onboarding (E1-09) — CRÍTICO
**Pasos:** Completar estilo, avatar y el formulario único (nombre, edad,
email, contraseña, medidas, talla) — y ANTES de terminar "¿Cuál es tu
estilo?" o el tutorial, **cerrar la app por completo** (no solo
minimizar).
**Esperado:** Al volver a abrir la app y hacer login con ese mismo
correo, la app NO muestra el closet ni datos guardados — manda de nuevo
a la pantalla de consentimiento, como si nunca se hubiera registrado.
Verificar en Supabase que no exista fila en `profiles` ni
`body_measurements` para ese usuario (puede existir en Auth, eso sí es
esperado).

**Resultado:** [x] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado (2026-09-04 — nada se guarda, confirmado; nota: en la práctica esto pasaba SIEMPRE, no solo si se cerraba la app, porque CP-06/look003 hacía que el flujo real nunca llegara al commit final — corregido en Sprint 3)

**Código del informe de error:** 

### CP-08 — Commit único al terminar el onboarding (E1-09)
**Pasos:** Repetir el registro completo (mismo correo del CP-07 u otro
nuevo) y esta vez SÍ llegar hasta el final (tutorial → "Ir a mi closet").
**Esperado:** Se ve un loading breve en el botón final, y recién ahí
aparece el closet vacío. Verificar en Supabase que ahora SÍ existan:
`consent_records`, `profiles` (con nombre, edad, estilo, perfil de
estilo, foto de avatar, talla por categoría si se llenó),
`body_measurements`.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [x] Falla &nbsp;&nbsp; [ ] No probado (2026-09-04)

**Código del informe de error:** look004 — corregido en Sprint 3, ver CP-15/CP-16

### CP-09 — Usuario que ya completó el onboarding entra directo (E1-09)
**Pasos:** Con un usuario que ya terminó todo el onboarding alguna vez
(ej. el del CP-08), cerrar sesión y volver a iniciar sesión.
**Esperado:** Login lleva directo a `/home` (el closet), sin pasar por
ningún paso de onboarding.

**Resultado:** [x] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado (2026-09-04)

**Código del informe de error:** 

### CP-10 — Correo duplicado al registrarse (E1-12)
**Pasos:** Intentar registrarse con un correo que ya tiene cuenta
(completó el onboarding o no).
**Esperado:** Mensaje claro "Ese correo ya tiene una cuenta — inicia
sesión en vez de registrarte", con un botón "Ir a iniciar sesión" en vez
del error técnico genérico.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [x] Falla &nbsp;&nbsp; [ ] No probado (2026-09-04)

**Código del informe de error:** look005 — corregido en Sprint 3, ver CP-17

### CP-11 — Usuario con cuenta pero onboarding incompleto puede reintentar (E1-11)
**Pasos:** Con el usuario del CP-07 (tiene cuenta de Auth pero nunca
completó el perfil), ir a "Iniciar sesión" y entrar con ese
email/contraseña que ya había definido.
**Esperado:** El login funciona (la cuenta existe), y manda a repetir el
onboarding completo desde el consentimiento — sin pedir crear una cuenta
nueva ni mostrar error de "correo duplicado" en este camino.

**Resultado:** No aplica — caso inválido según el product owner (2026-09-04): "solo hay dos opciones, o te registras o no te registras", no hay un estado intermedio distinto que probar aparte de CP-07.

**Código del informe de error:** 

### CP-12 — SUPERADO por look006, ver `perfil-de-estilo.md`
**Reemplazado 2026-09-04:** este caso probaba "Cambiar mi estilo" como
la lista fija de 6 estilos guardando directo. El informe `look006`
mostró que el product owner espera algo mucho más completo (catálogo + IA), y la
decisión fue FUSIONAR esa pantalla con "Mi perfil de estilo" en un solo
flujo (requisito E4-07) — la
pantalla fija de 6 como entrada independiente de Perfil deja de existir,
así que este caso tal como estaba escrito ya no aplica. Los casos
nuevos que la reemplazan son CP-08 a CP-15 de `perfil-de-estilo.md`.

**Resultado:** No aplica — reemplazado por CP-08 a CP-15 de `perfil-de-estilo.md`

**Código del informe de error:** look006 (ver también `cambiar-estilo-rediseno.md`)

### CP-13 — Actualizar medidas desde Perfil sigue funcionando
**Pasos:** Perfil → "Actualizar mis medidas", cambiar un valor, guardar.
**Esperado:** Se guarda directo (pantalla de edición, ya no forma parte
del onboarding) y confirma con un mensaje.

**Resultado:** [x] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

**Resultado del sprint:** ❌ bloqueante — CP-06/CP-08/CP-10 fallaron
(look003, look004, look005), ningún registro real llegaba a completarse
con confirmación de email obligatoria. Llevó a la Revisión 3 del diseño
(staging en el backend).

---

## Sprint 3 — 2026-09-04 (en curso), fix de E1-13/E1-12 — v1.9.0+10

Vuelve a probar exactamente lo que falló en el Sprint 2, ahora con el
registro guardado en el backend (no en el dispositivo) cuando no hay
sesión todavía. Backend desplegado y probado con curl — falta la
verificación en dispositivo real.

### CP-14 — El registro llega hasta "¿Cuál es tu estilo?" sin interrupciones — corrige look003
**Pasos:** Completar el formulario único (CP-05) y tocar "Registrarme".
**Esperado:** Ya NO aparece ningún aviso de "confirma tu correo" en
este punto — se pasa directo a "¿Cuál es tu estilo?" y después al
tutorial, como si hubiera sesión.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 

### CP-15 — Al terminar el tutorial sin sesión, avisa y manda a login — corrige look004 (parte 1)
**Pasos:** Elegir un estilo preferido, avanzar el tutorial y tocar "Ir a
mi closet" (con una cuenta que todavía no confirmó el correo).
**Esperado:** Aparece el aviso "Te enviamos un email para confirmar tu
cuenta. Confírmalo y luego inicia sesión" y la app manda a
`/auth/login` — NO intenta entrar directo al closet sin sesión.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 

### CP-16 — Confirmar el correo e iniciar sesión completa el registro solo — corrige look004 (parte 2)
**Pasos:** Confirmar el correo (abrir el enlace del email) y luego, en
la app, iniciar sesión con ese email/contraseña.
**Esperado:** Entra DIRECTO al closet vacío, sin pedir repetir fotos,
formulario ni estilo. Verificar en Supabase que ahora sí existan
`consent_records`, `profiles` y `body_measurements` completos, y que la
fila de `onboarding_staging` para ese usuario ya no exista (se borró al
aplicarse).

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 

### CP-17 — Correo duplicado se detecta en vivo, antes de enviar el formulario — corrige look005
**Pasos:** En el formulario único, escribir un correo que ya tiene
cuenta y tocar en otro campo (perder el foco del campo email).
**Esperado:** Sin tocar "Registrarme" todavía, aparece "Ese correo ya
tiene una cuenta" debajo del campo, y el resto del formulario (nombre,
edad, contraseña, medidas, talla) queda deshabilitado — solo queda
disponible el botón "Ir a iniciar sesión".

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 

### CP-18 — CP-07 sigue funcionando con el nuevo corte (regresión)
**Pasos:** Repetir CP-07, pero cerrando la app ANTES de tocar el botón
final del tutorial ("Ir a mi closet") — a mitad del formulario, o
después de elegir estilo pero antes del tutorial.
**Esperado:** Igual que CP-07: al volver y hacer login con ese correo
(sin haberlo confirmado, o confirmándolo después), la app reinicia el
onboarding completo desde consentimiento — no hay nada guardado ni en
el dispositivo ni en el backend.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [x] No probado

**Código del informe de error:** 
