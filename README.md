# 🎙️ Clonador de Voz con IA (Qwen3-TTS)

**Powered by [script1clic.com](https://script1clic.com)**

Herramienta gratuita para Google Colab que clona una voz a partir de un audio corto de referencia y la usa para decir cualquier texto nuevo, usando el modelo Qwen3-TTS. Interfaz visual (Gradio), sin necesidad de saber programar.

---

## ✨ Características

- 🎤 **Sube o graba** el audio de referencia directamente desde el navegador (con micrófono).
- 📝 **Transcripción automática** del audio de referencia (vía `faster-whisper`), editable si se equivoca.
- 🌐 **10 idiomas**: español, inglés, francés, alemán, italiano, portugués, ruso, japonés, coreano y chino.
- 🎯 **Modo "Solo timbre"**: clona únicamente el timbre de voz sin depender de la transcripción (útil si Whisper no transcribe bien el audio de referencia).
- 🔒 **Resultados repetibles**: "Modo estable" o una semilla fija hacen que el mismo audio + texto den siempre el mismo resultado.
- 🎚️ **Opciones avanzadas**: temperatura y top-p para controlar la expresividad cuando no se usa el modo estable.
- ✂️ **Recorte automático de silencios** al inicio/final del audio de referencia, para una clonación más limpia.
- ⚡ **Funciona con GPU o CPU** (con GPU: 10-30 segundos por frase; sin GPU: varios minutos).
- 🔗 **Enlace público** para abrir la herramienta desde el celular u otro dispositivo (necesario para que el micrófono funcione bien).

---

## 🚀 Cómo usarlo

1. **Abre el notebook en Google Colab.**
2. *(Recomendado)* Activa la GPU: `Entorno de ejecución` → `Cambiar tipo de entorno` → `T4 GPU`.
3. **Ejecuta la Celda 1** (instalación de dependencias). Tarda 2-4 minutos. Espera el mensaje `✅ Todo listo`. Solo hace falta ejecutarla una vez por sesión.
4. **Ejecuta la Celda 2** (configuración): elige el idioma de la voz clonada y si quieres enlace público.
5. **Ejecuta la Celda 3** para abrir la interfaz visual. Verás un enlace `https://xxxxx.gradio.live`.
   - **Ábrelo en una pestaña nueva** (no uses el recuadro embebido de Colab) — así el navegador sí permite usar el micrófono.
   - Dentro de esa pestaña, presiona **"🔓 Habilitar micrófono"** antes de grabar.
6. Dentro de la interfaz:
   - Sube o graba un audio de referencia de **5-15 segundos, limpio** (sin ruido de fondo ni música).
   - Revisa el texto que Whisper detectó automáticamente; corrígelo si se equivocó.
   - Escribe el texto nuevo que quieres que diga la voz clonada.
   - *(Opcional)* Abre "⚙️ Consistencia de la voz" para ajustar semilla, modo estable, temperatura, top-p o activar "Solo timbre".
   - Presiona **"✨ Generar Voz Clonada"** y descarga el resultado.
7. Si algo falla, vuelve a ejecutar la Celda 1, luego la 2 y la 3.

---

## 🎤 Sobre el audio de referencia

| Recomendación | Motivo |
|---|---|
| 5-15 segundos de duración | Es el rango que mejor resultado da con Qwen3-TTS; menos de 3s es muy corto, más de 20s no aporta mejora |
| Audio limpio, sin ruido ni música de fondo | El modelo clona también el ruido junto con la voz si está presente |
| Una sola persona hablando | Varias voces mezcladas confunden la clonación |
| Habla clara y natural | Mejora tanto la transcripción automática como la calidad del timbre clonado |

La herramienta recorta automáticamente los silencios al inicio y al final del audio de referencia antes de usarlo.

---

## 🎯 Modo "Solo timbre" vs. modo normal

| | Modo normal | 🎯 Solo timbre |
|---|---|---|
| Usa la transcripción del audio de referencia | Sí | No |
| Fidelidad al timbre original | Buena | Más alta |
| Expresividad / naturalidad | Mayor | Menor |
| Cuándo usarlo | Uso general | Si Whisper no transcribe bien el audio, o si la voz generada suena distinta al original |

---

## 🔒 Consistencia: Modo estable vs. semilla vs. parámetros libres

- **Modo estable (recomendado, activado por defecto):** prioriza que el resultado sea fiel y predecible.
- **Semilla fija:** con el modo estable desactivado, la misma semilla + mismo audio + mismo texto siempre da el mismo resultado — útil para reproducir una generación que gustó.
- **Temperatura y top-p:** solo se aplican con el modo estable desactivado. Controlan cuánta variación/expresividad tiene la voz generada; valores más altos dan resultados más variados pero menos predecibles.

---

## ⚙️ Requisitos

- Cuenta de Google (para usar Google Colab).
- No requiere instalación local ni conocimientos de programación.
- Todas las dependencias (`qwen-tts`, `faster-whisper`, `gradio`, `soundfile`, `ffmpeg`) se instalan automáticamente en la Celda 1.
- Micrófono del navegador (opcional, solo si vas a grabar en vez de subir un archivo).

---

## 🛠️ Solución de problemas

| Problema | Solución |
|---|---|
| Error en la instalación (Celda 1) | Vuelve a ejecutarla. Si persiste, `Entorno de ejecución` → `Reiniciar sesión` y ejecuta la Celda 1 de nuevo |
| "Faltan dependencias" en la Celda 3 | Ejecuta la Celda 1, espera `✅ Todo listo`, luego la Celda 2 y la 3 |
| El micrófono no funciona / no se detecta | Asegúrate de haber abierto el enlace `gradio.live` en una **pestaña nueva del navegador**, no en el recuadro embebido de Colab. Luego presiona "🔓 Habilitar micrófono" |
| La voz generada suena distinta al audio original | Activa "🎯 Solo timbre" en "Opciones avanzadas" |
| Whisper transcribe mal el audio de referencia | Corrige el texto manualmente en el cuadro "Texto detectado", o activa "Solo timbre" (no depende de la transcripción) |
| Falla la generación de voz | Suele deberse a: audio de referencia muy corto, texto de referencia que no coincide con el audio, o texto a generar vacío. Verifica esos tres puntos y vuelve a intentar |
| Quiero repetir exactamente un resultado que me gustó | Anota la semilla usada (por defecto 42), desactiva "Modo estable" y usa la misma semilla + mismo audio + mismo texto |

---

## 📌 Notas

- La primera vez que se ejecuta la Celda 3, se descargan el modelo de voz (Qwen3-TTS) y el modelo de transcripción (Whisper); esto puede tardar unos minutos. Quedan en memoria durante el resto de la sesión.
- El enlace público (`gradio.live`) es necesario para que el micrófono funcione correctamente y es temporal: se desactiva al cerrar la sesión de Colab.
- Los archivos y modelos descargados se pierden al cerrar la sesión de Colab (es normal, no afecta tus resultados ya descargados).
- Usar esta herramienta para clonar la voz de otra persona sin su consentimiento puede tener implicancias legales y éticas; úsala de forma responsable.

---

*Creado por [script1clic.com](https://script1clic.com)*
