# Registro de trabajo

> **Status:** CANONICAL  
> **Editable:** sí; añadir entradas al cerrar bloques materiales  
> **Document owner:** coordinación del dominio civil  
> **Canonical for:** historial resumido del trabajo realizado  
> **Sources:** historial Git y documentos enlazados por cada entrada  
> **Supersedes:** —  
> **Last reviewed:** 2026-10-01

## Regla de registro

Cada entrada debe resumir el objetivo, el resultado observable, los documentos
afectados, las cuestiones que permanecen abiertas, los commits y la siguiente
acción. No debe copiar aquí el razonamiento que pertenece al documento conceptual.

## Entradas

### 2026-10-01 — Consolidación de iteration-04 y apertura guiada de iteration-05

**Objetivo:** incorporar las notas de estudio de Ángel sobre representaciones,
estados y conciliación multi-modelo; analizar el informe posterior que propone
`Engineering System` como contexto superior a la ocurrencia; coordinar las fuentes
conceptuales y dejar preparada una siguiente iteración comprensible para el equipo.

**Resultado:** se incorpora
[`ANGEL_ITERATION_04.md`](iteration-04/ANGEL_ITERATION_04.md) como evidencia personal
`DRAFT`. Se abre [`iteration-05/`](iteration-05/ENUNCIADO.md) con la hipótesis de
`SistemaDeIngeniería`, sus cautelas y un ejercicio guiado: traducción del vocabulario
a preguntas ordinarias, ejemplo rellenado de `PR-05`, lista inicial de candidatos y
contraejemplos, plantilla copiable y cinco deberes concretos por participante. Se
crea [`ENGINEERING_SYSTEM.md`](domain-objects/ENGINEERING_SYSTEM.md) como fuente
propietaria `DRAFT`; el concepto se trata como contexto candidato, no como agregado
raíz ni como propietario exclusivo de modelos u ocurrencias. Se coordinan ocurrencia,
vocabulario, relaciones, reglas, resumen de entidades y conjunto de trabajo.

**Documentos afectados:** `docs/iteration-04/ANGEL_ITERATION_04.md`,
`docs/iteration-05/ENUNCIADO.md`, `docs/domain-objects/ENGINEERING_SYSTEM.md`,
`docs/domain-objects/DESIGN_OCCURRENCE.md`, `docs/VOCABULARY.md`,
`docs/RELATIONSHIPS.md`, `docs/RULES.md`, `docs/ENTITY_SUMMARY.md`,
`docs/WORKING_SET.md` y este registro.

**Cuestiones abiertas:** si `SistemaDeIngeniería` tiene identidad y responsabilidades
propias frente a conjunto físico, sistema funcional y contexto espacial; si modelos
y ocurrencias pueden asociarse a varios sistemas; cómo representar cobertura parcial
y fronteras compartidas; qué candidatos reconoce realmente el equipo; y qué alcance
tiene una conciliación transversal. Todo el contenido conceptual permanece `DRAFT`.

**Validación:** revisión del diff, cabeceras documentales, enlaces Markdown locales
y `git diff --check`. No se modifican inventario, modelo conceptual de consulta ni
documentos `CANONICAL` salvo los registros operativos autorizados.

**Commit:** commit de la rama `docs/angel-iteration-04-study` que contiene esta
entrada, publicada en `origin` para abrir un PR contra `develop`.

**Siguiente acción:** cada participante propone entre tres y cinco sistemas de
ingeniería reales, rellena una ficha para uno, aporta un contraejemplo, identifica
dos modelos o entregas y describe una decisión que solo tenga sentido sobre el
conjunto. La sesión unificará la lista y probará un caso de conciliación real antes
de ajustar el modelo conceptual.

### 2026-09-24 — Apertura de iteration-04: ocurrencia, representaciones y discrepancias

