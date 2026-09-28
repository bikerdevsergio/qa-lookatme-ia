# Casos de prueba — Legal y consentimiento

## CP-01 — Consentimiento obligatorio en onboarding
**Pasos:** Registro nuevo, llegar a la pantalla de consentimiento, intentar
tocar "Aceptar y continuar" sin marcar ningún checkbox.
**Esperado:** El botón está deshabilitado. No se puede avanzar.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-02 — Consentimiento de datos sensibles es independiente
**Pasos:** En la pantalla de consentimiento, marcar solo el checkbox de la
Política de Tratamiento de Datos (general), dejar sin marcar el de
foto corporal/medidas.
**Esperado:** Se puede continuar (el checkbox de foto corporal es
opcional para avanzar), pero más adelante en el flujo de foto corporal se
indica que esa función/prueba virtual no estará disponible sin ese
consentimiento.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-03 — Documentos legales se leen completos
**Pasos:** Desde consentimiento y desde Perfil → "Privacidad y mis datos",
abrir los 3 documentos (Política de Privacidad, T&C, Consentimiento
informado).
**Esperado:** Cada uno abre, se puede hacer scroll completo, el texto
coincide con `legal/*.md` (Bogotá como domicilio, sin el pie "redactado
con asistencia de IA" — remover ese pie fue instrucción explícita de
Sergi, ver commit correspondiente).

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-04 — `consent_records` guarda versión y fecha
**Pasos:** Completar el consentimiento con un usuario de prueba, revisar
la tabla `consent_records` en Supabase.
**Esperado:** Existe una fila con `policy_version` y `accepted_at`
poblados para ese usuario.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-05 — Canal de PQR visible
**Pasos:** Ir a Perfil → "Privacidad y mis datos".
**Esperado:** Se muestra `legal@raccoondev.dev` como canal de contacto
para peticiones, quejas y reclamos.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-06 — Documentos también publicados en la web
**Pasos:** Abrir `https://raccoondev.dev/legal/lookatme-ia/` desde un
navegador (fuera de la app).
**Esperado:** Los 3 documentos están accesibles y coinciden con la versión
dentro de la app (misma fecha, sin el pie de IA).

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:**
