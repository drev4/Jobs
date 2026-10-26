---
name: perfil-linkedin
description: Genera el contenido completo del perfil de LinkedIn (titular, extracto, experiencia, skills, aptitudes destacadas, ajustes de Open to Work y SEO) a partir del SOT de profile/. Optimizado para que los reclutadores encuentren el perfil en LinkedIn Recruiter. Úsala cuando el usuario quiera crear o actualizar su LinkedIn, mejorar su visibilidad, o tras un cambio relevante en el SOT.
---

# Perfil de LinkedIn

## 0. Diferencia clave con el CV
**No es un CV pegado en una web.** Cambian el objetivo, el tono y las reglas:

| | CV | LinkedIn |
|---|---|---|
| Objetivo | Pasar un ATS para **una** oferta | Que **te encuentren** para muchas |
| Dirección | Yo escribo a la empresa | El reclutador me busca a mí |
| Tono | Impersonal, telegráfico | Primera persona, algo más humano |
| Optimización | Keywords de esa oferta | Keywords que los reclutadores **buscan** |
| Longitud | 1-2 páginas | El extracto se corta a ~3 líneas en móvil |

Consecuencia: **el perfil se escribe para el conjunto de ofertas que el usuario
quiere**, no para una concreta. Léete `07-preferencias.md` antes que nada: el
perfil debe atraer lo que quiere y repeler lo que no.

## 1. Cargar
Lee **todos** los ficheros de `profile/`. Mira también
`09-historial-candidaturas.md`: las tecnologías que se repiten en las ofertas que
le interesan son las que deben dominar el perfil.

## 2. Cómo funciona LinkedIn Recruiter (esto decide las decisiones)
- Los reclutadores buscan por **keywords booleanas** sobre titular, extracto,
  experiencia y skills. Una tecnología que no esté escrita **no existe**.
- El **titular** es el campo con más peso en el ranking de búsqueda, y es lo
  único que se ve en los resultados. Aprovecha los 220 caracteres.
- Las **skills** (máx. 50, con 3 destacadas) alimentan el matching de ofertas.
  El orden importa: las 3 primeras son las que se muestran.
- **Ubicación** filtra duro. Si acepta reubicarse, hay que decirlo explícitamente
  en el extracto, porque el filtro geográfico no lo sabe.
- **"Abierto a trabajar"** en modo privado solo lo ven los reclutadores con
  licencia; en modo público lo ve todo el mundo, empleador actual incluido.
  **Avisa siempre de esa diferencia.**
- El perfil en **inglés como versión secundaria** multiplica el alcance
  internacional — pero solo si el nivel declarado lo sostiene.

## 3. Qué generar

### Titular (máx. 220 caracteres)
Fórmula: **rol objetivo · tecnologías núcleo · años o diferenciador**.
Usa la jerarquía de `03-skills.md`: solo tecnologías de nivel *núcleo* y, como
mucho, las de nivel *sólido* que la persona quiera hacer crecer. Nada de "apasionado por".
Genera **3 variantes** con distinto énfasis y recomienda una, explicando qué
tipo de oferta atrae cada una.

### Extracto / "Acerca de" (máx. 2.600 caracteres)
- **Las 3 primeras líneas son lo único visible sin pulsar "ver más".** Ahí va lo
  más fuerte: qué eres, con qué, y el logro más contable del SOT.
- Primera persona, frases cortas, sin corporativismo.
- Estructura sugerida: qué hago y con qué → 2-3 logros con métrica → hacia dónde
  voy (de `07-preferencias.md`) → qué busco y cómo contactarme.
- **Si acepta reubicación o remoto, dilo aquí explícitamente.**
- Termina con un bloque de keywords en texto natural, no una lista suelta.

### Experiencia
Un bloque por puesto: título, empresa, fechas MM/AAAA, ubicación y modalidad.
Descripción de **3-5 líneas en prosa** más 3-4 bullets de logro con métrica.
Reutiliza `01-experiencia.md`, pero reescrito: LinkedIn admite más contexto y
menos telegrama que el CV.

### Aptitudes (skills)
Genera la lista ordenada, hasta 50, en este orden:
1. Las **3 destacadas** (las que definen el perfil y más se buscan)
2. Núcleo
3. Sólidas
4. Acotadas — solo si suman en búsquedas
**Nunca** las *no cubiertas*. Marca cuáles conviene que le validen otras personas.

### Proyectos, formación, idiomas, certificaciones
De `04-proyectos.md` y `02-formacion.md`. Los proyectos con repo público van con
enlace. Idiomas: el nivel real de `08-idiomas-movilidad.md`, sin inflar.

### Ajustes recomendados
- **Abierto a trabajar**: modo privado o público, con el aviso de arriba.
- **URL personalizada** del perfil.
- **Foto y banner**: sí en LinkedIn (al contrario que en el CV). Describe qué
  transmite una buena foto; no la generes.
- **Sección destacada**: qué anclar arriba (repos, proyectos).

## 4. Coherencia con el CV (obligatorio comprobarlo)
LinkedIn y CV se comparan siempre. Verifica y reporta:
- Mismas fechas MM/AAAA en todos los puestos
- Mismos títulos de puesto
- Mismas fechas de titulación
- Ninguna tecnología en LinkedIn que no esté en el SOT

Si detectas una discrepancia con el CV en `salidas/` o con `data/`, **dilo
explícitamente** y di cuál es la versión correcta.

## 5. Salida
Crea `salidas/linkedin-<YYYY-MM-DD>/perfil-linkedin.md`, con una sección por
campo, lista para copiar y pegar, y las 3 variantes de titular al principio.

Si el usuario quiere versión en inglés, genera además `perfil-linkedin-en.md`,
**solo si `08-idiomas-movilidad.md` sostiene ese nivel**; si no, avisa del riesgo
de atraer procesos que no podrá seguir.

## 6. Cierre
Resume: qué keywords cubre el perfil, qué tipo de ofertas debería atraer y qué
tres acciones concretas mejorarían más su visibilidad. Pregunta si quiere la
versión en inglés.