**Objetivo:** capturar una nueva sesión de trabajo aportada por Miguel
(ocurrencia, representaciones múltiples, reformulación de `EstadoDeDiseño`
como posible vista derivada, discrepancias, entorno común, elementos
secundarios, transferencia entre disciplinas, cinco significados de "tipo" y
catálogos) y encargar al agente un análisis explícito de próximos pasos,
riesgos y correspondencias con el resto del proyecto.

**Resultado:** se abre `iteration-04/` con dos artefactos:
[`ENUNCIADO.md`](iteration-04/ENUNCIADO.md), evidencia fiel de la sesión, y
[`ANALISIS_AGENTE.md`](iteration-04/ANALISIS_AGENTE.md), análisis derivado que
etiqueta cada afirmación como acuerdo, hipótesis, alternativa, recomendación o
decisión pendiente. El análisis prioriza cerrar la reformulación de
`EstadoDeDiseño`, formalizar `Discrepancia`, reconciliar los significados de
tipo con la duda de `HEB 300` ya abierta en `iteration-02`, y señala una
laguna real todavía sin conectar: el versionado por conjuntos completos del
23 de septiembre frente al estado derivado por ocurrencia individual de esta
sesión. `iteration-02` sigue siendo el frente activo formal; `iteration-03`
también sigue abierta.

**Documentos afectados:** `docs/iteration-04/ENUNCIADO.md` (nuevo),
`docs/iteration-04/ANALISIS_AGENTE.md` (nuevo), `docs/WORKING_SET.md`.

**Cuestiones abiertas:** las doce del encargo original (definición formal de
Ocurrencia/Representación/Estado, persistencia del estado, ciclo de vida de
Discrepancia, source of truth por atributo, nivel de catálogos, gestión de
cambios en tipos compartidos, criterios de agrupación documental, identidad
entre aplicaciones, reglas de propagación, elementos ausentes, separación
clase/forma/sección/rol, geometría extensible y correspondencia IFC), más las
preguntas críticas añadidas por el análisis (responsabilidad ante una vista
derivada incorrecta, destino de discrepancias sobre ocurrencias dadas de
baja, invalidación silenciosa por tipo vivo, autoridad de catálogo
compartido, autoridad de discrepancias entre disciplinas, y la integración
pendiente entre versionado por conjuntos y estado por ocurrencia).

**Commit:** commit de la rama `develop` que contiene esta entrada.

**Siguiente acción:** llevar `ANALISIS_AGENTE.md` a la próxima sesión conjunta
y usar su agenda propuesta (sección 6) como punto de partida, en paralelo a
los pendientes ya abiertos de `iteration-02` e `iteration-03`.

### 2026-09-24 — Apertura de iteration-03: revisión vs. recálculo

**Objetivo:** capturar una duda operativa real de Miguel —cuándo una edición en
STAAD/SAP2000 o en la maqueta 3D constituye un nuevo `EstadoDeDiseño` frente a
cuándo exige recálculo— separada deliberadamente de las notas de `iteration-02`
para no mezclar dos bloques de investigación distintos.

**Resultado:** se abre `iteration-03/` con
[`NOTAS_REVISION_VS_RECALCULO.md`](iteration-03/NOTAS_REVISION_VS_RECALCULO.md)
como primer artefacto: distingue snapshot de estado aceptado (regla 5 de
`RULES.md`), propone un criterio práctico ("¿de quién es este dato?"), resuelve
los tres casos concretos aportados (elementos auxiliares en la maqueta, bandejas
de piping sin recalcular, arriostramientos que cambian de posición) y separa
"nuevo estado" (barato) de "requiere recálculo" (decisión explícita de quien
tiene autoridad). Incluye una pregunta abierta sobre autoridad delegada para
aceptar sin recálculo, con ejemplo de bandejas dentro de un margen de diseño ya
previsto. `iteration-02` sigue siendo el frente activo; abrir esta carpeta no la
cierra ni la sustituye. Se integró sin pérdida el commit concurrente de Luis del
23 de septiembre (`ENTITY_SUMMARY.md` y ampliaciones relacionadas).

