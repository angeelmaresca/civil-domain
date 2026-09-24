# Conjunto de trabajo

> **Status:** CANONICAL  
> **Editable:** sí; actualizar al iniciar o terminar un bloque de trabajo  
> **Document owner:** coordinación del dominio civil  
> **Canonical for:** estado operativo, alcance de edición y siguiente acción  
> **Sources:** conversación inicial del equipo  
> **Supersedes:** —  
> **Last reviewed:** 2026-09-24 (actualizado de nuevo el mismo día con la apertura de `iteration-04/`)

## Empieza aquí

Este documento es la única puerta de entrada operativa. Antes de editar, leer las
instrucciones de [`../AGENTS.md`](../AGENTS.md).

## Hito actual

Segunda iteración: someter la definición `DRAFT` de `OcurrenciaDeDiseño` a casos de
frontera para decidir qué individuos físicos necesitan identidad en el CDM y separar
una estructura física de un sistema funcional, un contenedor espacial, un tipo y un
modelo analítico.

## Documentos activos

[`iteration-02/ENUNCIADO.md`](iteration-02/ENUNCIADO.md) conserva la reflexión de
partida, el contraste explícito con IFC y los puntos que pueden investigarse en la
próxima sesión; no exige preparar ni devolver una ficha.
[`domain-objects/DESIGN_OCCURRENCE.md`](domain-objects/DESIGN_OCCURRENCE.md) es la
fuente propietaria `DRAFT` que esta iteración debe intentar refutar o ajustar.

[`iteration-01/`](iteration-01/ENUNCIADO.md) conserva el enunciado, las tres fichas
y la síntesis que aportan la evidencia inicial. Continúan en estado `DRAFT`, pero
ya no coordinan el frente activo.

## Alcance de edición actual

| Documento | Uso permitido |
|---|---|
| `iteration-02/ENUNCIADO.md` | Memoria razonada, comparación con IFC y agenda opcional de la segunda iteración |
| `iteration-02/NOTAS_TIPO_ESTADO_DISENO.md` | Notas personales de Miguel (tipo vs. estado de diseño); apoyo para la sesión, no ficha exigida |
| `iteration-02/NOTAS_CORRESPONDENCIA_FISICO_ANALITICA.md` | Notas personales de Miguel (correspondencia físico–analítica); apoyo para la sesión, no ficha exigida |
| `iteration-03/NOTAS_REVISION_VS_RECALCULO.md` | Nota personal de Miguel sobre cuándo cambia un `EstadoDeDiseño` frente a cuándo exige recálculo; primer artefacto de `iteration-03/` |
| `iteration-04/ENUNCIADO.md` | Evidencia de la sesión sobre ocurrencia, representaciones, estado derivado y discrepancias; primer artefacto de `iteration-04/` |
| `iteration-04/ANALISIS_AGENTE.md` | Análisis derivado del agente sobre esa sesión; distingue acuerdos, hipótesis, alternativas, recomendaciones y decisiones pendientes |
| `iteration-01/` | Evidencia de consulta; las fichas individuales solo se corrigen con sus autores |
| `iteration-01/SINTESIS.md` | Trazabilidad de la primera iteración y organización documental acordada |
| `VOCABULARY.md` | Índice breve de términos acordados o candidatos; enlaza a su fuente propietaria |
| `ENTITY_SUMMARY.md` | Resumen derivado solicitado de entidades y conceptos candidatos, descripciones, propiedades mencionadas y pendientes; no sustituye sus fuentes propietarias |
| `domain-objects/DESIGN_OCCURRENCE.md` | Primera definición conceptual `DRAFT` de una ocurrencia de diseño y de su frontera |
| `RELATIONSHIPS.md` | Vocabulario y semántica `DRAFT` de relaciones entre objetos; separado del vocabulario general |
| `RULES.md` | Reglas e invariantes conceptuales candidatos; no constituye todavía un esquema ejecutable |
| `research/IFC_CORE_CONCEPTS.md` | Referencia didáctica; editar solo si la aplicación de los ejemplos descubre una corrección |
| `BIM_REFERENCE_MAP.md` | Actualización coordinada únicamente si cambia el frente de investigación |
| `WORKING_SET.md` | Mantener el estado presente y la siguiente acción |
| `WORK_LOG.md` | Registrar el bloque únicamente cuando se cierre |
| `../README.md` | Ajustar la presentación si cambia el propósito del repositorio |
| `../README.pdf` | Copia generada del README para consulta; no es fuente editable |
| `research/IFC_CORE_CONCEPTS.pdf` | Copia generada del estudio IFC; regenerar cuando cambie el Markdown |
| `study/STUDY_GUIDE.md` | Guía didáctica derivada para estudio offline; no define el dominio |
| `study/STUDY_WORKBOOK.md` | Ejercicios individuales sobre las distinciones de la primera iteración |
| `study/STUDY_ANSWERS.md` | Respuestas razonadas con enlaces a las fuentes propietarias |
| `../AGENTS.md` | Ajustar reglas de trabajo cuando el equipo lo acuerde |

[`ELEMENT_INVENTORY.md`](ELEMENT_INVENTORY.md) y
[`CONCEPTUAL_MODEL.md`](CONCEPTUAL_MODEL.md) se conservan como documentos de consulta,
pero no son frentes editables durante este hito. La investigación debe terminar con
recomendaciones explícitas antes de trasladar conceptos al inventario.

La carpeta `study/` reúne tres artefactos didácticos concretos para consulta offline.
Resume y ejercita el material vigente, pero no abre una iteración, no sustituye a las
fuentes y no convierte convergencias `DRAFT` en consenso del equipo.

