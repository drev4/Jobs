---
name: crear-perfil
description: Crea o actualiza el SOT de profile/ a partir del CV del usuario (PDF/DOCX/texto en data/), su LinkedIn y una entrevista corta. Úsala en el primer uso del sistema, cuando profile/ no exista o esté vacío, o cuando el usuario diga "actualiza mi perfil", "he cambiado de trabajo" o aporte un CV nuevo.
---

# Crear / actualizar el perfil (SOT)

Todo el sistema depende de `profile/`. Un SOT pobre produce análisis optimistas
y CVs genéricos; un SOT con niveles y evidencia produce candidaturas defendibles.

## 0. Preparar
- Si `profile/` no existe, cópialo desde `profile.example/` (los 10 ficheros).
- Si ya existe, **es una actualización**: no sobrescribas nada sin enseñar el
  cambio. Añade, corrige y marca con fecha (`actualizado DD/MM/AAAA`).
- Busca material en `data/` (CV en PDF, DOCX o texto). Si no hay nada, pide al
  usuario que deje su CV ahí o lo pegue. Lee también, si las da, la URL de su
  LinkedIn o un export del perfil.

## 1. Extraer del CV (sin inventar)
Rellena desde el CV lo que conste literalmente: identidad, puestos con fechas
MM/AAAA, formación, tecnologías mencionadas, logros con métricas, idiomas.
Todo lo que el CV no diga queda como `<!-- PENDIENTE -->`. **No completes huecos
con suposiciones razonables**: un dato inventado en el SOT acaba en un CV.

## 2. Entrevista (en rondas cortas, no un cuestionario de 40 preguntas)
Pregunta lo que el CV no puede decir, por orden de impacto en los análisis:

1. **Jerarquía de fortalezas** (`03-skills.md`): de las tecnologías del CV, cuáles
   son *núcleo* (defendería cualquier profundidad), *sólido* (producción real, no
   especialidad), *acotado* (lo he tocado) y qué gaps conoce (*no cubierto*).
   Es lo más importante del SOT: empújale a ser honesto, no generoso.
2. **Preferencias** (`07-preferencias.md`): rol objetivo y roles que no quiere,
   salario actual y mínimo (remoto / con mudanza), modalidad, ciudades,
   tipo de empresa, sectores descartados, red flags, dirección a 2-3 años.
3. **Idiomas y movilidad** (`08`): nivel real hablado vs leído, nacionalidad y
   permisos, reubicación.
4. **Evidencia de logros** (`01`): para cada puesto, 2-3 logros con número
   (rendimiento, bugs, usuarios, clientes, tiempo). Si no hay número, el contexto.
5. **Historias STAR** (`06`): un problema técnico difícil, un error propio, un
   desacuerdo técnico, mentoring, trato con cliente.
6. **Recursos** (`00`): si tiene LinkedIn Premium, disponibilidad, situación actual.
7. Proyectos personales (`04`) y aprendizaje en curso (`05`).

Tras cada ronda, escribe lo obtenido en su fichero antes de seguir: si la
conversación se corta, lo dicho no se pierde.

## 3. Reglas
- Cada skill en `03-skills.md` lleva **nivel y evidencia** (dónde, cuánto tiempo).
  Sin evidencia, márcala `(?)` y pregunta.
- Fechas siempre `MM/AAAA`. Las mismas que el CV original; si hay discrepancia
  entre CV y LinkedIn, pregunta cuál es la buena y anótalo.
- Mantén `09-historial-candidaturas.md` intacto si ya tiene datos.
- No copies nunca datos reales a `profile.example/`: es la plantilla pública.

## 4. Cierre
En el terminal: qué ficheros se han rellenado, cuántos `PENDIENTE` quedan y
cuáles de ellos afectan más a los análisis (los de `03` y `07` primero).
Propón el siguiente paso: `/analizar-oferta` con una oferta real, o
`/perfil-linkedin`.
