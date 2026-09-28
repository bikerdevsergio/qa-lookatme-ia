# Casos de prueba — Prueba virtual (Módulo 4)

## CP-01 — Superposición básica
**Pasos:** Fotografiar una prenda externa (o subir de galería), iniciar
prueba virtual.
**Esperado:** Se genera una imagen del usuario con la prenda superpuesta
sobre su foto corporal guardada.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-02 — El usuario sigue siendo él mismo (CRÍTICO)
**Pasos:** Repetir CP-01 con al menos 3 personas/fotos corporales
distintas.
**Esperado:** En los 3 casos, la persona en el resultado sigue siendo
reconociblemente la misma persona — mismo rostro, mismo tono de piel,
mismo cuerpo. Solo puede cambiar la pose si hace falta para que la prenda
se vea natural. **Este fue un bug real reportado en producción** ("me
cambió la cara, no parezco yo") — cualquier regresión acá es bloqueante,
no se publica la versión.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-03 — Comparador de tallas
**Pasos:** Ingresar medidas/talla de la prenda externa, correr la prueba
virtual con un usuario que ya tiene `body_measurements` guardadas.
**Esperado:** El consejo de talla es coherente (ej. "te quedaría ancho en
hombros pero bien en cintura — pide talla M"), basado en las medidas
reales del usuario vs las de la prenda.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-04 — Sin foto corporal guardada
**Pasos:** Usuario que omitió la foto corporal en onboarding intenta usar
prueba virtual.
**Esperado:** Se le indica que necesita cargar una foto corporal primero
(con acceso directo a hacerlo), no un error críptico.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-05 — La foto de la prenda externa no se guarda
**Pasos:** Hacer una prueba virtual, luego revisar en Supabase Storage.
**Esperado:** No debe existir un archivo persistente de la foto de la
prenda externa que se subió — es efímera, se procesa y se descarta (ver
Política de Privacidad, sección "Contenido efímero de la prueba virtual").

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-06 — Límite de cuota (ver también `premium-y-cuotas.md`)
**Pasos:** Ver CP-02 de `premium-y-cuotas.md`.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:**
