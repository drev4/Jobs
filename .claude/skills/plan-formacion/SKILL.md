---
name: plan-formacion
description: Diseña un plan de formación en un área concreta (backend, arquitectura, cloud, testing, IA, inglés...) con el objetivo de ampliar el rango de ofertas a las que se puede aplicar con garantías. Calcula qué ofertas desbloquea cada área y prioriza por retorno real. Úsala cuando el usuario pregunte qué aprender, quiera abrir su mercado, o tras detectar gaps recurrentes en el historial.
---

# Plan de formación para ampliar mercado

## 0. Diferencia con `plan-entrevista`
`plan-entrevista` prepara **una oferta concreta**, con fecha y a corto plazo.
Esta prepara **el perfil**, a medio plazo, para que entren ofertas que hoy
quedan fuera. Objetivo distinto: no es aprobar un examen, es **cambiar a qué
ofertas se puede aplicar con garantías**.

## 1. Cargar y diagnosticar
Lee **todos** los ficheros de `profile/`. Presta atención especial a:
- `03-skills.md` — la jerarquía de niveles y el bloque "no cubierto"
- `05-aprendizaje.md` — qué hay en curso y a qué ritmo real
- `07-preferencias.md` — **la dirección a 2-3 años manda sobre todo lo demás**
- `09-historial-candidaturas.md` — **"Gaps recurrentes detectados" es la mejor
  fuente que hay**: son gaps medidos contra ofertas reales, no supuestos

## 2. Elegir el área
Si el usuario nombra el área, trabaja sobre ella — pero **di honestamente si el
retorno es peor que el de otra**, con datos del historial.

Si no la nombra, propón 3 áreas candidatas ordenadas por retorno y deja que elija.
Criterios de retorno, en este orden:
1. **Frecuencia en las ofertas que le interesan** (cuéntala en el historial)
2. **Alineación con la dirección a 2-3 años** de `07-preferencias.md`
3. **Distancia desde lo que ya tiene** — un puente adyacente corto rinde más que
   empezar de cero
4. **Efecto sobre la banda salarial** — di cuánto, y en qué te basas
5. **Caducidad** — una tecnología de moda envejece; un fundamento no

## 3. Definir el objetivo en términos de mercado
Antes del plan, escribe **qué se desbloquea**, en concreto:

| | |
|---|---|
| Área | |
| Nivel actual (escala de `03-skills.md`) | |
| Nivel objetivo | |
| **Qué ofertas desbloquea** | Tipos de puesto y ejemplos reales del historial |
| **Qué NO desbloquea** | Sé explícito: evita expectativas infladas |
| Efecto en banda salarial | Con fuente o marcado como estimación |
| Tiempo total estimado | En horas y en semanas al ritmo declarado |

Si el objetivo no cambia a qué ofertas puede aplicar, **dilo y replantea**.
Aprender por aprender es legítimo, pero esta skill es para ampliar mercado.

## 4. El plan
Por **fases**, no por temas sueltos. Cada fase:
- **Objetivo comprobable** — qué sabrá hacer que hoy no sabe
- **Contenido** — concreto: qué leer, qué curso, qué documentación
- **Proyecto** — la fase se cierra con **algo construido y público**. Sin output,
  no cuenta: no se puede poner en un CV ni defender en una entrevista
- **Horas estimadas** y semanas al ritmo real declarado
- **Cómo se demuestra** — repo, demo desplegada, artículo, certificación
- **Qué añadir al SOT** al terminarla, y con qué nivel

Reglas:
- **Máximo 3 fases.** Un plan de 8 fases no se termina.
- **La primera fase debe dar resultado en 2-4 semanas.** Si el primer hito está a
  tres meses, se abandona.
- Prioriza **profundidad sobre amplitud**: una tecnología a nivel 3-4 abre más
  puertas que cuatro a nivel 2.
- Si hay certificación con valor real en el mercado español/UE, dilo — y di
  también cuándo **no** compensa (la mayoría de las veces, frente a un proyecto).

## 5. Ritmo realista
Pregunta cuántas horas semanales puede dedicar de verdad. Si no lo dice, asume
5-8 h/semana y márcalo como supuesto.

**No infles el plan.** Un plan que no cabe en la vida real del usuario es peor
que no tener plan: genera culpa y se abandona. Si el área requiere más tiempo
del que hay, **dilo y propón un alcance menor**.

Ten en cuenta lo que ya está en curso en `05-aprendizaje.md`: no propongas un
plan que compita con algo que ya está haciendo sin decírselo.

## 6. Salida
Crea `salidas/plan-formacion-<area>-<YYYY-MM-DD>.md` con el diagnóstico, la tabla
de desbloqueo de mercado, las fases y un **calendario por semanas**.

Añade al final una sección **"Cómo saber si está funcionando"**: qué debería
cambiar en los análisis de ofertas dentro de 1, 3 y 6 meses. Métricas concretas:
% de match, gaps que dejan de aparecer, tipos de oferta nuevos.

## 7. Actualizar el SOT
- Añade el plan a `05-aprendizaje.md` con fecha de inicio y estado.
- Al completar cada fase, **sube el nivel de la skill en `03-skills.md` con su
  evidencia**. Sin esto, el sistema seguirá tratando el área como gap.
- Si el plan cambia lo que busca, refleja el matiz en `07-preferencias.md`.

## Formato de salida
En el terminal: el área elegida y por qué, qué desbloquea, las 3 fases en una
línea cada una y el tiempo total. El detalle va al fichero.
Si has descartado otras áreas con mejor retorno, **dilo antes que nada**.