**Documentos afectados:** `docs/iteration-03/NOTAS_REVISION_VS_RECALCULO.md`
(nuevo), `docs/WORKING_SET.md`.

**Cuestiones abiertas:** quién tiene autoridad para aceptar un estado como "no
requiere recálculo" sin pasar por el ingeniero de cálculo en cada caso, qué
evidencia mínima debe registrarse en ese caso, y cómo vigilar el acumulado de
varias aceptaciones "dentro de margen" sucesivas.

**Commit:** commit de la rama `develop` que contiene esta entrada.

**Siguiente acción:** llevar la nota a discusión con el equipo, en paralelo a
`iteration-02`, y decidir si la pregunta de autoridad delegada requiere su
propia entidad (`DecisionDeAceptacion`) antes de cerrar el bloque.

### 2026-09-21 — Notas de Miguel para la sesión de iteration-02

**Objetivo:** preparar conceptos y preguntas de apoyo para la sesión de
`iteration-02`, centrados en dos hilos donde Miguel ya tenía evidencia previa:
tipo vs. estado de diseño, y correspondencia físico–analítica.

**Resultado:**

- se redactó [`NOTAS_TIPO_ESTADO_DISENO.md`](iteration-02/NOTAS_TIPO_ESTADO_DISENO.md):
  separación Ocurrencia/Estado/Tipo, mecánica de tipado (declaración del tipo,
  relación `está tipado por`, herencia con override, retipado vía nuevo
  estado), evidencia cruzada con la zapata de Luis, y una pregunta abierta con
  ejemplo para debatir (perfil `HEB 300`: ¿tipo intencional, clasificación, o
  ambos?);
- se redactó [`NOTAS_CORRESPONDENCIA_FISICO_ANALITICA.md`](iteration-02/NOTAS_CORRESPONDENCIA_FISICO_ANALITICA.md):
  las cuatro cardinalidades físico–analíticas (1:1, 1:N, N:1, N:M) con
  ejemplos del caso común, el matiz que las distingue de la correspondencia
  acción–analítico ya vista en la ficha de Miguel, y una pregunta abierta
  sobre vigencia de la correspondencia cuando cambia el estado físico;
- ambos documentos quedan enlazados entre sí y se incorporaron al alcance
  editable de `WORKING_SET.md`. Son apoyo personal, `iteration-02/ENUNCIADO.md`
  no exige ficha.

**Documentos afectados:** `docs/iteration-02/NOTAS_TIPO_ESTADO_DISENO.md`
(nuevo), `docs/iteration-02/NOTAS_CORRESPONDENCIA_FISICO_ANALITICA.md`
(nuevo), `docs/WORKING_SET.md`.

**Cuestiones abiertas:** las preguntas de debate recogidas en ambos
documentos (tipo vs. clasificación del perfil `HEB 300`; revisión propia del
tipo cuando cambia su definición; vigencia automática o re-evaluación
explícita de una correspondencia físico–analítica tras un cambio de estado).

**Commit:** commit de la rama `develop` que contiene esta entrada.

**Siguiente acción:** llevar ambos documentos a la sesión conjunta de
`iteration-02` y contrastar sus preguntas con el resto del equipo.

### 2026-09-18 — Organización documental y apertura de la segunda iteración

**Objetivo:** aplicar la organización documental aceptada por el equipo, formular
la primera frontera de `OcurrenciaDeDiseño` y convertir sus dudas en una investigación
estructurada antes de diseñar tablas o clases.

**Resultado:** se creó `domain-objects/` con un archivo propietario por objeto del
dominio y se inició con la definición `DRAFT` de `OcurrenciaDeDiseño`. Se separaron
el índice de vocabulario, la semántica de relaciones y las reglas candidatas. La
síntesis registra que el equipo acepta esta organización, sin convertir su contenido
en canónico. También se incorporó el material didáctico offline ya preparado.

