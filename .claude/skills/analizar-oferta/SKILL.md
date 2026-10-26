---
name: analizar-oferta
description: Analiza una oferta de trabajo de software (España/Europa) contra el perfil del usuario en profile/. Devuelve encaje, % de match con rúbrica, nivel de competencia estimado para el puesto, gaps, red flags y un veredicto accionable. Úsala cuando el usuario pegue una oferta, pase una URL de oferta, o pregunte "¿me encaja esto?".
---

# Analizar oferta

## 0. Entrada
La oferta puede llegar como texto pegado, ruta a fichero en `ofertas/`, o URL.
Si es URL, léela con WebFetch. Si el texto está incompleto (falta stack o
requisitos), dilo y analiza con lo que hay, marcando la incertidumbre.

Guarda siempre el texto original en `ofertas/<empresa>-<puesto>-<YYYY-MM-DD>.md`
(slug en minúsculas, sin tildes, con guiones; fecha de hoy). Ese mismo slug es el
de la carpeta `salidas/` que usarán el resto de skills para esta oferta.

## 1. Cargar el perfil
Lee **todos** los ficheros de `profile/`. No analices con memoria parcial.
Si `profile/` no existe o está esencialmente vacío, para y propón `/crear-perfil`.

Busca además la empresa en `research/mercado-y-competencia.md` (si existe): si ya
se analizó otra oferta suya, reutiliza ese research y datos de competencia en vez
de repetirlo, y dilo.

## 2. Extraer la oferta a estructura
Destila la oferta en:
- **Puesto real** (ignora el título de marketing: "Ninja Developer" -> Backend Engineer)
- **Seniority real** (por años pedidos y responsabilidades, no por la etiqueta)
- **Requisitos imprescindibles** — lista literal
- **Requisitos valorables** — lista literal
- **Stack completo** mencionado
- **Responsabilidades** del día a día
- **Condiciones**: modalidad, ciudad, salario publicado, tipo de contrato, idioma de trabajo
- **Empresa**: sector, tamaño aproximado, producto vs consultora
- **Señales implícitas**: qué revela el texto sobre el equipo, la madurez técnica y la deuda técnica

## 2b. Research de la empresa y estimación salarial (obligatorio si no hay banda)

El **~95% de las ofertas españolas no publica salario**, así que la ausencia de
banda no es información: es el estado por defecto. En vez de penalizarla, hay
que **estimar la banda** y decir con qué confianza.

Haz este research **siempre que la oferta no publique salario**:

1. **WebSearch de la empresa**: nombre + "salarios", nombre + Glassdoor,
   nombre + Levels.fyi, nombre + "financiación"/"ronda"/"funding".
   Busca también el nombre en Glassdoor/Indeed España directamente.
2. **Tamaño, financiación y madurez**: LinkedIn (nº de empleados), notas de
   prensa, rondas levantadas, si es filial/spin-off de un grupo mayor. Una
   startup con ronda Serie A reciente paga distinto que una bootstrapped.
3. **Producto vs consultora**: las consultoras españolas pagan por debajo a
   igualdad de stack. Detecta el patrón y dilo.
4. **Comparables del mercado**: puesto + seniority + ciudad. Usa referencias
   públicas (informes de Michael Page / Hays / Robert Walters, encuestas
   sectoriales, ofertas equivalentes que sí publican banda).
5. **Señales del propio texto**: rango de años pedido (una oferta calibrada a
   3-5 años paga menos que la misma a 6-8), stack de nicho (sube), sector
   regulado (sube), "sueldo según valía" (baja), beneficios enumerados en vez
   de salario (suele indicar banda modesta).

Entrega una tabla así, y **di siempre en qué te basas y con qué confianza**:

| | Estimación |
|---|---|
| Banda estimada | X – Y € brutos/año |
| Confianza | alta / media / baja + por qué |
| Base del cálculo | fuentes concretas usadas |
| ¿Supera mi umbral? | sí / no / depende del tramo |

Si el research no da nada sólido, **dilo abiertamente** y estima solo por
comparables de mercado, marcando confianza baja. **Nunca inventes cifras
presentándolas como dato.**

Usa la banda estimada para puntuar la dimensión "Condiciones". Si la estimación
queda por debajo del umbral de `07-preferencias.md`, dilo como el riesgo
principal de la candidatura y conviértelo en la primera pregunta a hacer.

## 3. Rúbrica de match (usa exactamente estos pesos)

| Dimensión | Peso | Cómo puntuar 0-100 |
|---|---|---|
| Requisitos imprescindibles | 40 | % de "must" cubiertos con **evidencia en el SOT**. Un must no cubierto pesa el doble que uno cubierto. |
| Seniority y años | 15 | 100 si estoy en el rango; 70 si estoy 1 año por debajo; 40 si 2+; 60 si estoy claramente por encima (riesgo de descarte por sobrecualificación/salario) |
| Stack secundario / valorables | 15 | % de valorables cubiertos |
| Dominio y sector | 10 | Experiencia previa en ese dominio (fintech, salud, ecommerce...) |
| Condiciones vs mis preferencias | 15 | Modalidad, ciudad, salario e idioma contra `07-preferencias.md` y `08-idiomas-movilidad.md` |
| Trayectoria (¿me acerca a mi objetivo?) | 5 | Contra "Dirección a 2-3 años" |

**Match final = suma ponderada, redondeada a entero.**

Muestra la tabla con la puntuación de cada dimensión y una frase de justificación
por fila. Nada de números sin justificar.

