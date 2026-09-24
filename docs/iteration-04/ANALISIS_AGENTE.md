# Análisis del agente — sesión de ocurrencia, representaciones y discrepancias

> **Status:** DRAFT
> **Editable:** sí; análisis derivado, no fuente propietaria de ningún concepto
> **Document owner:** asistente (a petición de Miguel), pendiente de contraste del equipo
> **Canonical for:** —
> **Sources:** [`ENUNCIADO.md`](ENUNCIADO.md) de esta iteración,
> [`domain-objects/DESIGN_OCCURRENCE.md`](../domain-objects/DESIGN_OCCURRENCE.md),
> [`RELATIONSHIPS.md`](../RELATIONSHIPS.md), [`RULES.md`](../RULES.md),
> [`VOCABULARY.md`](../VOCABULARY.md), [`ENTITY_SUMMARY.md`](../ENTITY_SUMMARY.md),
> [`iteration-02/ENUNCIADO.md`](../iteration-02/ENUNCIADO.md) (incluida la sesión
> del 23 de septiembre), [`iteration-02/NOTAS_TIPO_ESTADO_DISENO.md`](../iteration-02/NOTAS_TIPO_ESTADO_DISENO.md),
> [`iteration-02/NOTAS_CORRESPONDENCIA_FISICO_ANALITICA.md`](../iteration-02/NOTAS_CORRESPONDENCIA_FISICO_ANALITICA.md),
> [`iteration-03/NOTAS_REVISION_VS_RECALCULO.md`](../iteration-03/NOTAS_REVISION_VS_RECALCULO.md)
> y [`research/IFC_CORE_CONCEPTS.md`](../research/IFC_CORE_CONCEPTS.md).
> **Supersedes:** —
> **Last reviewed:** 2026-09-24

## Cómo leer este documento

Cada afirmación lleva una etiqueta. No se presenta ninguna hipótesis como
decisión tomada:

| Etiqueta | Significado |
|---|---|
| `[ACUERDO]` | Ya está registrado como consenso en una fuente propietaria existente; aquí solo se conecta o reutiliza. |
| `[HIPÓTESIS]` | Afirmación de la sesión aportada, todavía sin contraste del equipo. |
| `[ALTERNATIVA]` | Camino posible entre varios, sin inclinar la balanza. |
| `[RECOMENDACIÓN]` | Sugerencia del agente; el equipo puede descartarla. |
| `[PENDIENTE]` | Decisión que solo puede tomar el equipo. |

Nada de este documento promueve contenido a `CANONICAL`. Es un análisis
derivado; las fuentes propietarias enlazadas siguen siendo la autoridad.

## 1. Próximos pasos priorizados

`[RECOMENDACIÓN]` Orden sugerido, de mayor a menor efecto de bloqueo sobre el
resto del trabajo:

1. **Cerrar la reformulación de `EstadoDeDiseño`** (persistido / calculado /
   snapshot validado, punto 3). Casi todo lo demás depende de esta decisión:
   Discrepancia necesita saber qué compara, y la sesión del 23 de septiembre ya
   asume una noción de "estado" que esta reformulación podría alterar (ver
   sección 9).
2. **Formalizar `Discrepancia` como entidad**, aprovechando que ya existen
   reglas que la sustentan (`RULES.md` 5, 12, 15) y un caso ya resuelto en
   `iteration-03` (bandejas de piping, arriostramientos). Es la pieza con más
   evidencia acumulada de las tres.
3. **Reconciliar los 5 significados de "tipo"** de esta sesión con la duda ya
   abierta sobre `HEB 300` en `NOTAS_TIPO_ESTADO_DISENO.md` (punto 7): esa nota
   preguntaba "tipo o clasificación"; esta sesión añade tres significados más
   que no estaban contemplados.
4. **Resolver la transferencia de información entre disciplinas** (punto 8),
   reutilizando el criterio de "¿de quién es este dato?" ya propuesto en
   `iteration-03`.
