# Consulta de Donaciones — sitio web

Página pública donde cada persona consulta sus donaciones y se ve el balance global en dólares.
Los datos vienen de una planilla de Google a través de Google Apps Script (API por JSONP).

## Estructura del repo

```
/
├─ index.html      ← la página (toda la lógica está acá)
├─ netlify.toml    ← configuración de despliegue
└─ README.md
```

> El backend (Code.gs) NO va en este repo: vive en Google Apps Script. Acá solo está la vista.

## Publicar con GitHub + Netlify (despliegue automático)

### 1. Subir a GitHub
- Creá un repositorio nuevo en GitHub (ej. `donaciones-web`).
- Subí estos archivos a la raíz del repo (`index.html`, `netlify.toml`, `README.md`).
  - Desde la web de GitHub: **Add file → Upload files**, arrastrás los archivos y **Commit**.
  - O por terminal:
    ```bash
    git init
    git add .
    git commit -m "Sitio de consulta de donaciones"
    git branch -M main
    git remote add origin https://github.com/TU_USUARIO/donaciones-web.git
    git push -u origin main
    ```

### 2. Conectar en Netlify
- En https://app.netlify.com → **Add new project → Import an existing project**.
- Elegí **GitHub** y autorizá el acceso.
- Seleccioná el repo `donaciones-web`.
- Configuración de build (dejar así):
  - **Build command:** (vacío)
  - **Publish directory:** `.`
- **Deploy**. Netlify te da la URL pública.

### 3. Listo
Cada vez que hagas un cambio y lo subas a GitHub (push / commit), Netlify vuelve a publicar solo. No hay que arrastrar nada nunca más.

## Notas

- La URL de la API ya está dentro de `index.html` (constante `API_URL`). Si reimplementás Apps Script con una URL distinta, actualizá esa línea y subí el cambio.
- Si cambiás el `Code.gs`, acordate de **Implementar → Administrar implementaciones → Versión: Nueva** en Apps Script. El sitio toma los datos en vivo, no hay que tocar GitHub por eso.
- Dominio propio: en Netlify → **Domain settings → Add a domain** (gratis).