Se abrió [`iteration-02/`](iteration-02/ENUNCIADO.md) con un artefacto concreto: una
memoria razonada de las conclusiones provisionales, un contraste detallado con
`IfcObject`, `IfcProduct`, tipos, assemblies, sistemas, estructura espacial,
relaciones y modelo analítico, y una agenda de cuestiones para revisar si la
definición de ocurrencia necesita ajustes. No se solicita una ficha como entrega.
La revisión de carpetas concluye que no se justifican todavía directorios adicionales
para relaciones, reglas, decisiones, fuentes o esquemas.

**Documentos afectados:** `README.md`, `docs/WORKING_SET.md`,
`docs/iteration-01/SINTESIS.md`, `docs/iteration-02/ENUNCIADO.md`,
`docs/domain-objects/DESIGN_OCCURRENCE.md`, `docs/VOCABULARY.md`,
`docs/RELATIONSHIPS.md`, `docs/RULES.md`, los tres documentos de `docs/study/` y
este registro.

**Validación:** revisión de cabeceras documentales, enlaces Markdown locales,
estructura de carpetas, estado Git y espacios con `git diff --check`. No se encontró
una herramienta local configurada para regenerar `README.pdf`; la copia derivada
queda pendiente y no se modificó.

**Cuestiones abiertas:** decidir si `ST-01` posee identidad como conjunto físico,
qué partes requieren lifecycle propio, qué cambios conservan identidad y qué
autoridad decide estados, sustituciones, divisiones, fusiones y bajas. Sigue
pendiente contrastar las ampliaciones de Luis sobre resultados y summaries.

**Commit:** commit de `develop` que contiene esta entrada; publicación autorizada
por el equipo mediante «actualiza y sube los cambios».

**Siguiente acción:** revisar en sesión las diferencias deliberadas y accidentales
respecto de IFC; utilizar `ST-01` y los contraejemplos solo cuando ayuden a corregir
o sostener la definición `DRAFT` de `OcurrenciaDeDiseño`.

### 2026-09-16 — Acciones, esfuerzos y consultas de envolventes con Luis

**Objetivo:** recoger las entrevistas del 15 y 16 de septiembre y cerrar el bloque
documental para publicación en `develop`, a petición de Luis.

**Resultado:** ampliada la ficha de Luis con la distinción de acciones, reacciones,
hipótesis, combinaciones, matriz y envolventes; reglas de summaries; esfuerzos,
EsfuerzosPlaca, desplazamientos y representaciones analíticas alternativas de zapata.
La síntesis enlaza las aportaciones y registra la propuesta de catálogos para
discusión del equipo. Las aportaciones siguen `DRAFT`.

**Documentos afectados:** `iteration-01/FICHA_LUIS_ZAPATA.md`,
`iteration-01/SINTESIS.md`, `WORKING_SET.md` y este registro.

**Validación:** revisión del diff, coherencia de componentes y número de entradas,
enlaces locales y comprobación de espacios con `git diff --check`.

**Cuestiones abiertas:** summaries de desplazamientos y tensiones/presiones,
eventual advanced de EsfuerzosPlaca, contraste del equipo y organización documental.
Se mantienen las preguntas previas de identidad de acción e intercambio de unidades.

**Commit:** commit de `develop` que contiene esta entrada.

**Siguiente acción:** Luis consulta al equipo la organización propuesta; continuar
las preguntas pendientes sin promover documentos ni crear catálogos todavía.

### 2026-09-14 — Consolidación documental de la primera iteración

**Objetivo:** reunir las aportaciones disponibles y facilitar su contraste en
`develop` sin convertir hipótesis de trabajo en decisiones canónicas.

**Resultado:** se agrupó el enunciado y las fichas de Ángel, Luis y Miguel en
[`iteration-01/`](iteration-01/ENUNCIADO.md) con nombres homogéneos; se incorporó
la [síntesis transversal](iteration-01/SINTESIS.md) como `DRAFT`, con vocabulario
provisional y ejemplos de identidad, procedencia y conciliación entre modelos.
Se actualizaron los accesos desde el README y el working set. Se comprobó que
`origin/develop` no aportaba cambios nuevos y se retiró el paquete local
`offline/`, ya innecesario; no formaba parte de Git.