5. **Diseñar el "entorno común"** (punto 6) — deliberadamente en último lugar:
   es una decisión de arquitectura/herramienta, y `AGENTS.md` pide mantener
   separada la conceptualización del dominio de esas decisiones mientras no
   sean necesarias.

## 2. Deberes concretos para la siguiente sesión

`[RECOMENDACIÓN]`

- Cada persona trae **un ejemplo real de discrepancia vivida** (un caso donde
  STAAD cambió y la maqueta no, o viceversa) para servir de caso de contraste
  al formalizar la entidad.
- Ángel prepara **un ejemplo de una misma familia de elemento** (p. ej.
  columna) mostrando sus 5 significados de "tipo" por separado: clase,
  variante geométrica, plantilla de catálogo, agrupación documental, estándar
  vs. especial. Si algún significado no aplica a su ejemplo, decirlo
  explícitamente en vez de forzarlo.
- Miguel aporta el caso de bandejas de piping de `iteration-03` como primer
  intento de resolver el punto 8 con el criterio ya propuesto allí.
- Alguien trae **2–3 ejemplos concretos de elementos secundarios** (una
  barandilla permanente de acceso, una escalera de mantenimiento, un grating
  temporal de montaje) y aplica la prueba de individualidad/continuidad/razón
  de negocio ya existente en `DESIGN_OCCURRENCE.md` a cada uno, para ver si
  alguno sí necesita ser `OcurrenciaDeDiseño` y otro no.
- Si es posible, una captura o export real de cómo STAAD o SP3D versionan
  internamente (no para adoptar su modelo, solo como evidencia comparativa,
  igual que se ha hecho con IFC).

## 3. Decisiones que deben cerrarse antes de implementar

`[PENDIENTE]` — ninguna de estas tiene todavía respuesta en el repositorio:

1. Persistencia vs. cálculo dinámico vs. snapshot de `EstadoDeDiseño`.
2. Autoridad y ciclo de vida completo de `Discrepancia` (quién decide, cómo se
   evita notificación repetida, qué pasa si nadie decide nunca).
3. Si el tipo es **referencia viva**, **plantilla**, o ambas cosas según el
   tipo concreto — esto cambia el comportamiento de `está tipado por` de forma
   incompatible entre las dos opciones.
4. Al menos si habrá **más de un ámbito de catálogo** (corporativo/proyecto),
   aunque no se cierre el detalle de cada uno.
5. **Source of truth por atributo** — sin esto, el "entorno común" no puede
   decidir razonablemente qué representación prevalece ante una discrepancia.

## 4. Conceptos que necesitan ejemplos o contraejemplos

`[RECOMENDACIÓN]`

| Concepto | Ejemplo a favor | Contraejemplo a buscar |
|---|---|---|
| Estado derivado | Una ocurrencia con maqueta y analítico alineados | Una ocurrencia con representación analítica pero **sin** representación física todavía (prediseño) — ¿tiene estado válido? |
| Discrepancia real | Bandeja añadida en maqueta, ausente en STAAD (`iteration-03`) | Un cambio que **no** debería generar discrepancia — elemento auxiliar sin relevancia estructural (ya resuelto en `iteration-03`, reutilizar) |
| Tipo vivo vs. plantilla | `HEB 300`: si el catálogo corrige un dato, ¿deben cambiar todas las columnas que lo usan? | Un "tipo de zapata estándar del proyecto X" que cada zapata copia y luego modifica libremente sin arrastrar a las demás |
| Elemento secundario como ocurrencia | Escalera de acceso permanente, aparece en mediciones y fabricación | Barandilla temporal de montaje, sin trazabilidad ni fabricación propia |

## 5. Artefactos a preparar

`[RECOMENDACIÓN]`, distinguiendo qué es útil ya y qué sería prematuro:

**Ahora:**
- **Glosario** — no crear uno nuevo; extender `VOCABULARY.md` con los 5
  significados de "tipo" (regla de fuente única de `AGENTS.md`).