**Reglas de corte** (aplican después del cálculo, y se anuncian explícitamente):
- Requisito legal no cumplido (permiso de trabajo, titulación obligatoria, idioma
  de trabajo por debajo de mi nivel) -> match máximo 25, veredicto NO.
- Red flag de `07-preferencias.md` presente -> márcalo, resta 10 puntos y explícalo.
  - **Excepción explícita: el salario no publicado NO es red flag y no resta
    nada.** Es el comportamiento del ~95% del mercado español. Se sustituye por
    el research del paso 2b. Sí es red flag que **se nieguen a dar la banda al
    preguntarla**, o que la banda estimada/confirmada quede bajo el umbral.
  - **Aplica las reglas propias de `07-preferencias.md`** sobre modalidad
    (p. ej. si remoto e híbrido pesan igual y solo penaliza la mudanza) y sobre
    tipo de rol (p. ej. qué variante de un rol no penaliza en "Trayectoria").
    Esas reglas mandan sobre cualquier default de esta rúbrica; anúncialas.
- Menos del 50% de los "must" cubiertos -> veredicto máximo "TIRO LARGO".

## 4. Nivel de competencia estimado

### 4.0 Pide primero los datos de LinkedIn Premium
Solo si `00-identidad.md` indica que el usuario **tiene LinkedIn Premium** y la
oferta viene de LinkedIn: **pídele estos datos antes de estimar nada**, porque
convierten este apartado entero de estimación en dato:

- **Nº real de candidatos** (no "clics en Solicitar", que infla mucho).
- **Desglose de candidatos**: seniority, años de experiencia, formación.
- **En qué percentil queda él** respecto a esa muestra.
- **Cuántos candidatos tienen cada skill** que pide la oferta.
- **Rango salarial estimado por LinkedIn** para el puesto y la zona.
- **Datos de plantilla y crecimiento** de la empresa.

Pídelos con una frase corta y concreta, no con un cuestionario. Si te los da,
**úsalos como fuente principal y dilo**; si no, estima y márcalo como estimación.
El dato de "cuántos candidatos tienen la skill X" es especialmente valioso: es lo
que dice si un requisito es un filtro real o decorativo.

Si LinkedIn da rango salarial, **incorpóralo al paso 2b** y contrástalo con los
comparables de mercado: si divergen, dilo y explica por qué.

### 4.1 Estimación
No inventes cifras. Estima con razonamiento explícito y di en qué te basas:
- **Volumen de candidatos esperado**: alto / medio / bajo, según remoto vs presencial,
  stack popular vs de nicho, si la empresa es conocida, si el salario es atractivo,
  si es un puesto junior (siempre saturado en España).
- **Perfil del competidor típico** para esa oferta.
- **Mi posición relativa**: ¿en qué percentil aproximado caigo y por qué?
- **Mis 2-3 diferenciadores reales** frente a ese competidor típico.
- **Probabilidad estimada de pasar el primer filtro**: alta / media / baja + motivo.

Contexto España/UE que debes tener en cuenta:
- Los juniors compiten con cientos de candidatos; los perfiles mid con stack de
  nicho, con decenas.
- Remoto europeo = competencia continental, no local.
- Una banda salarial publicada y alta atrae más candidatos; no publicarla es lo
  normal y no reduce la competencia por sí solo.
- Muchas ofertas en España son de consultoría intermediando para un cliente final.
  Detecta ese patrón y dilo.

## 5. Gaps y cómo mitigarlos
Para cada requisito no cubierto:
- ¿Es bloqueante o negociable?
- ¿Tengo algo **adyacente** en el SOT que sirva de puente? (ej: piden Kotlin, tengo Java)
- ¿Se puede cubrir antes de la entrevista? (con qué y en cuánto tiempo)

**Antes de declarar un gap limpio, comprueba las familias de skills** que
`03-skills.md` marca explícitamente como puente (p. ej. una familia de APIs de
render en cliente como Google Maps/D3/PDF.js cubre parcialmente OpenLayers,
Leaflet o Canvas; Vue cubre parcialmente React; Java cubre parcialmente Kotlin). Un requisito con puente adyacente fuerte **puntúa como cobertura
parcial, no como cero**, y se presenta como "no lo he usado, pero he resuelto
esta misma clase de problema con X".

## 6. Veredicto
Uno de: **APLICA YA** (>=75) · **APLICA CON TRABAJO** (60-74) · **TIRO LARGO** (45-59) · **NO** (<45).
Una frase de recomendación concreta y, si aplica, qué hacer antes de enviar.

## 7. Registrar
Añade una fila a `profile/09-historial-candidaturas.md` y, si el gap detectado ya
aparece en filas anteriores, súbelo a "Gaps recurrentes detectados" (incrementa
el contador; no dupliques filas del mismo gap).

El research detallado de empresa, salario y datos de LinkedIn Premium va a
`research/mercado-y-competencia.md` (crea el fichero si no existe), bajo un
encabezado `### <Empresa> · <Puesto> · <DD/MM/AAAA>`. **No lo metas en el
historial**: se carga en cada skill y debe mantenerse corto.

Si durante el análisis el usuario confirma un dato nuevo sobre sí mismo (una
skill, una preferencia), actualiza el fichero del SOT correspondiente.

## 8. Cierre
Pregunta si quiere que genere el CV a medida (`/generar-cv`) y la cover letter.
No los generes sin confirmación.

## Formato de salida
Markdown en el terminal, en este orden: veredicto y % primero (una línea),
luego la tabla de rúbrica, **la estimación salarial del paso 2b**, competencia,
gaps, y acción recomendada.
Sin preámbulos.