**Documentos afectados:** `README.md`, `docs/WORKING_SET.md`, este registro y los
documentos de `docs/iteration-01/` (incluidos los trasladados desde `docs/`).

**Cuestiones abiertas:** revisar la síntesis con el equipo, completar la ficha de
Alberto, corregir la de Luis y contrastar las hipótesis de correspondencia con
un intercambio real entre programas. Ninguna propuesta se promueve a `CANONICAL`.

**Validación:** revisión del diff, enlaces locales y ausencia de errores de
espaciado antes de publicar.

**Commit:** commit de `develop` que contiene esta entrada.

**Siguiente acción:** discusión conjunta del vocabulario mínimo y selección de
un caso de intercambio físico–analítico para probarlo.

### 2026-09-14 — Ficha individual de Luis (Zapata)

**Objetivo:** preparar la aportación de Luis a la primera iteración a partir de
las entrevistas del 11 y 14 de septiembre.

**Resultado:** se redactó la [ficha de zapata](iteration-01/FICHA_LUIS_ZAPATA.md), incluyendo identidad,
tipos, geometría, armado, emplazamiento, encepados y elementos profundos separados.
Se incorporaron métodos de análisis manuales, algorítmicos y de elementos finitos,
y una propuesta transversal de comprobaciones y validación técnica trazable.
La ficha permanece `DRAFT`; su publicación no aprueba el modelo de dominio.

**Documentos afectados:** `docs/FICHA_ZAPATA.md`, `docs/WORKING_SET.md` y este registro.

**Cuestiones abiertas:** las propuestas de clasificación, tipos, asignación
geotécnica y validación se contrastarán con el equipo; los detalles pendientes
permanecen en la ficha.

**Validación:** revisión del contenido, enlaces locales y diff sin errores de
espacios; alcance limitado a la ficha de Luis y documentos de coordinación.

**Commit:** commit de `develop` que contiene esta entrada, autorizado por Luis
mediante «súbelos».

**Siguiente acción:** revisar la ficha con Luis y compararla con las demás
aportaciones de la primera iteración.

### 2026-09-09 — Inicio del dominio e investigación BIM

**Objetivo:** preparar un repositorio compartible para conceptualizar gradualmente
el dominio civil y estructural de una planta industrial.

**Resultado:**

- se establecieron las reglas de trabajo, el working set y el crecimiento deliberado
  del repositorio;
- se creó un inventario preliminar de elementos organizado por ocho grupos de
  exploración;
- se abrió como primera tarea la investigación de referencias BIM, estructurales y
  de plantas industriales;
- se redactó el primer estudio didáctico sobre el núcleo conceptual de IFC;
- se preparó el README como introducción y lectura previa suficiente para el equipo.

**Documentos afectados:** `README.md`, `AGENTS.md` y el conjunto documental inicial
contenido en `docs/`.

**Cuestiones abiertas:** revisar con el equipo los conceptos IFC mediante ejemplos de
pipe rack, viga, equipo y zapata; acordar después el reparto de los siguientes
frentes de investigación.

**Commit:** commit inicial de la rama `develop` que contiene esta entrada.

**Siguiente acción:** realizar la primera sesión de contraste y decidir si IFC
necesita una segunda pasada antes de abrir el frente estructural analítico.

### 2026-09-10 — Preparación de la primera iteración del equipo

**Objetivo:** convertir el estudio inicial de IFC en un ejercicio comparable para
Alberto, Luis, Miguel y Ángel antes de la siguiente reunión.

**Resultado:**

- se definió un caso común desde equipo y estructura hasta cimentación y terreno;
- se creó una batería transversal de preguntas sobre realidad física, identidad,
  tipos, jerarquías, geometría, materiales, conexiones, acciones y modelos
  analíticos;
- se delimitaron focos provisionales para conexiones, zapata, cargas y
  correspondencia físico–analítica;