- **Diagrama simple** — un único diagrama del recorrido `Ocurrencia →
  Representaciones → Estado (¿derivado?) → Discrepancia`, en texto o imagen,
  para fijar vocabulario visual sin comprometer implementación.
- **Matriz de autoridad** — es justo lo que falta para resolver "quién
  decide" en `Discrepancia`, en la aceptación sin recálculo de `iteration-03`
  y en la aceptación de versiones de la sesión del 23 de septiembre. Un único
  artefacto puede servir a las tres preguntas.

**Después, cuando se cierren los puntos 1–3 de la sección 3:**
- **Mapa de eventos** (event storming) para el ciclo de vida de `Discrepancia`
  y de aceptación de versiones — muy útil, pero depende de tener resuelto qué
  es un "cambio relevante".
- **Modelo conceptual actualizado** (`CONCEPTUAL_MODEL.md` sigue fuera del
  alcance editable actual) — actualizar solo cuando haya algo estable que
  trasladar.

**Prematuro todavía:**
- **Casos de uso** — implican un flujo de aplicación; el modelo conceptual no
  está cerrado.
- **ADR técnicos** — reservar para cuando el equipo cierre una decisión
  concreta con consecuencias de arquitectura, como "tipo vivo vs. plantilla"
  (punto 3.3). Un ADR sobre algo todavía `DRAFT` sería prematuro.

## 6. Agenda propuesta para la próxima sesión

`[RECOMENDACIÓN]`, con tiempos orientativos para 2 horas:

1. (10 min) Repaso rápido: confirmar que `ENUNCIADO.md` de esta iteración
   refleja fielmente la sesión anterior.
2. (30 min) Cerrar persistencia/cálculo de `EstadoDeDiseño`, usando los
   contraejemplos de la sección 4.
3. (30 min) Formalizar `Discrepancia`: ciclo de vida, autoridad, criterio de
   "no repetir notificación".
4. (25 min) Los 5 significados de tipo + reconciliar con la duda de `HEB 300`
   ya abierta en `iteration-02`.
5. (15 min) Validar el criterio de "posesión del dato" de `iteration-03`
   contra el caso real de piping que traiga Miguel.
6. (10 min) Cierre: qué queda para `iteration-05`, quién se lleva cada deber.

## 7. Entidades, value objects, agregados y eventos de dominio candidatos

`[HIPÓTESIS]` — pensado para ayudar a la discusión, no para empezar a
implementar. `AGENTS.md` pide mantener separada la conceptualización del
dominio de las decisiones de clases o esquema mientras no sean necesarias;
esta sección es exploratoria y no cambia esa fase.

**Entidades candidatas (con identidad propia):**

- `OcurrenciaDeDiseño` `[ACUERDO]` — ya definida.
- `Representación` `[HIPÓTESIS]` — ligada a una ocurrencia, con su propia
  versión, propósito y estado de validación (punto 2 de la sesión).
- `Discrepancia` `[HIPÓTESIS]` — con ciclo de vida propio: detectada →
  presentada → decidida (aceptada / rechazada / ignorada / pospuesta).
- `DecisionDeAceptacion` `[ACUERDO]` — ya nombrada en `DESIGN_OCCURRENCE.md`.
- `DefinicionDeTipo` `[ACUERDO parcial]` — ya tratada; esta sesión añade la
  pregunta de si necesita dos variantes (viva / plantilla), sección 9.
- `Catalogo` `[HIPÓTESIS]` — nuevo candidato de esta sesión, contenedor de
  definiciones de tipo, con ámbito por decidir.
- `ModeloAnalitico` / `ObjetoAnalitico` `[ACUERDO]` — ya tratados.
- **`EstadoDeDiseño` — estatus incierto a propósito:** si termina siendo una
  vista puramente derivada (sin persistencia propia), probablemente **no** es
  una Entidad sino una proyección/consulta; si se materializa como snapshot
  validado, sí lo sería. Esta es exactamente la decisión pendiente 3.1 de la
  sección 3 — no se prejuzga aquí.