La carpeta `domain-objects/` se incorpora tras la aceptación del equipo de la
propuesta de organización documental. Aloja un archivo por objeto del dominio y
se crea ahora porque existe un primer artefacto concreto: la definición `DRAFT` de
`OcurrenciaDeDiseño`. Evita concentrar objetos distintos en un único documento y
no presupone qué otros objetos acabarán formando parte del CDM.

La carpeta `iteration-02/` se crea porque ya existe un bloque de investigación
concreto: probar y ajustar la frontera de `OcurrenciaDeDiseño`. Su primer artefacto
es el enunciado de la iteración. No se crean todavía carpetas independientes para
relaciones, reglas, decisiones, fuentes o esquemas: el volumen actual no las
justifica y `schemas/` sería prematuro antes de cerrar el modelo conceptual.

La carpeta `iteration-03/` se abre por decisión explícita de Miguel, antes de
que `iteration-02` haya cerrado con su sesión de contraste. El artefacto
concreto que la justifica es un caso operativo real —cuándo una edición en
STAAD/SAP2000 o en la maqueta 3D constituye un nuevo `EstadoDeDiseño` frente
a cuándo exige recálculo— que se mantiene deliberadamente separado de las
notas de `iteration-02` para no mezclar dos bloques de investigación
distintos. `iteration-02` sigue siendo el frente activo del equipo; abrir
esta carpeta no la cierra ni la sustituye.

La carpeta `iteration-04/` se abre por decisión explícita de Miguel para
recoger una nueva sesión de trabajo (ocurrencia, representaciones, estado de
diseño reformulado como posible vista derivada, discrepancias, entorno común,
elementos secundarios, transferencia entre disciplinas, significados de
"tipo" y catálogos) junto con el análisis solicitado al agente. Ninguna de las
carpetas de iteración anteriores queda cerrada por esto: `iteration-02` sigue
siendo el frente activo formal del equipo, e `iteration-03` sigue abierta.

## Siguiente acción

Bloque del 23 de septiembre cerrado: [evidencia de la conversación](iteration-02/ENUNCIADO.md#11-sesión-del-23-de-septiembre-conjuntos-y-versiones).
Se coordinan resumen de entidades, ocurrencia, vocabulario, relaciones y reglas;
el contenido conceptual continúa en `DRAFT`.

Prioridad: debatir con el equipo si el módulo incluye cimentación, aplazado
expresamente. Sigue sin respuesta el caso de cimentación compartida. Después,
precisar aceptación sin cambios entre versiones y estados de piezas en conjuntos.

Revisar conjuntamente la reflexión de
[`iteration-02/ENUNCIADO.md`](iteration-02/ENUNCIADO.md), en especial las diferencias
entre `IfcObject`, `IfcProduct`, assembly físico, sistema, estructura espacial y
modelo analítico. Acordar qué divergencias del CDM son deliberadas y cuáles revelan
un concepto ausente o una frontera mal definida.

Como apoyo a la conversación, aplicar cuando resulte útil los contraejemplos de
sustitución, división, fusión, traslado y agrupación temporal a `ST-01`, `C-101`,
`B-101`, `F-101` y `EQ-101`. No se solicita una ficha. Cualquier ajuste se trasladará
a [`OcurrenciaDeDiseño`](domain-objects/DESIGN_OCCURRENCE.md),
[`RELATIONSHIPS.md`](RELATIONSHIPS.md), [`RULES.md`](RULES.md) o
[`VOCABULARY.md`](VOCABULARY.md), manteniendo el contenido en `DRAFT` hasta el
contraste humano.

## Decisiones operativas vigentes

La organización documental propuesta por Luis queda aceptada con el matiz acordado
el 18 de septiembre: los objetos del dominio viven en `domain-objects/`, uno por
archivo; [`RELATIONSHIPS.md`](RELATIONSHIPS.md) permanece separado de
[`VOCABULARY.md`](VOCABULARY.md). La estructura se amplía solo al aparecer contenido
real y no convierte los conceptos `DRAFT` en definiciones canónicas.

No se diseñarán todavía tablas, clases, un esquema ejecutable o una jerarquía
canónica. La segunda iteración debe estabilizar primero identidad, estados y
relaciones mediante ejemplos y contraejemplos.

## Pendientes heredados de la primera iteración

Sigue pendiente contrastar la [ampliación de Luis sobre esfuerzos y modelos
analíticos](iteration-01/FICHA_LUIS_ZAPATA.md#11-esfuerzos-desplazamientos-y-representaciones-analíticas).
Faltan las reglas concretas de summaries de desplazamientos y tensiones/presiones;
el summary de EsfuerzosPlaca está descrito como propuesta confirmada por Luis.

Contrastar con el equipo la [aclaración de Luis sobre acciones y escenarios](iteration-01/FICHA_LUIS_ZAPATA.md#10-aclaración-de-luis-acciones-escenarios-y-summaries),
incorporada en su ficha tras la entrevista del 15 de septiembre. Incluye envolventes
y summaries. Es una aportación `DRAFT` y no sustituye la ficha de Miguel.

Luis revisa y corrige su [ficha de zapata](iteration-01/FICHA_LUIS_ZAPATA.md), redactada a partir de
las entrevistas del 11 y 14 de septiembre, incluida la ampliación sobre encepados,
métodos de análisis y validación técnica. Sus propuestas siguen en estado `DRAFT`.

La ficha de Alberto sobre conexiones todavía no está incorporada; la síntesis de
la primera iteración no se presenta como consenso de los cuatro frentes.

La copia derivada `../README.pdf` queda pendiente de regeneración: no se ha encontrado
en el repositorio ni en el entorno una herramienta local configurada para hacerlo.
`README.md` continúa siendo la fuente editable y su publicación no queda bloqueada
por esta limitación conocida.