- se añadió un pedestal resuelto como guía del nivel de detalle esperado;
- se generaron copias PDF del README y del estudio de fundamentos IFC.

**Documentos afectados:** `README.md`, `README.pdf`, `docs/WORKING_SET.md`,
`docs/FIRST_ITERATION.md` y `docs/research/IFC_CORE_CONCEPTS.pdf`.

**Cuestiones abiertas:** contrastar las cuatro fichas, precisar el alcance de cada
frente y decidir qué conceptos requieren investigación adicional.

**Commit:** commit de la rama `develop` que contiene esta entrada.

**Siguiente acción:** preparar las fichas individuales y utilizarlas como entrada de
la próxima reunión, sin diseñar todavía tablas o clases definitivas.

### 2026-09-11 — Ficha individual de Miguel (Acciones y cargas)

**Objetivo:** construir, pregunta a pregunta, la ficha individual del foco
"Acciones y cargas" a partir del ejemplo de un depósito (`EQ-101`) apoyado
sobre la estructura soporte.

**Resultado:**

- se recorrió la batería común aplicada al ejemplo (bloques A, E y F, más
  la pregunta específica de sistema de coordenadas y convenio de signos);
- se fijó la separación entre objeto físico, Acción, agrupación (caso de
  carga) y aplicación analítica, evitando guardar la carga como propiedad
  de un elemento físico;
- se identificaron dos representaciones analíticas alternativas (nodo vs.
  barra) para la misma acción física;
- se registraron 5 conceptos candidatos, 3 dudas para la reunión y un
  ejemplo de simplificación válida frente a un diseño frágil;
- se creó `FICHA_ACCIONES_CARGAS.md` y se incorporó al alcance editable de
  `WORKING_SET.md`.

**Documentos afectados:** `docs/FICHA_ACCIONES_CARGAS.md` (nuevo),
`docs/WORKING_SET.md`.

**Cuestiones abiertas:** las 3 dudas recogidas en la ficha (cambio de TAG
ante revisiones de diseño, dónde vive el convenio de signos, cuándo
ampliar el alcance de un apoyo individual al reparto entre varios apoyos).

**Commit:** commit de la rama `develop` que contiene esta entrada.

**Siguiente acción:** contrastar esta ficha con las de Alberto, Luis y
Ángel en la próxima reunión, según `FIRST_ITERATION.md` sección 7.

### 2026-09-23 — Resumen de entidades y cierre de conjuntos y versiones

**Objetivo:** reunir entidades y propiedades documentadas y conservar la conversación
sobre modularización, identidad, versionado y dependencias de cargas.

**Resultado:** se incorpora `ENTITY_SUMMARY.md`, preparado el 22 de septiembre,
como resumen derivado. La sesión del 23 se registra en `iteration-02/ENUNCIADO.md`,
coordinada con ocurrencia, vocabulario, relaciones y reglas. Se distingue versión de
diseño de revisión documental; se recoge el versionado completo de conjuntos y la
necesidad de referencias y aceptaciones entre versiones de proveedores y receptores.
Todo el contenido conceptual permanece `DRAFT`. No se modifican fichas individuales,
inventario ni modelo conceptual de consulta.

**Documentos afectados:** `ENTITY_SUMMARY.md`, `iteration-02/ENUNCIADO.md`,
`domain-objects/DESIGN_OCCURRENCE.md`, `VOCABULARY.md`, `RELATIONSHIPS.md`, `RULES.md`,
`WORKING_SET.md` y este registro.

**Pendientes:** inclusión de cimentación en módulo (reservada al equipo), cimentación
compartida (sin respuesta), autoridad de continuidad, aceptación sin cambios y estado
de piezas dentro de versiones del conjunto.

**Validación:** revisión de diff y enlaces locales; sin cambios ejecutables.

**Commit:** commit de cierre de `develop` que contiene esta entrada.

**Siguiente acción:** contrastar los pendientes con el equipo antes de aprobar las
propuestas conceptuales.
