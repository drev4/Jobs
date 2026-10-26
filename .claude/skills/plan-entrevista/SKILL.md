---
name: plan-entrevista
description: Genera un plan de estudio y preparación para una oferta concreta, calibrado al tiempo disponible. Cubre los gaps técnicos de esa oferta, prepara las historias de entrevista del SOT y anticipa las preguntas que van a hacer. Úsala cuando al usuario le convoquen a una entrevista técnica, o antes de aplicar si quiere cerrar gaps primero.
---

# Plan de preparación para una oferta

## 0. Entrada
Necesitas la oferta y, si existe, su análisis previo (los gaps ya están
identificados ahí — no los recalcules desde cero, reutilízalos).

**Pregunta siempre dos cosas antes de planificar**, porque cambian todo el plan:
1. **¿Cuánto tiempo hay?** (días hasta la entrevista, u "aún no me han llamado")
2. **¿Cuántas horas al día puede dedicar** de forma realista, entre semana y en
   fin de semana?

Si no lo sabe, asume 1-2 h entre semana y 4 h en fin de semana, y dilo.

Lee **todos** los ficheros de `profile/`, y el research de la empresa en
`research/mercado-y-competencia.md` si existe.

## 1. Dos modos

### Modo A — Entrevista convocada (hay fecha)
Prioridad absoluta: **lo que más probabilidad tiene de salir en esa entrevista**.
No es momento de aprender tecnologías nuevas: es momento de **poder defender lo
que ya sabes** y de no quedarse en blanco en lo que no.

### Modo B — Aún sin convocatoria
Hay margen para cerrar gaps de verdad, con output tangible (un repo, una demo).
Prioriza lo que además **sirva para otras ofertas**, no solo para esta.
Si el gap es recurrente en `09-historial-candidaturas.md`, sube su prioridad.

Di explícitamente en qué modo estás trabajando.

## 2. Qué se prepara, por orden de retorno

### 2.1 Defender lo que ya tengo (siempre lo primero)
El fallo más caro no es no saber algo: es **no saber explicar lo que sí sabes**.
Para cada tecnología del SOT que la oferta pide como *must*:
- ¿Puedo explicar **por qué** se hizo así, no solo qué se hizo?
- ¿Aguanto tres "¿y por qué?" seguidos?
- ¿Tengo el número a mano? (las métricas del SOT)

Marca las que estén flojas: eso es estudio, aunque sea "algo que ya sé".

### 2.2 Gaps, clasificados por lo que se puede hacer con ellos
| Tipo | Qué hacer |
|---|---|
| **Cubrible con práctica** (una librería, una herramienta) | Proyecto mínimo con output público. Estimación de horas realista |
| **Cubrible con lectura** (un concepto, un patrón) | Entender para conversar, no para implementar. Di qué leer, en concreto |
| **No cubrible a tiempo** | **Preparar la frase honesta.** Ver 2.3 |
| **Con puente adyacente** (ver `03-skills.md`) | Preparar la analogía: "no he usado X, pero he resuelto esa clase de problema con Y" |

**No planifiques aprender algo que no da tiempo.** Es la trampa clásica: se
llega a la entrevista a medias en todo. Mejor tres cosas sólidas y una frase
honesta que cinco cosas superficiales.

### 2.3 La frase honesta para cada gap no cubrible
Redacta la frase literal, y sigue la regla del SOT: **acotar sin disculparse**.
Estructura: qué no tengo → qué tengo cerca → qué haría para cubrirlo.
Nunca "no tengo ni idea", nunca inflar.

### 2.4 Historias de entrevista
De `06-extraprofesional.md`. Mapea **qué historia responde a qué pregunta
probable** de esta oferta concreta. Si una historia necesita adaptarse al
contexto de la empresa, dilo.
Comprueba que hay historia preparada para las clásicas: un problema técnico
difícil, un error propio, un desacuerdo técnico, tu punto débil, por qué te vas.

### 2.5 Preguntas que van a hacer
Deriva de la oferta y del research de la empresa, no de una lista genérica.
Separa: **técnicas de conocimiento**, **de experiencia** ("cuéntame cuándo..."),
**de diseño/arquitectura** y **de encaje cultural**.
Marca las 5 más probables.

### 2.6 Preguntas que hacer yo
5-8, específicas de esa empresa, sacadas del research y de
`07-preferencias.md`. Deben servir para **decidir si le interesa el puesto**, no
solo para parecer interesado. Incluye siempre las incómodas necesarias: banda
salarial, composición del equipo, cómo se toman las decisiones técnicas.

### 2.7 Prueba técnica: qué formato esperar
Deduce del texto de la oferta qué tipo de prueba es probable (live coding, pair
programming, take-home, system design, preguntas teóricas) y prepara para ese
formato. Una empresa que dice "Extreme Programming" hará pair programming; una
que dice "arquitectura" hará diseño en pizarra.

## 3. El plan
Genera un **calendario día a día** hasta la fecha (Modo A) o un plan por semanas
(Modo B), con:
- Bloques con **horas estimadas reales**, ajustadas a la disponibilidad declarada
- Qué se hace en cada bloque, en concreto (no "estudiar .NET")
- **Output verificable** por bloque: un repo, un resumen escrito, una explicación
  grabada, un ejercicio resuelto
- Un **día de repaso** antes de la entrevista, sin material nuevo

Sé honesto con el tiempo: si no cabe, **dilo y recorta**, no comprimas.

## 4. Salida
Crea `salidas/<empresa>-<puesto>-<YYYY-MM-DD>/plan-entrevista.md`.
Si ya existe la carpeta de la oferta, escribe dentro.

Incluye al final una **checklist del día anterior**: material repasado, preguntas
propias escritas, logística (dirección, hora, enlace, con quién), y —si es
online— comprobación de cámara, micro y compartir pantalla.

## 5. Actualizar el SOT
Si durante la preparación se cubre un gap real, **añádelo a `03-skills.md` o a
`05-aprendizaje.md`** con su evidencia. El aprendizaje solo cuenta si queda
registrado; si no, el siguiente análisis lo volverá a marcar como gap.

## Formato de salida
En el terminal: el modo, el tiempo disponible, las 3 prioridades del plan y lo
que se ha decidido **no** preparar (y por qué). El calendario detallado va al
fichero.
