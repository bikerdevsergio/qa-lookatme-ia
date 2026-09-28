# Casos de prueba — AdMob / anuncios

## CP-01 — Inicialización no bloqueante
**Pasos:** Abrir la app con el teléfono en modo avión (sin red).
**Esperado:** La app abre normalmente, muestra la pantalla de bienvenida o
Home. El banner de anuncios puede no cargar (espacio vacío o placeholder),
pero la app **no se cierra ni queda en pantalla de carga infinita**.

**Resultado:** [x ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-02 — Banner visible para usuario free
**Pasos:** Login con un usuario sin `premium_until` activo, ir al closet.
**Esperado:** Banner no intrusivo visible, no tapa contenido crítico
(botones, prendas), no es un popup de pantalla completa.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-03 — Banner oculto para usuario premium
**Pasos:** Login con un usuario con `premium_until` en el futuro (ej. uno
de los primeros 50 registros), ir al closet.
**Esperado:** No aparece banner de anuncios.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:** 

## CP-04 — App usable si AdMob falla al iniciar
**Pasos:** Revisar `adb logcat` al abrir la app; forzar el fallo si es
posible (ej. bloquear el dominio de AdMob a nivel de red).
**Esperado:** El log puede mostrar `MobileAds.initialize() failed: ...`
(mensaje agregado en `main.dart` a partir de v1.5), pero no debe aparecer
ningún `FATAL EXCEPTION` ni cierre de la app.

**Resultado:** [ ] Pasa &nbsp;&nbsp; [ ] Falla &nbsp;&nbsp; [ ] No probado

**Código del informe de error:**
