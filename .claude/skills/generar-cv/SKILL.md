---
name: generar-cv
description: Genera un CV a medida y ATS-friendly para una oferta concreta, a partir del SOT en profile/. Produce Markdown, HTML maquetado y PDF, más la lista de skills a declarar en el formulario de la oferta. Úsala cuando el usuario pida un CV, adaptar el CV a una oferta, o tras aprobar el análisis de /analizar-oferta.
---

# Generar CV a medida

## 0. Prerrequisitos
Necesitas la oferta analizada. Si no hay análisis previo en esta conversación,
busca la fila en `profile/09-historial-candidaturas.md` y el texto en `ofertas/`;
si tampoco existe, ejecuta primero el flujo de `analizar-oferta` (al menos los
pasos 1-3).
Lee **todo** `profile/`.

## 1. Regla inviolable
Cada línea del CV debe poder trazarse a una línea del SOT. Si no puedes señalar
la fuente, no va. Puedes:
- reordenar y priorizar por relevancia
- reformular usando la terminología exacta de la oferta (si describe lo mismo)
- agregar bullets relacionados en uno
- traducir al idioma de la oferta

No puedes: añadir tecnologías, inflar años, inventar métricas, ni convertir
"he tocado" en "domino".

Aplica la **jerarquía de fortalezas** de `03-skills.md`: el titular y el perfil
se anclan en el nivel *núcleo*; *sólido* se presenta como capacidad efectiva;
*acotado* solo si la oferta lo pide y acotado; *no cubierto* nunca. El orden de
las competencias técnicas comunica esa jerarquía.

## 2. Idioma
El del texto de la oferta. Oferta en inglés -> CV en inglés. Oferta en español
para empresa española -> español. Si la empresa es internacional con oferta en
español, pregunta.

## 3. Selección de contenido
1. Saca las 8-12 **palabras clave** de la oferta (tecnologías, metodologías,
   responsabilidades). Esas son el objetivo de cobertura del CV.
2. Elige de `01-experiencia.md` los bullets que las cubran. Máx 4-6 por puesto
   reciente, 2-3 por puestos antiguos.
3. Incluye `04-proyectos.md` solo si cubre una palabra clave que la experiencia
   no cubre, o si el perfil es junior.
4. `06-extraprofesional.md` entra solo si la oferta pide explícitamente esa soft
   skill y tienes evidencia concreta.
5. Reescribe cada bullet con la fórmula: **verbo de acción + qué + con qué stack
   + resultado medible**. Sin métrica en el SOT, sin métrica en el bullet.

## 4. Estructura del CV (orden ATS canónico)
1. **Nombre** y titular ajustado al puesto de la oferta
2. **Contacto**: email, teléfono, ciudad, LinkedIn, GitHub — en texto plano, una línea
3. **Perfil** — 3-4 líneas, escritas *para esta oferta*: años + especialidad +
   2-3 tecnologías clave de la oferta + qué busco. Sin adjetivos vacíos.
4. **Competencias técnicas** — agrupadas (Lenguajes / Frameworks / Datos / Cloud
   y DevOps / Testing). Solo lo que esté en la oferta o sea relevante; no un
   listado exhaustivo.
5. **Experiencia profesional** — Puesto · Empresa · Ciudad · MM/AAAA–MM/AAAA
6. **Proyectos** (opcional)
7. **Formación**
8. **Certificaciones** (si las hay)
9. **Idiomas**

Longitud: **1 página** hasta ~5 años de experiencia; 2 como máximo absoluto.

## 5. Reglas ATS (duras)
- Sin tablas, sin columnas, sin cuadros de texto, sin cabecera/pie, sin imágenes,
  sin iconos, sin gráficos de barras de "nivel de skill".
- Fechas siempre `MM/AAAA – MM/AAAA`, coherentes en todo el documento.
- Nombres de sección canónicos (Experiencia / Formación / Competencias técnicas).
- Sin foto: en España es común ponerla, pero perjudica en ATS y en procesos
  internacionales. Por defecto, sin foto; si el usuario la quiere, avísale del trade-off.
- Nada de datos protegidos innecesarios: sin edad, sin DNI, sin estado civil,
  sin dirección completa (solo ciudad). Es la práctica correcta bajo GDPR y evita sesgo.
- Un solo tipo de viñeta, fuente estándar (Arial/Helvetica/Calibri), 10-11pt.

## 6. Salida
Usa la carpeta `salidas/<empresa>-<puesto>-<YYYY-MM-DD>/` de la oferta (mismo
slug que el fichero en `ofertas/`; créala solo si no existe) con:
- `cv.md` — fuente editable
- `cv.html` — aplicando `templates/cv-ats.html` (sustituye el bloque
  `<!--CONTENT-->` y pon `<title>Nombre Apellido — CV</title>`)
- `<Nombre>_<Apellido>_CV.pdf` — nombre profesional, sin tildes (es el fichero
  que se sube al portal). Ver "Generar el PDF"
- `skills-formulario.md` — ver sección 7
- `trazabilidad.md` — tabla `línea del CV -> fuente en profile/`, para poder
  defender cada afirmación en la entrevista

## 7. Lista de skills para el formulario
Muchos portales (LinkedIn, InfoJobs, Workday, Greenhouse) piden marcar skills.
Genera tres bloques:
- **Declarar sí** — cubiertas por el SOT y pedidas en la oferta, ordenadas por
  peso en la oferta.
- **Declarar con matiz** — nivel *sólido* o *acotado* en la jerarquía del SOT:
  decláralas, pero prepárate a acotarlas en entrevista. Incluye la frase exacta
  con la que acotarlas.
- **No declarar** — pedidas pero sin evidencia (nivel *no cubierto*). Explica por qué no mentir aquí:
  es lo primero que se comprueba en la técnica.

Añade también las **keywords literales de la oferta** que deben aparecer en el
CV, y confirma cuáles has conseguido colocar.

## 8. Generar el PDF
Usa un navegador Chromium headless (Edge o Chrome). Localiza el que exista:

| SO | Rutas habituales |
|---|---|
| Windows (Bash) | `/c/Program Files (x86)/Microsoft/Edge/Application/msedge.exe`, `/c/Program Files/Google/Chrome/Application/chrome.exe` |
| macOS | `/Applications/Google Chrome.app/Contents/MacOS/Google Chrome`, `/Applications/Microsoft Edge.app/Contents/MacOS/Microsoft Edge` |
| Linux | `google-chrome`, `chromium`, `chromium-browser`, `microsoft-edge` |

```
"<navegador>" --headless --disable-gpu --no-pdf-header-footer \
  --print-to-pdf="<ruta absoluta>/Nombre_Apellido_CV.pdf" \
  "file:///<ruta absoluta>/cv.html"
```

En Windows, las rutas que se pasan al navegador deben ser **absolutas y en
formato Windows** (`--print-to-pdf="C:\ruta\Nombre_Apellido_CV.pdf"`) y el HTML
como URL `file:///C:/...`. Verifica después que el PDF existe y pesa >0. Si falla, deja el HTML y dile al usuario que lo abra e
imprima a PDF (Ctrl+P -> Guardar como PDF, márgenes por defecto, sin cabeceras).

## 9. Cierre
Resume: qué keywords cubre el CV, cuáles no ha podido cubrir y por qué, y
cuántas páginas ha salido. Pregunta si quiere cover letter.
