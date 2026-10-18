# Local image converter

> Convierte imágenes AVIF y WebP a JPG, PNG, GIF o WebP directamente en tu navegador. Sin servidor y sin subir nada.

![Versión](https://img.shields.io/badge/versi%C3%B3n-1.2.1-blue)
![Manifest V3](https://img.shields.io/badge/Chrome-Manifest%20V3-green)
![Idiomas](https://img.shields.io/badge/idiomas-ES%20%7C%20EN%20%7C%20PT%20%7C%20FR%20%7C%20JA-orange)

[English](README.md) · **Español**

<!-- Añade aquí una captura, por ejemplo ![Captura](docs/captura.png) -->

**Local image converter** es una extensión de Chrome que encuentra las imágenes de cualquier página web y las convierte por lotes, todo en tu propio equipo. Elige el formato de salida, una subcarpeta dentro de Descargas y recibe todo en un único ZIP o archivo por archivo.

## Características

- **Detecta las imágenes de la página**: `<img>`, `srcset`, fuentes de `<picture>`, imágenes con carga diferida, enlaces a archivos de imagen y fondos CSS.
- **Varias formas de usarla**: clic en el icono de la extensión, clic derecho sobre una imagen (*Convertir imagen…*), clic derecho en la página (*Detectar imágenes de esta página*) o arrastrar archivos al convertidor.
- **Conversión por lotes** a **JPG, PNG, GIF o WebP**, con deslizador de calidad para JPG y WebP.
- **Imágenes animadas**: las animaciones WebP, AVIF y GIF se pueden convertir a GIF animado, conservando los tiempos de cada fotograma y la transparencia simple.
- **Sin pérdida innecesaria**: si el origen ya tiene el formato elegido, se guarda el archivo original sin tocarlo.
- **Filtros y selección**: filtra por tipo (AVIF, WebP, JPG, PNG, GIF) y por tamaño mínimo; botones *Seleccionar visibles*, *Quitar selección* y *Limpiar selección*.
- **Opciones de descarga**: subcarpeta dentro de Descargas, un ZIP o archivos sueltos, "Preguntar dónde guardar" opcional y una notificación al completar la descarga.
- **Recuerda tu configuración** entre sesiones.
- **Multilingüe**: sigue el idioma de tu navegador (español, inglés, portugués, francés y japonés; inglés como respaldo).
- **Privada por diseño**: todo se procesa localmente en tu navegador.

## Instalación

La extensión todavía no está en Chrome Web Store, así que se instala desde el código:

1. Descarga el último ZIP desde la página de [Releases](../../releases) (o usa **Code → Download ZIP**) y descomprímelo.
2. Abre `chrome://extensions` en Chrome.
3. Activa el **Modo de desarrollador** (arriba a la derecha).
4. Pulsa **Cargar descomprimida** y selecciona la carpeta que contiene `manifest.json`.
5. Fija la extensión desde el menú de la pieza de puzle para tener siempre visible su icono.

Requiere una versión reciente de Chrome (102 o superior). Otros navegadores basados en Chromium pueden funcionar, pero no se han probado.

**Actualizar:** reemplaza la carpeta con la nueva versión y pulsa el botón de recargar en la tarjeta de la extensión en `chrome://extensions`.

## Cómo se usa

1. Abre una página con imágenes y pulsa el icono de la extensión. Se abre una pestaña nueva con todas las imágenes detectadas en esa página.
2. Selecciona las imágenes que quieras (clic en cada tarjeta o **Seleccionar visibles**). Usa los filtros por tipo y el tamaño mínimo para acotar la lista.
3. Elige el **formato de salida** y, si quieres, una **subcarpeta** dentro de Descargas.
4. Pulsa **Convertir y descargar**. Recibirás una notificación cuando los archivos estén guardados.

También puedes arrastrar archivos de imagen desde tu equipo a la página del convertidor.

## Formatos de salida

| Salida | Calidad | Notas |
| --- | --- | --- |
| **PNG** | Sin pérdida | Las imágenes animadas conservan solo el primer fotograma. |
| **JPG** | Deslizador (50–100 %) | Las zonas transparentes se rellenan con el color que elijas. Las animadas conservan solo el primer fotograma. |
| **GIF** | 256 colores por fotograma | Conserva la animación, los tiempos y la transparencia simple (sí/no). |
| **WebP** | Deslizador (50–100 %) | Con pérdida incluso al 100 %. Las animadas conservan solo el primer fotograma. |

## Permisos

| Permiso | Para qué se necesita |
| --- | --- |
| `activeTab`, `scripting` | Leer la lista de imágenes de la página en la que estás al pulsar el icono. |
| `<all_urls>` (acceso a sitios) | Descargar las imágenes desde el sitio de origen para convertirlas localmente. |
| `downloads` | Guardar los archivos convertidos, en una subcarpeta de Descargas si la indicas. |
| `storage` | Recordar tu configuración y pasar las imágenes detectadas a la pestaña del convertidor. |
| `contextMenus` | Las opciones del clic derecho. |
| `notifications` | Avisarte cuando la descarga se complete. |

## Privacidad

No se sube nada a ningún sitio. Tu navegador descarga las imágenes, las convierte localmente y las guarda en tu disco. La extensión no tiene servidor, ni analíticas, ni rastreo.

## Limitaciones conocidas

- Chrome solo permite guardar **dentro de la carpeta Descargas**. Una ruta absoluta como `D:\Imagenes` se reduce al nombre de su última carpeta.
- Algunos sitios bloquean que sus imágenes se descarguen desde fuera de sus páginas (protección contra hotlinking), así que alguna imagen puede no cargar.
- Las páginas internas de Chrome (`chrome://…`, Web Store) no se pueden escanear; allí usa arrastrar y soltar.
- El GIF está limitado por el propio formato a 256 colores por fotograma.

## Estructura del proyecto

```
manifest.json        Manifiesto de la extensión (Manifest V3)
background.js        Detección de imágenes y menús contextuales
converter.html/.css  Página del convertidor
converter.js         Decodificación, codificación, descargas, i18n
_locales/            Traducciones (es, en, pt_BR, pt_PT, fr, ja)
lib/                 gifenc y fflate (incluidas, no necesitan red)
icons/ images/       Iconos e imagen de fondo
```

## Añadir un idioma

Copia `_locales/en` a una carpeta nueva con el código del idioma (por ejemplo `de`), traduce los valores `message` de `messages.json` y recarga la extensión.

## Créditos

Creado por **[Angel4RS](https://github.com/Angel4RS)**.

Si te resulta útil, puedes apoyar el proyecto en **[Ko-fi](https://ko-fi.com/angel4kv1)**.

Hecho con [gifenc](https://github.com/mattdesl/gifenc) (codificación GIF) y [fflate](https://github.com/101arrowz/fflate) (creación de ZIP).
