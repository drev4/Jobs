# Sistema de candidatura asistida — Ingeniería de Software (España / Europa)

## Qué es esto
Un sistema para evaluar ofertas de trabajo contra el perfil real del usuario y,
si encajan, generar material de candidatura a medida (CV, lista de skills, cover
letter, respuestas de formulario, plan de entrevista).

## Primer uso
Si `profile/` no existe o está esencialmente vacío, **no analices nada**: ejecuta
`/crear-perfil`, que copia las plantillas de `profile.example/` y las rellena
a partir del CV del usuario (en `data/`) y de una entrevista corta.

## Fuente de verdad (SOT)
Todo el conocimiento sobre el usuario vive en `profile/`. **Nunca inventes datos
que no estén ahí.** Si falta algo relevante, pregúntalo y añádelo al fichero
correspondiente.

| Fichero | Contenido |
|---|---|
| `profile/00-identidad.md` | Datos de contacto, ubicación, disponibilidad, links, recursos (p. ej. LinkedIn Premium) |
| `profile/01-experiencia.md` | Empleos, proyectos profesionales, logros con métricas |
| `profile/02-formacion.md` | Estudios reglados, certificaciones, cursos |
| `profile/03-skills.md` | **Jerarquía de fortalezas** + lenguajes, frameworks, herramientas con nivel y evidencia |
| `profile/04-proyectos.md` | Proyectos personales / open source |
| `profile/05-aprendizaje.md` | Qué está aprendiendo ahora y a qué ritmo |
| `profile/06-extraprofesional.md` | Soft skills con evidencia e historias de entrevista (STAR) |
| `profile/07-preferencias.md` | Qué quiere y qué no: rol, stack, salario, modalidad, sector, red flags, reglas propias de la rúbrica |
| `profile/08-idiomas-movilidad.md` | Idiomas, permisos de trabajo, disponibilidad geográfica |
| `profile/09-historial-candidaturas.md` | Log de ofertas analizadas, gaps recurrentes y patrones |

Fuera del SOT (se consultan **bajo demanda**, no en cada skill):
- `research/mercado-y-competencia.md` — research de empresas y salarios, datos de
  competencia de LinkedIn Premium, comparables de mercado y correcciones al sistema.
  Léelo cuando la oferta sea de una empresa ya analizada o necesites comparables.
- `ofertas/` — texto original de cada oferta.
- `data/` — CV original del usuario (referencia para coherencia).
- `templates/cv-ats.html` — plantilla del CV.

## Flujo de trabajo

### Por oferta
1. `/analizar-oferta` — pego la oferta, obtengo veredicto + % match + competencia
   + research de empresa y estimación salarial
2. Si decido seguir: `/generar-cv` — CV a medida en Markdown + HTML + PDF
3. `/cover-letter` — solo si la oferta la pide o aporta valor
4. `/rellenar-workday` — respuestas campo a campo para el formulario del portal
   (Workday, Greenhouse, SuccessFactors, InfoJobs...)
5. `/plan-entrevista` — plan de preparación cuando me convocan (o antes, si
   quiero cerrar gaps antes de aplicar)

### Transversales (no dependen de una oferta)
- `/crear-perfil` — poblar o actualizar el SOT desde un CV y una entrevista
- `/perfil-linkedin` — contenido completo del perfil: titular, extracto,
  experiencia, aptitudes y ajustes de visibilidad
- `/plan-formacion` — plan de estudio en un área para **ampliar el rango de
  ofertas** a las que puedo aplicar con garantías

### Datos de LinkedIn Premium
Si `profile/00-identidad.md` indica cuenta Premium y la oferta viene de LinkedIn,
`/analizar-oferta` **pide** los datos de competencia (nº de candidatos, desglose
por seniority y formación, skills que tienen). Convierten la estimación de
competencia en dato real.

## Reglas duras
- **Cero invención.** Nada de tecnologías, años o logros que no consten en el SOT.
  Se puede reformular, priorizar y traducir a la jerga de la oferta; no fabricar.
- **Respeta la jerarquía de fortalezas** de `profile/03-skills.md` (sección al
  principio del fichero). Tener una tecnología en el SOT no la convierte en
  fortaleza: cada skill tiene un nivel (**núcleo / sólido / acotado / no
  cubierto**) y ese nivel decide si lidera el CV, si se menciona, o si se declara
  como gap. Sobrevender lo secundario es el fallo más probable de este sistema y
  el que peor sale en una entrevista técnica.
- **Las preferencias del usuario mandan sobre los defaults de las skills.** Si
  `07-preferencias.md` define una regla (umbral salarial, modalidad, qué penaliza
  y qué no), se aplica tal cual y se anuncia en el análisis.
- Contexto **España/UE**: convenios, jornada, modalidades (presencial/híbrido/remoto),
  rangos salariales locales, requisitos de permiso de trabajo, GDPR.
- El CV debe pasar filtros **ATS**: sin tablas, sin columnas, sin gráficos, sin
  iconos, sin cabeceras/pies, fuentes estándar, secciones con nombres canónicos.
- Salidas a `salidas/<empresa>-<puesto>-<YYYY-MM-DD>/` (slug en minúsculas, sin
  tildes, con guiones). Todas las skills de una misma oferta escriben en **esa
  misma carpeta**; no se crean carpetas nuevas. La fecha es la del análisis y
  coincide con el nombre del fichero en `ofertas/`.
  Las transversales van a `salidas/linkedin-<fecha>/` y
  `salidas/plan-formacion-<area>-<fecha>.md`.
- Cada análisis se registra en `profile/09-historial-candidaturas.md` (fila +
  gaps recurrentes). El research detallado va a `research/mercado-y-competencia.md`,
  no al historial: el historial se carga en cada skill y debe seguir siendo corto.
- **Coherencia entre entregables:** CV, formulario y LinkedIn deben decir lo
  mismo — mismas fechas MM/AAAA, mismos títulos, mismas tecnologías. Una
  discrepancia entre ellos es bandera roja para cualquier reclutador.
- **El aprendizaje solo cuenta si se registra.** Cuando se cubre un gap, hay que
  subir el nivel en `profile/03-skills.md` con su evidencia; si no, el siguiente
  análisis lo volverá a marcar como gap.
- **Salario no publicado no es red flag** (lo hace el ~95% del mercado español):
  se estima con research. Ver paso 2b de `analizar-oferta`.
- **Privacidad:** `profile/`, `data/`, `ofertas/`, `salidas/` y `research/`
  contienen datos personales y están en `.gitignore`. No los muevas a rutas
  versionadas ni copies datos reales a `profile.example/`.
