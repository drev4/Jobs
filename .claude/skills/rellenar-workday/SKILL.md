---
name: rellenar-workday
description: Genera todas las respuestas para rellenar una solicitud de empleo en Workday (myworkdayjobs.com) o portales equivalentes (Greenhouse, SuccessFactors, Taleo, InfoJobs), a partir del SOT de profile/ y del análisis de la oferta. Devuelve un fichero campo a campo, listo para copiar y pegar. Úsala cuando el usuario vaya a aplicar a una oferta por un portal corporativo, diga "voy a rellenar la solicitud", o pegue las preguntas de un formulario.
---

# Rellenar solicitud de Workday

## 0. Entrada
Necesitas:
- La **oferta** (fichero en `ofertas/`, texto pegado o URL).
- Si existe, el **análisis previo** y el CV generado en `salidas/`. Reutilízalos:
  la solicitud debe decir **exactamente lo mismo** que el CV. Una incoherencia
  entre CV y formulario es una bandera roja automática en cualquier ATS.

Si el usuario pega las preguntas literales del formulario, respóndelas en ese
orden. Si no, usa el guion estándar de la sección 3.

Lee **todos** los ficheros de `profile/`.

## 1. Regla inviolable
Igual que en el CV: **cada respuesta trazable al SOT**. Nada inventado.
Y además: **coherencia total con el CV enviado**. Mismos años, mismas fechas,
mismos títulos de puesto, mismas tecnologías. Los ATS comparan ambos.

## 2. Cómo se comporta Workday (contexto que cambia las respuestas)
- **Parsea el CV y prerrellena** los campos. Suele equivocarse con fechas y
  títulos: avisa al usuario de que **revise lo autocompletado**, no solo lo vacío.
- **Los campos de skills son de autocompletado sobre un catálogo cerrado.** Si la
  skill exacta no aparece, hay que elegir la más próxima. Da alternativas.
- **Muchos campos son irreversibles** una vez enviado. Avisa de cuáles.
- **"Expected salary" suele ser obligatorio** y no admite "negociable". Prepara
  una cifra defendible (sección 5).
- El **CV se sube igual**: rellenar el formulario no lo sustituye.

## 3. Campos a generar
Genera respuestas para todos estos, marcando cuáles no aplican:

### Datos personales
Nombre, apellidos, email, teléfono (con prefijo internacional), país, ciudad,
provincia — todo de `00-identidad.md`.
**Nunca** dirección completa, DNI, fecha de nacimiento, estado civil ni foto,
salvo que el formulario los exija por ley. Si los exige, dilo y explica por qué.

### Elegibilidad
- ¿Autorización para trabajar en el país? → según nacionalidad y permisos de
  `08-idiomas-movilidad.md` y el país de la oferta.
- ¿Necesitas patrocinio de visado? → según `08-idiomas-movilidad.md` (un
  ciudadano UE no lo necesita dentro del EEE ni en Suiza).
- ¿Has trabajado antes en la empresa? → según el SOT.
- Disponibilidad de incorporación → de `00-identidad.md`.

### Experiencia laboral
Cada puesto con: título, empresa, ubicación, MM/AAAA–MM/AAAA, y una descripción
de **3-5 líneas** reescrita para esta oferta. **No copies el bullet del CV tal
cual**: Workday muestra estos campos como texto corrido, no como lista.

### Formación
Titulación, centro, fechas, país. Nota media solo si es alta y la piden.

### Idiomas
Con la escala del formulario. **Nunca por encima de lo que sostiene
`08-idiomas-movilidad.md`.** Si el perfil es asimétrico (p. ej. comprensión C1,
producción B1-B2), elige el nivel defendible en una conversación, no el de
lectura, y explica la elección.

### Skills
Reutiliza `skills-formulario.md` de `salidas/` si existe. Si no, genera los tres
bloques (declarar sí / con matiz / no declarar) según la sección 7 de `generar-cv`.

### Preguntas abiertas
Las típicas: "¿por qué quieres trabajar aquí?", "¿por qué encajas?", "cuéntanos
un logro". Máximo 150-200 palabras cada una, concretas, con una métrica del SOT.
**Sin adjetivos vacíos ni frases de plantilla.**

### Preguntas de diversidad y datos protegidos
Género, discapacidad, origen étnico, veteranía. **Son voluntarias por ley en la
UE.** Di al usuario que puede marcar "prefiero no contestar" sin ningún perjuicio,
y que esos datos no llegan al equipo de selección. No respondas por él.

## 4. Motivación y encaje: cómo escribirlos
Fórmula: **qué hace la empresa que me interesa de verdad (concreto, sacado de la
oferta o del research) + qué traigo yo que encaja (con evidencia del SOT) + qué
busco (de `07-preferencias.md`)**.

Prohibido: "empresa líder del sector", "apasionado por la tecnología", "siempre
he querido". Si la frase vale para cualquier empresa, está mal escrita.

## 5. Expectativa salarial
Este campo hunde candidaturas. Reglas:
1. Parte de la **banda estimada en el paso 2b de `analizar-oferta`**.
2. Aplica los umbrales salariales de `07-preferencias.md` (p. ej. mínimo en
   remoto / con mudanza) como **suelo, nunca como cifra a pedir**.
3. Pide **una cifra en el tercio superior de la banda estimada**, no el suelo:
   en España se negocia a la baja desde lo que pides.
4. Si el campo admite texto, propón rango. Si solo admite número, da la cifra
   única y explica por qué esa.
5. **Avisa siempre** de que esta cifra ancla toda la negociación posterior.

## 6. Salida
Crea `salidas/<empresa>-<puesto>-<YYYY-MM-DD>/solicitud-workday.md` con:
- Una sección por campo, con la respuesta **lista para copiar y pegar**
- Los campos que requieren decisión del usuario, marcados `⚠️ DECIDIR`
- Una **checklist final** antes de enviar
- Un aviso de qué campos son irreversibles

Si ya existe la carpeta de la oferta, escribe dentro. No crees una nueva.

## 7. Checklist final (inclúyela siempre en la salida)
- [ ] Las fechas del formulario coinciden **exactamente** con las del CV
- [ ] Los títulos de puesto coinciden con los del CV
- [ ] Ninguna skill declarada sin evidencia en el SOT
- [ ] Idiomas declarados al nivel real, no inflado
- [ ] CV adjunto en PDF, con nombre de fichero profesional
- [ ] Expectativa salarial decidida conscientemente
- [ ] Revisado lo que Workday autocompletó, no solo lo que estaba vacío
- [ ] Preguntas de diversidad: respondidas o marcadas "prefiero no contestar"

## 8. Registrar
Marca en `profile/09-historial-candidaturas.md` la columna "¿Apliqué?" con la
fecha (`Sí (DD/MM)`). Si la solicitud revela requisitos nuevos que no estaban en la oferta
publicada, añádelos al análisis.

## Formato de salida
En el terminal: resumen corto de qué has generado, los `⚠️ DECIDIR` y la
expectativa salarial recomendada con su justificación. El detalle campo a campo
va al fichero, no al terminal.
