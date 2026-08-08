# sinfiltro-assets

Repo de **infraestructura pública** de Sin Filtro. No tiene código de la marca: solo sirve archivos.

Hace tres trabajos que en realidad son el mismo problema:

1. **CDN de imágenes.** TikTok no acepta subir binarios en photo posts: solo `PULL_FROM_URL`, o sea que las imágenes tienen que estar en una URL pública HTTPS. Acá viven, en `img/<carrusel-id>/`.
2. **Dominio verificable.** La app de TikTok exige que el dominio desde el que se sirven las imágenes esté verificado en el Developer Portal.
3. **Páginas que la app de TikTok pide para aprobarse:** términos, privacidad y el callback de OAuth.

Se publica con GitHub Pages (rama `main`, raíz).

## Cómo se suben las imágenes

Desde el repo del render:

```bash
node render.js data/mi_carrusel.json --jpg     # TikTok no acepta PNG
node publicar_assets.js data/mi_carrusel.json  # copia acá y te da las URLs
```

Después commitear y pushear este repo: recién ahí las URLs quedan vivas.

## Estructura

```
index.html        landing mínima (Pages necesita algo en la raíz)
terminos.html     términos de uso
privacidad.html   política de privacidad
callback.html     landing del callback de OAuth de TikTok
img/<id>/*.jpg    las piezas publicadas
```

## Ojo con el tamaño

Estimado ~5MB por día de imágenes. GitHub recomienda mantener los repos por debajo de 1GB. A ese ritmo son ~6 meses. Cuando se acerque, hay dos salidas: podar `img/` de piezas viejas (ya publicadas, no se vuelven a servir) o mudarse a un object storage con dominio propio — pero eso obliga a re-verificar el dominio en TikTok.
