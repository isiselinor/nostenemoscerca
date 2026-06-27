# Publicar la consulta de donaciones en Netlify

La página vive en Netlify, pero los datos los sigue entregando tu Google Sheet a través de Apps Script. El `Code.gs` **no se sube a Netlify**: se queda en Apps Script funcionando como API.

## Paso 1 — Actualizar y publicar Apps Script como API

1. En el editor de Apps Script, reemplazá el contenido de **`Código.gs`** con el nuevo `Code.gs` (la función `doGet` ahora también responde datos).
2. Guardá (💾).
3. **Implementar → Administrar implementaciones → ✏️ editar → Versión: Nueva → Implementar**.
4. Confirmá que en "Quién tiene acceso" diga **Cualquier persona**.
5. Copiá la **URL de la aplicación web** (termina en `/exec`).

> Probá que la API funciona: pegá en el navegador `TU_URL/exec?action=totals`. Debería devolver un texto JSON con los totales.

## Paso 2 — Pegar tu URL en la página

1. Abrí `index.html` (con cualquier editor de texto, o avisame y lo dejo listo).
2. Buscá la línea:
   ```js
   var API_URL = "https://script.google.com/macros/s/PEGA_TU_ID_DE_IMPLEMENTACION/exec";
   ```
3. Reemplazá esa URL por la tuya de `/exec`. Guardá.

## Paso 3 — Subir a Netlify

Opción rápida (sin Git):

1. Entrá a https://app.netlify.com → **Add new project / site → Deploy manually**.
2. **Arrastrá la carpeta `netlify`** (la que contiene `index.html`) a la zona de "drag and drop".
3. Netlify te da una URL pública (ej. `https://tu-sitio.netlify.app`). ¡Listo!

> Para actualizar el diseño después: editás `index.html` y volvés a arrastrar la carpeta (o conectás un repo de GitHub para que se actualice solo).

## Notas

- Si cambiás algo en `Code.gs`, recordá hacer **Nueva versión** en "Administrar implementaciones", o Netlify seguirá viendo la versión vieja.
- La página usa **JSONP** para pedir los datos, así evita el bloqueo de CORS entre el dominio de Netlify y el de Google.
- Solo necesitás subir `index.html`. El archivo `LEEME-NETLIFY.md` es solo esta guía, no hace falta subirlo.
- Tu dominio propio (si tenés uno) se puede conectar gratis desde Netlify: **Domain settings → Add a domain**.