**Value objects candidatos (sin identidad propia):**

- `Geometria` `[HIPÓTESIS]` — consecuencia directa del punto 11 (desacoplar
  geometría de identidad).
- `SistemaDeCoordenadas` / `Transformacion` `[ACUERDO]` — ya mencionados en
  `ENTITY_SUMMARY.md` §3.
- `Version` `[ALTERNATIVA]` — podría ser Value Object simple (número + fecha)
  o necesitar identidad propia si debe aceptarse/rechazarse individualmente
  (la sesión del 23 de septiembre sugiere que sí necesita trazabilidad
  propia, lo que empuja hacia Entidad, no Value Object).

**Agregados candidatos:**

- `OcurrenciaDeDiseño` como raíz, con sus `Representación` dentro del límite
  — `[HIPÓTESIS]`.
- `Conjunto` / `Módulo` (`ST-01`, `PR-05`) como agregado propio con sus
  versiones — `[ACUERDO]`, ya establecido el 23 de septiembre.
- `Discrepancia` como agregado **independiente**, no anidado dentro de una
  ocurrencia — `[RECOMENDACIÓN]` — porque compara representaciones que pueden
  pertenecer a ocurrencias distintas o a un analítico frente a un físico;
  anidarla dentro de una sola ocurrencia forzaría una pertenencia que no
  tiene.

**Eventos de dominio candidatos:** `[HIPÓTESIS]`

`OcurrenciaCreada`, `RepresentacionActualizada`, `DiscrepanciaDetectada`,
`DiscrepanciaDecidida` (con motivo), `VersionAceptadaSinCambios`,
`TipoModificado` (relevante solo si existe tipo vivo — dispararía
notificación a las ocurrencias tipadas por él).

## 8. Bounded contexts candidatos y sus relaciones

`[HIPÓTESIS]`, en vocabulario ligero de DDD, sin comprometer arquitectura:

| Contexto candidato | Responsabilidad | Relación con el núcleo CDM |
|---|---|---|
| **Núcleo CDM** | `OcurrenciaDeDiseño`, `Discrepancia`, decisiones de aceptación | Es el contexto integrador |
| **Maqueta / coordinación** (SP3D u otra) | Representación física, geometría de coordinación | Anticorruption Layer — no importar su modelo interno tal cual (`AGENTS.md` ya lo prohíbe para IFC/CADMATIC/Tekla/Revit) |
| **Cálculo estructural** (STAAD/SAP2000) | Modelo analítico, resultados | Anticorruption Layer, igual que el anterior |
| **Piping** | Origen de geometría/necesidad de soporte | Upstream/Downstream — Piping no debería dictar el modelo interno de estructura (punto 8) |
| **Catálogos / tipos** | `DefinicionDeTipo`, ámbito corporativo o de proyecto | Open Host Service si es corporativo; Shared Kernel si es solo de proyecto — a decidir junto con la sección 3.4 |

## 9. Riesgos o contradicciones con decisiones anteriores

`[RIESGO]` señalado explícitamente en cada caso, no una acusación de error:

1. **Estado derivado vs. regla 5 de `RULES.md`.** La regla dice que *"un
   estado aceptado registra decisión, responsable, fecha, contexto y
   evidencia; no equivale al snapshot más reciente"*. Si `EstadoDeDiseño` pasa
   a ser una vista puramente calculada, **¿dónde vive esa decisión humana**
   que la regla exige? Si no se resuelve, se corre el riesgo de que la "vista
   derivada" termine comportándose exactamente como el snapshot más reciente
   que la regla 5 quiso evitar. Esta contradicción debe resolverse
   explícitamente, no diluirse.
