# Off Axis Studio — Links Page
## Guía de Implementación y Mantenimiento

---

### 📁 Estructura del proyecto

```
off-axis-deploy/
├── index.html      ← La página principal (todo el sitio en un archivo)
├── netlify.toml    ← Configuración de Netlify (headers, cache, seguridad)
├── robots.txt      ← Para SEO / crawlers
└── sitemap.xml     ← Para Google Search Console
```

---

### 🚀 Deploy en Netlify (paso a paso)

#### Opción A: Deploy desde GitHub (recomendada)

1. **Crea un repo en GitHub**
   ```bash
   cd off-axis-deploy
   git init
   git add .
   git commit -m "Off Axis Links - v1"
   git remote add origin https://github.com/TU-USUARIO/offaxis-links.git
   git push -u origin main
   ```

2. **Conecta con Netlify**
   - Ve a [app.netlify.com](https://app.netlify.com) y crea una cuenta (gratis)
   - Click en **"Add new site"** → **"Import an existing project"**
   - Selecciona GitHub y autoriza acceso
   - Elige el repo `offaxis-links`
   - Build command: **(déjalo vacío)**
   - Publish directory: **`.`**
   - Click **"Deploy site"**

3. **Configura el dominio personalizado**
   - En Netlify: **Site settings → Domain management → Add custom domain**
   - Escribe: `links.offaxisstudio.com`
   - En el panel DNS de Alonso (donde tiene el dominio), agrega un registro:
     - **Tipo:** CNAME
     - **Nombre:** links
     - **Valor:** el-nombre-random.netlify.app (Netlify te da esto)
   - Netlify configura HTTPS automáticamente (tarda ~5 min)

4. **Flujo de actualizaciones**
   ```bash
   # Editas index.html localmente
   git add .
   git commit -m "Actualizado precio de guía X"
   git push
   # Netlify detecta el push y re-deploya automáticamente (~30 seg)
   ```

#### Opción B: Deploy manual (drag & drop)

1. Ve a [app.netlify.com/drop](https://app.netlify.com/drop)
2. Arrastra toda la carpeta `off-axis-deploy` al navegador
3. Listo, ya está online
4. Para actualizar: drag & drop de nuevo con los cambios

---

### 🔗 Configurar como Link-in-Bio

Una vez que la página esté en `links.offaxisstudio.com`:

| Plataforma | Dónde ponerlo |
|------------|---------------|
| **Instagram** | Perfil → Editar → Sitio web → `links.offaxisstudio.com` |
| **TikTok** | Perfil → Editar → Sitio web → `links.offaxisstudio.com` |
| **YouTube** | Canal → Personalizar → Info básica → Links |
| **Facebook** | Página → Acerca de → Sitio web |
| **Twitter/X** | Perfil → Editar → Sitio web |

---

### ✏️ Guía de mantenimiento para Mao

Cuando Alonso te pida cambios, estas son las ediciones más comunes:

#### Cambiar un precio
Busca el texto del precio actual (ej: `$9.90`) dentro del card de la guía correspondiente y cámbialo. Cada guía tiene su precio en `.guide-price-tag` y los packs en `.pack-price`.

#### Agregar una guía nueva
Copia uno de los bloques `<a class="guide-link">...</a>` existentes y cambia:
- La URL del `href` al link de Hotmart nuevo
- La imagen en `<img src="...">`
- El título en `.guide-title`
- El hook en `.guide-hook`
- El precio en `.guide-price-tag`
- Agrega `<span class="guide-new-badge">Nueva</span>` si quieres el badge verde

#### Cambiar una imagen de producto
Sube la imagen nueva a Cloudinary de Alonso y reemplaza la URL en el `src` de la imagen correspondiente. Mantén los parámetros de Cloudinary: `w_350,q_auto,f_auto` para guías individuales, `w_500,q_auto,f_auto` para packs.

#### Cambiar el texto del Muppet
El speech bubble está en `.muppet-inter-bubble` y la quote final en `.muppet-quote`. Edita el texto directamente.

#### Agregar un pack nuevo
Copia un bloque `<a class="pack">...</a>` y ajusta contenido. Si son 3 packs, el grid se ajusta automático.

---

### 📊 OG Tags — Lo que se ve al compartir

Cuando alguien comparta el link en redes sociales o WhatsApp, va a ver:

- **Título:** "Off Axis Studio — Guías de Producción Musical"
- **Descripción:** "Aprende mezcla, mastering, efectos y más con guías directas..."
- **Imagen:** El logo de Off Axis Studio

> ⚠️ **IMPORTANTE:** Después de deployar, actualiza las URLs en las meta tags `og:url` y `<link rel="canonical">` con la URL final real de producción. También actualiza `robots.txt` y `sitemap.xml`.

Para verificar cómo se ve el preview:
- Facebook: [developers.facebook.com/tools/debug](https://developers.facebook.com/tools/debug/)
- Twitter: [cards-dev.twitter.com/validator](https://cards-dev.twitter.com/validator)
- General: [opengraph.xyz](https://opengraph.xyz)

---

### 💡 Nota sobre la OG Image

La imagen OG actual usa el logo de Off Axis directamente desde Cloudinary con transformaciones (`w_1200,h_630,c_fill`). Si Alonso quiere una imagen más elaborada para compartir (con fondo oscuro, el muppet, texto promocional, etc.), se puede crear una imagen custom de 1200x630px, subirla a Cloudinary y actualizar las meta tags `og:image` y `twitter:image`.

---

### 🔒 Seguridad incluida

El `netlify.toml` ya configura:
- **X-Frame-Options:** Evita que embeddeen la página en iframes
- **X-Content-Type-Options:** Previene MIME sniffing
- **Referrer-Policy:** Protege la privacidad de navegación
- **Cache headers:** Balance entre frescura y velocidad

---

### 📱 Tip: Probar la OG image antes de compartir

Después del deploy, usa WhatsApp Web para mandarte el link a ti mismo — ahí verás exactamente cómo se ve el preview que van a ver los seguidores de Alonso cuando compartan la página.
