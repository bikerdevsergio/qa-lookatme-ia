# Smoke test — obligatorio antes de entregar un APK

Objetivo: detectar en 5 minutos si el APK está roto de forma obvia (como
v1.4, que se cerraba sola al abrir). Se corre SIEMPRE antes de copiar el
APK a `releases/` o al escritorio.

## Cómo correrlo

1. Build limpio: `flutter clean && flutter pub get`.
2. `flutter build apk --release > build_log.txt 2>&1; echo "EXIT:$?"` —
   revisar que diga `EXIT:0`. **Nunca usar `| tail` sin capturar el exit
   code aparte: enmascara builds fallidos.**
3. Instalar en el teléfono real (no solo emulador):
   `adb install -r build/app/outputs/flutter-apk/app-release.apk`
4. Si hay teléfono conectado por USB, dejar corriendo en paralelo para
   capturar logs en vivo:
   `adb logcat *:E flutter:V | grep -i -E "lookatme|flutter|AndroidRuntime"`

## Checklist

- [ ] La app **abre** y muestra la pantalla de bienvenida (no se cierra
      sola, no queda en pantalla negra/blanca más de 3 segundos).
- [ ] Si es la primera instalación: aparece la pantalla de consentimiento
      y el botón "Comenzar"/"Aceptar y continuar" responde.
- [ ] Login con un usuario de prueba existente funciona.
- [ ] El closet carga sin crashear (aunque esté vacío).
- [ ] El banner de AdMob aparece (o falla en silencio) — **nunca debe
      tumbar la app si no hay red o si el SDK falla al iniciar**.
- [ ] Rotar/minimizar y volver a abrir la app no la cierra.
- [ ] `adb logcat` no muestra ningún `FATAL EXCEPTION` ni
      `AndroidRuntime` crash en los primeros 10 segundos tras abrir.

Si cualquiera de estos puntos falla → NO se entrega el APK. Se corrige
primero.
