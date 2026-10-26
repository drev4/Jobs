# Candidatura asistida con Claude Code

Sistema para buscar trabajo de ingeniería de software en **España y Europa** con
[Claude Code](https://claude.com/claude-code). Evalúa cada oferta contra tu perfil
real y, si encaja, genera el material de candidatura a medida: CV ATS en PDF,
lista de skills para el formulario, cover letter, respuestas para Workday y plan
de entrevista.

La idea central: **todo sale de una única fuente de verdad (`profile/`) y nada
se inventa.** Cada línea del CV se puede trazar a un dato de tu perfil, y cada
skill tiene un nivel honesto que decide si lidera el CV, se menciona acotada o
se declara como gap.

## Qué hace

| Comando | Qué obtienes |
|---|---|
| `/crear-perfil` | Rellena tu perfil desde tu CV y una entrevista corta. **Empieza por aquí** |
| `/analizar-oferta` | Veredicto (APLICA YA / CON TRABAJO / TIRO LARGO / NO), % de match con rúbrica ponderada, estimación salarial con research, competencia esperada, gaps y cómo cubrirlos |
| `/generar-cv` | CV a medida en Markdown, HTML y PDF ATS-friendly + skills a declarar + tabla de trazabilidad |
| `/cover-letter` | Carta de presentación (solo si aporta) + versión corta para el mensaje al reclutador |
| `/rellenar-workday` | Respuestas campo a campo para Workday, Greenhouse, SuccessFactors, InfoJobs... coherentes con el CV |
| `/plan-entrevista` | Plan día a día hasta la entrevista: defender lo que sabes, frases honestas para los gaps, preguntas probables |
| `/perfil-linkedin` | Titular, extracto, experiencia y aptitudes optimizados para LinkedIn Recruiter |
| `/plan-formacion` | Qué aprender para **ampliar las ofertas** a las que puedes aplicar, priorizado por gaps reales del historial |

Detalles que marcan la diferencia:
- **Rúbrica de match explícita** (requisitos, seniority, stack, dominio,
  condiciones, trayectoria) con reglas de corte (permiso de trabajo, idioma) y
  tus propias reglas de preferencias.
- **Salario no publicado no es red flag**: lo hace ~95% del mercado español. En su
  lugar, research de empresa y banda estimada con nivel de confianza.
- **Gaps recurrentes**: el historial cuenta qué requisitos te faltan una y otra
  vez y alimenta el plan de formación.
- **Puentes entre skills**: Vue → React o Java → Kotlin cuentan como cobertura
  parcial, no como cero.
- Contexto **España/UE**: modalidades, rangos salariales locales, GDPR (sin foto,
  edad ni DNI en el CV), permisos de trabajo.

## Requisitos

- [Claude Code](https://docs.claude.com/en/docs/claude-code/overview) (CLI, app de escritorio o extensión de IDE).
- Microsoft Edge o Google Chrome, para generar el PDF del CV en modo headless.
- Opcional: LinkedIn Premium. Si lo indicas en tu perfil, el análisis te pedirá
  los datos reales de competencia de cada oferta.

## Instalación

```bash
git clone https://github.com/<tu-usuario>/<este-repo>.git candidaturas
cd candidaturas
mkdir data
# Copia tu CV actual (PDF, DOCX o texto) a data/
claude
```

Dentro de Claude Code:

```
/crear-perfil
```

Copia las plantillas de `profile.example/` a `profile/`, extrae lo que dice tu CV
y te pregunta lo que el CV no puede decir: tu jerarquía real de fortalezas,
salario mínimo, modalidad, idiomas, logros con métricas e historias de
entrevista. Cuanto más honesto seas aquí, mejores serán los análisis.

## Uso diario

```
/analizar-oferta <pega aquí la oferta o su URL>
```

Si el veredicto te convence:

```
/generar-cv
/rellenar-workday        # si aplicas por portal corporativo
/cover-letter            # solo si la piden o aporta
```

Cuando te convoquen:

```
/plan-entrevista
```

Todo lo de una misma oferta queda en `salidas/<empresa>-<puesto>-<fecha>/`.

## Estructura

```
.
├── CLAUDE.md                 # Reglas del sistema para Claude
├── .claude/
│   ├── settings.json         # Permisos compartidos (web, lectura del perfil)
│   └── skills/               # Un SKILL.md por comando
├── profile.example/          # Plantillas del perfil (públicas)
├── templates/cv-ats.html     # Plantilla HTML del CV (una columna, ATS)
│
│   # Generado por ti / por el sistema — ignorado por git:
├── profile/                  # Tu fuente de verdad (00-identidad … 09-historial)
├── data/                     # Tu CV original
├── ofertas/                  # Texto original de cada oferta analizada
├── research/                 # Research de empresas, salarios y competencia
└── salidas/                  # CVs, cartas, formularios y planes generados
```

### El perfil (`profile/`)

| Fichero | Contenido |
|---|---|
| `00-identidad.md` | Contacto, ubicación, disponibilidad, si tienes LinkedIn Premium |
| `01-experiencia.md` | Puestos con fechas MM/AAAA, logros y métricas |
| `02-formacion.md` | Estudios, certificaciones, cursos |
| `03-skills.md` | **Jerarquía de fortalezas** (núcleo / sólido / acotado / no cubierto) y tablas con nivel y evidencia |
| `04-proyectos.md` | Proyectos personales con enlace |
| `05-aprendizaje.md` | Qué estás aprendiendo y planes activos |
| `06-extraprofesional.md` | Historias STAR y soft skills con evidencia |
| `07-preferencias.md` | Rol objetivo, salario mínimo, modalidad, red flags, reglas propias para la rúbrica |
| `08-idiomas-movilidad.md` | Idiomas reales, permisos, reubicación |
| `09-historial-candidaturas.md` | Log de ofertas analizadas y gaps recurrentes (lo mantiene el sistema) |

El fichero más importante es `03-skills.md`: la jerarquía de fortalezas evita
el fallo más común de los CVs generados con IA, que es sobrevender lo
secundario y quedar expuesto en la entrevista técnica.

## Privacidad

`profile/`, `data/`, `ofertas/`, `research/` y `salidas/` contienen datos
personales (contacto, salario, CV) y **están en `.gitignore`**. Antes de hacer
push, comprueba con `git status` que ninguno aparece. Si haces fork, no subas
nunca tu `profile/` real ni lo copies a `profile.example/`.

Las skills hacen búsquedas web (research de empresas y salarios) con WebSearch y
WebFetch; tus datos personales no se envían en esas búsquedas.

## Personalizar

- **Rúbrica y reglas**: `.claude/skills/analizar-oferta/SKILL.md`. Tus
  preferencias personales van mejor en `profile/07-preferencias.md` (sección
  "Reglas propias para la rúbrica"), que manda sobre los defaults.
- **Diseño del CV**: `templates/cv-ats.html`. Mantén una sola columna, sin tablas
  ni iconos, para no romper el parseo ATS.
- **Otro mercado**: las skills asumen España/UE (salarios, GDPR, permisos).
  Adaptarlas a otro país pasa por editar esas secciones.

## Limitaciones

- La estimación salarial y de competencia es research con nivel de confianza,
  no un dato. El sistema lo dice en cada análisis.
- El sistema es tan bueno como tu perfil: niveles inflados en `03-skills.md`
  producen matches optimistas y CVs que no aguantan una entrevista.
- Revisa siempre lo generado antes de enviarlo.
