# qaessential

Sitio web de **Essential Coder**: https://qaessential.dev

Página estática hecha solo con HTML y Tailwind CSS. No tiene paso de build en
el despliegue: los ficheros del repositorio son el sitio.

| Fichero | Qué es |
| --- | --- |
| `index.html` | La página |
| `assets/styles.css` | Tailwind compilado (generado, no editar a mano) |
| `src/tailwind.css` | Fuente de Tailwind |
| `app-ads.txt` | Vendedores autorizados de AdMob para las apps (CityScout) |
| `robots.txt` | Permite rastrear todo el sitio |

## app-ads.txt

AdMob lo busca en la raíz del *sitio web del desarrollador* de la ficha de
Google Play, que es `https://qaessential.dev/`. Por eso tiene que responder en
`https://qaessential.dev/app-ads.txt` con HTTP 200 y `text/plain`, sin
redirigir a otro dominio.

## Cambiar estilos

Tras cambiar clases en `index.html`, regenera `assets/styles.css`:

```bash
npm install --no-save --no-package-lock tailwindcss@4.3.3 @tailwindcss/cli@4.3.3
npx tailwindcss -i src/tailwind.css -o assets/styles.css --minify
```

`node_modules` está en `.gitignore`.

## Despliegue en Vercel

1. Importar el repositorio. *Framework preset*: **Other**, sin *Build Command*
   y con la raíz como *Output Directory*.
2. *Settings → Domains*: añadir `qaessential.dev`. Si se añade también
   `www.qaessential.dev`, que sea `www` la que redirige a `qaessential.dev` y no
   al revés.
3. En Cloudflare (zona `qaessential.dev`), crear el registro que indique Vercel
   para el dominio raíz, en modo **DNS only**.

Comprobación:

```bash
curl -sSI https://qaessential.dev/app-ads.txt   # 200 y content-type text/plain
curl -sS  https://qaessential.dev/app-ads.txt   # la línea de AdMob
```
