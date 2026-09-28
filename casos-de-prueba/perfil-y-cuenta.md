# Casos de prueba — Perfil y cuenta

## CP-01 — Cambiar foto corporal ("cambio de look")
**Pasos:** Perfil → cambiar foto corporal → tomar/elegir nueva foto →
guardar.
**Esperado:** La foto anterior se reemplaza (verificar en Storage que la
vieja no quede huérfana), se refleja en la próxima prueba virtual/outfit
generado.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-02 — Actualizar medidas
**Pasos:** Perfil → actualizar medidas → cambiar algún valor → guardar.
**Esperado:** Se guarda correctamente, se usa en la siguiente comparación
de tallas.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-03 — Cambiar estilo preferido
**Pasos:** Perfil → cambiar estilo → seleccionar uno distinto.
**Esperado:** Se guarda, afecta futuras generaciones de outfits.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-04 — Eliminar cuenta (CRÍTICO, requisito de Google Play)
**Pasos:** Perfil → "Eliminar mi cuenta" → confirmar. Usar un usuario de
prueba, no uno real.
**Esperado:**
- Se cierra sesión automáticamente tras confirmar.
- En Supabase: el usuario desaparece de Auth.
- En Storage: no quedan archivos en `closet-photos`, `body-photos`,
  `outfit-renders` ni `tryon-renders` para ese usuario (los 4 buckets —
  el cascade de Postgres borra las filas de las tablas pero NUNCA los
  archivos de storage, hay que verificar los 4 explícitamente).
- No se puede volver a iniciar sesión con esas credenciales.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-05 — Pantalla "Privacidad y mis datos"
**Pasos:** Perfil → "Privacidad y mis datos".
**Esperado:** Ver CP-03 y CP-05 de `legal-y-consentimiento.md`.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:**