2. **Tipo vivo vs. mecánica de tipado ya documentada.** `NOTAS_TIPO_ESTADO_DISENO.md`
   describía solo el patrón "plantilla + override" (declarar tipo, heredar
   valores, poder sobrescribir). El "tipo como referencia viva" de esta sesión
   es un mecanismo **distinto** que no estaba contemplado: si cambiar el tipo
   afecta a las ocurrencias ya aceptadas, reaparece el riesgo de "herencia
   silenciosa" que esa misma nota (punto 8) y `iteration-03` ya señalaron para
   otro caso. No es un error, es un mecanismo nuevo que necesita su propia
   regla de propagación antes de mezclarse con el ya existente.
3. **Integración pendiente con el versionado por conjuntos del 23 de
   septiembre.** Ese acuerdo dice que estructura y cimentación **se versionan
   como conjuntos completos, no pieza a pieza** (`RULES.md` regla 17). Pero
   esta sesión propone que `EstadoDeDiseño` sea una vista derivada "de las
   versiones relevantes de las representaciones asociadas a **una**
   ocurrencia". Si una columna no tiene versión propia (solo la tiene el
   conjunto), **¿de qué "versión relevante" se deriva el estado de esa
   columna en concreto?** Esta es una laguna real entre dos sesiones
   distintas que nadie ha conectado todavía — no es una contradicción
   irreconciliable, pero sí un hueco que debe cerrarse antes de cerrar el
   punto 3.1 de la sección 3.
4. **Alineación positiva (no un riesgo):** la supresión de notificaciones
   repetidas de `Discrepancia` (punto 5) coincide exactamente con el criterio
   ya propuesto en `iteration-03` ("¿de quién es este dato?" / distinguir
   nuevo estado de recálculo necesario). Es una confirmación cruzada, no una
   tensión.
5. **Entorno común y la separación de `AGENTS.md`.** El punto 6 empieza a
   describir una interfaz concreta (visualizar, comparar, decidir,
   trazabilidad). `AGENTS.md` pide mantener separada la conceptualización del
   dominio de las decisiones de tecnología/API mientras no sean necesarias.
   Recomendación: tratarlo por ahora solo como un bounded context conceptual
   (sección 8), sin diseñar su interfaz.

## 10. Posibles simplificaciones para un primer prototipo

`[ALTERNATIVA]` — ninguna de estas es una decisión, son caminos más simples
para validar el modelo sin cerrar prematuramente el diseño completo:

- Tratar `EstadoDeDiseño` como **snapshot explícito y persistido** en el
  prototipo (no derivado dinámicamente), dejando la vista calculada como
  evolución futura si el equipo la confirma.
- Implementar `DefinicionDeTipo` **solo como plantilla** en el prototipo,
  posponiendo "referencia viva" — evita el problema de propagación y
  notificación de tipos compartidos hasta que haya una regla clara.
- Un único ámbito de catálogo (p. ej. "proyecto") en el prototipo, aunque el
  modelo conceptual contemple varios ámbitos a futuro.
- `Discrepancia` con solo 2 desenlaces (aceptar / posponer) en el prototipo,
  en vez de las 4 variantes completas, para validar el flujo antes de cubrir
  todos los casos.
- Elementos secundarios: tratarlos en el prototipo como "representación sin
  ocurrencia propia" salvo que un caso concreto (aplicando la prueba ya
  existente de `DESIGN_OCCURRENCE.md`) demuestre que necesitan identidad —
  no crear una categoría especial "elemento secundario" de entrada.

## 11. Correspondencias preliminares con IFC

`[HIPÓTESIS]`, reutilizando el análisis ya hecho en `research/IFC_CORE_CONCEPTS.md`
e `iteration-02/ENUNCIADO.md` donde aplica, sin repetirlo:

