# davidpena-web

**En vivo:** https://davidpena-web.pages.dev

Página personal de David Peña. HTML + CSS puro, **sin build step**: lo que está en el repo es exactamente lo que se sirve.

Este repo es además el material de la clase **"Sube tu web a Cloudflare Pages"**.

---

## Archivos

| Archivo       | Para qué sirve |
|---------------|----------------|
| `index.html`  | La página. Único punto de entrada. |
| `styles.css`  | Todos los estilos. Sin frameworks, con modo oscuro automático. |
| `404.html`    | Página de error. Cloudflare Pages la usa sola si existe con ese nombre. |
| `_headers`    | Cabeceras HTTP que aplica Cloudflare al desplegar (seguridad y caché). No se sirve al visitante. |
| `img/`        | Foto (WebP + JPEG de respaldo) y favicon SVG. |
| `.gitignore`  | Lo que git debe ignorar. |

---

## La clase, en 6 pasos

### 1. Crear el repositorio en GitHub
```bash
gh repo create davidpena-web --public --source=. --remote=origin --push
```
(O desde github.com → New repository, y después `git remote add origin ...`)

### 2. Entrar a Cloudflare
https://dash.cloudflare.com → menú lateral **Compute (Workers & Pages)**.

### 3. Crear el proyecto de Pages
**Create application** → pestaña **Pages** → **Connect to Git**.

### 4. Autorizar GitHub
Cloudflare pide instalar su GitHub App. Se puede dar acceso a **todos** los repos o **solo a los seleccionados** (más seguro: elegir solo `davidpena-web`).

### 5. Configurar el build
Como es HTML plano, no hay nada que compilar:

| Campo | Valor |
|---|---|
| Production branch | `main` |
| Framework preset | `None` |
| Build command | *(vacío)* |
| Build output directory | `/` |

### 6. Save and Deploy
En ~30 segundos queda en `https://davidpena-web.pages.dev`.

---

## El punto de la clase: cada push despliega solo

```bash
# cambiás algo en index.html
git add .
git commit -m "Cambio el titular"
git push
```

Cloudflare detecta el push, despliega y actualiza el sitio. **No hay FTP, no hay servidor que mantener, no hay "subir archivos".**

Además:
- Cada rama distinta de `main` genera un **preview deploy** con su propia URL, para revisar antes de publicar.
- Cada deploy queda en el historial y se puede hacer **rollback** con un clic.

---

## Dominio propio (opcional)

En el proyecto → **Custom domains** → **Set up a domain**. Si el dominio ya está en Cloudflare, el DNS se configura solo. El certificado HTTPS también.

---

## Probar localmente

No hace falta ningún servidor: se puede abrir `index.html` con doble clic en el navegador.
Si querés que las rutas absolutas (`/styles.css` del 404) funcionen igual que en producción:

```bash
npx serve .
```
