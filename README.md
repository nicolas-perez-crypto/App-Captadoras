# Cima Propiedades — Panel Captadora (versión instalable)

Esta es tu app real (`App_Captadoras (3).html`) ya conectada a tu proyecto Supabase,
ahora empaquetada para poder:

- **Instalarse en el celular** como app (ícono en pantalla de inicio, pantalla completa).
- **Actualizarse sola**: cada vez que subas un cambio y tengas internet, al abrir la
  app se carga automáticamente la versión más nueva (no hace falta reinstalar).
- **Funcionar sin internet** para lo último que se cargó (modo offline básico).

No toqué la lógica de tu app ni tu conexión a Supabase — solo agregué los archivos
necesarios para que sea instalable:
- `manifest.json` (le dice al celular cómo se llama la app, su ícono, colores)
- `sw.js` (el "service worker" que la hace instalable y con caché offline)
- `icons/` (íconos de la app)
- unas líneas agregadas al `<head>` y antes de `</body>` de tu `index.html`

---

## Publicar la app (una sola vez)

La forma más simple de mantenerla actualizable es **GitHub + Vercel**.

### 1. Sube esta carpeta a GitHub
```bash
cd cima-pwa
git init
git add .
git commit -m "Panel Captadora instalable"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/cima-captadora.git
git push -u origin main
```

### 2. Despliega en Vercel (gratis)
1. Entra a https://vercel.com y conecta tu cuenta de GitHub.
2. **Add New → Project** → elige el repositorio `cima-captadora`.
3. Es un sitio estático (no necesita build ni variables de entorno, porque tu
   Supabase URL y anon key ya están dentro del `index.html`). Dale **Deploy**.
4. En ~1 minuto obtienes una URL como `https://cima-captadora.vercel.app`.

---

## Instalar en el celular

**Android (Chrome):**
1. Abre la URL de Vercel.
2. Menú (⋮) → **"Instalar app"** o **"Añadir a pantalla de inicio"**.

**iPhone (Safari):**
1. Abre la URL de Vercel en **Safari**.
2. Botón **Compartir** → **"Añadir a pantalla de inicio"**.

Queda como un ícono más, se abre a pantalla completa, sin barra del navegador.

---

## Cómo actualizarla en el futuro

Cada vez que quieras cambiar algo en la app:

1. Edita `index.html` (o pídeme el cambio).
2. Sube el cambio:
   ```bash
   git add .
   git commit -m "Descripción del cambio"
   git push
   ```
3. Vercel vuelve a publicar automáticamente (~1 minuto).
4. La próxima vez que alguien abra la app instalada **con internet**, va a
   cargar la versión nueva sola — no hay que desinstalar ni reinstalar nada.

---

## Nota sobre tu llave de Supabase

Tu `index.html` ya trae adentro la URL y la **anon key** (llave pública) de tu
proyecto Supabase. Eso es normal y así está diseñado Supabase: esa llave es
pública a propósito, lo que realmente protege tus datos son las políticas de
seguridad (RLS) configuradas en las tablas de tu proyecto. Si nunca las
revisaste, dime y las repasamos juntos para asegurarnos de que cada captadora
solo vea sus propios clientes.