| Concepto propio | Correspondencia IFC | Nota |
|---|---|---|
| `OcurrenciaDeDiseño` | Ninguna directa (deliberadamente más estrecho que `IfcObject`/`IfcProduct`) | Ya analizado en `iteration-02/ENUNCIADO.md` §3.1–3.2; no repetir aquí |
| `Representación` (múltiples, por herramienta) | Parcialmente `IfcShapeRepresentation`, pero IFC no versiona representaciones por aplicación con estado de validación propio | **No forzar**: es una extensión propia del dominio |
| `EstadoDeDiseño` (si es vista derivada) | Sin equivalente en IFC | **No forzar**: IFC no tiene un concepto de vista agregada multi-representación con aceptación humana |
| `Discrepancia` | Sin equivalente en IFC | **No forzar**: es un concepto de flujo de decisión propio del dominio |
| `DefinicionDeTipo` (variante "referencia viva") | Se parece a `IfcTypeObject` + `IfcRelDefinesByType`, que también son vivos por defecto | Buena correspondencia, reutilizable como referencia |
| `DefinicionDeTipo` (variante "plantilla") | Sin equivalente limpio en IFC | **No forzar**: extensión propia, IFC asume tipado vivo |
| `ModeloAnalitico` / `ObjetoAnalitico` | `IfcStructuralAnalysisModel` / `IfcStructuralItem` | Ya documentado, ver `IFC_CORE_CONCEPTS.md` §12 |
| Elementos secundarios (barandillas, gratings) | `IfcElement` ordinario (p. ej. `IfcRailing`) | Sin divergencia real; la pregunta de identidad es propia del dominio, no de IFC |
| Catálogos con ámbito corporativo | Sin equivalente en el núcleo IFC | Corresponde más al territorio de bSDD/Uniclass, ya reservado como "Frente 4" en `BIM_REFERENCE_MAP.md` — no mezclar con el núcleo IFC |
| "Entorno común" (interfaz CDM) | No es un concepto IFC en absoluto | Es una decisión de arquitectura propia, fuera de cualquier correspondencia con el estándar |

## 12. Preguntas críticas que el equipo todavía no se está haciendo

`[PENDIENTE]` — preguntas nuevas, no repetidas de la lista de "Preguntas
abiertas" del `ENUNCIADO.md`:

1. Si `EstadoDeDiseño` es una vista derivada, **¿quién es responsable cuando
   esa vista combina una representación desactualizada con otra vigente**, y
   produce una lectura incorrecta? ¿Existe una versión "congelada" para
   auditoría, o siempre se recalcula al vuelo?
2. **¿Qué pasa con una `Discrepancia` no resuelta cuando la ocurrencia
   implicada se da de baja?** ¿Se cierra automáticamente, se archiva o queda
   huérfana?
3. Si el tipo puede ser "referencia viva", **¿invalida silenciamente una
   aceptación ya validada** cuando el tipo cambia después? (Ver riesgo 2 de
   la sección 9.)
4. **¿Quién decide el ámbito de un catálogo cuando dos proyectos quieren
   compartirlo pero uno necesita una variante local?** — conflicto latente
   entre referencia viva corporativa y autonomía de proyecto.
5. **¿Las discrepancias entre disciplinas** (piping vs. estructura) **tienen
   la misma autoridad de decisión que las discrepancias dentro de una misma
   disciplina** (dos revisiones de STAAD)? El texto de la sesión no distingue,
   pero probablemente no debería ser la misma persona en ambos casos.
6. **¿Es una `Discrepancia` real, o una divergencia aceptable por diseño**,
   cuando dos representaciones de la misma ocurrencia son ambas "válidas" para
   propósitos distintos pero geométricamente incompatibles (la maqueta de
   coordinación sitúa una viga en una posición y el analítico en otra, cada
   una correcta para su propósito)?
7. **La pregunta de integración más urgente:** si el versionado es de
   conjuntos completos (23 de septiembre) pero el estado derivado se propone
   por ocurrencia individual (esta sesión), **¿cómo se calcula el estado de
   una pieza concreta dentro de un conjunto que no tiene su propio contador de
   versión?** Ver riesgo 3 de la sección 9 — esta pregunta conecta dos
   sesiones que todavía no se han hablado entre sí y debería plantearse
   explícitamente en la próxima reunión, no darse por implícitamente resuelta.
