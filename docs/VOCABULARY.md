# Vocabulario del dominio civil

> **Status:** DRAFT
> **Editable:** sí; índice vivo de términos dentro de `WORKING_SET.md`
> **Document owner:** equipo de dominio civil
> **Canonical for:** —
> **Sources:** [síntesis de la primera iteración](iteration-01/SINTESIS.md) y documentos propietarios enlazados por cada término
> **Supersedes:** —
> **Last reviewed:** 2026-09-23

## Propósito

Este documento permite encontrar términos, sinónimos y ambigüedades. No duplica la
definición extensa: cada entrada enlaza a su fuente propietaria. Una palabra incluida
aquí no implica que el concepto ni su nombre estén aprobados.

| Término | Significado breve | Estado conceptual | Fuente propietaria |
|---|---|---|---|
| Ocurrencia de diseño | Individuo físico concreto que el proyecto pretende seguir entre estados de diseño. | Candidato | [`OcurrenciaDeDiseño`](domain-objects/DESIGN_OCCURRENCE.md#definición-candidata) |
| Estado de diseño | Definición de una ocurrencia aceptada para una revisión o contexto. | Candidato; falta documento propio | [Ocurrencia: identidad y estado](domain-objects/DESIGN_OCCURRENCE.md#identidad-y-estado) |
| Estructura | Término ambiguo: puede designar conjunto físico, sistema funcional, contenedor, modelo analítico o tipo. | Abierto; no usar sin calificador | [¿Una estructura es una ocurrencia?](domain-objects/DESIGN_OCCURRENCE.md#una-estructura-es-una-ocurrencia) |
| Tipo intencional | Definición común declarada para reutilizar una intención dentro de un alcance. | Candidato | [Síntesis v0.1](iteration-01/SINTESIS.md#vocabulario-mínimo-propuesto-para-contrastar-v01) |
| Agrupación derivada | Conjunto calculado por similitud de propiedades, sin declaración de tipo compartido. | Candidato | [Síntesis v0.1](iteration-01/SINTESIS.md#vocabulario-mínimo-propuesto-para-contrastar-v01) |
| Snapshot importado | Afirmación conservada de una fuente y revisión concretas. | Candidato | [Síntesis v0.1](iteration-01/SINTESIS.md#vocabulario-mínimo-propuesto-para-contrastar-v01) |
| Referencia externa | Identificador contextualizado por aplicación, modelo y revisión. | Candidato | [Síntesis v0.1](iteration-01/SINTESIS.md#vocabulario-mínimo-propuesto-para-contrastar-v01) |
| Representación física | Forma o descripción que representa un estado físico para un propósito. | Candidato | [Síntesis v0.1](iteration-01/SINTESIS.md#vocabulario-mínimo-propuesto-para-contrastar-v01) |
| Idealización analítica | Objeto o formulación creada para un análisis y propósito concretos. | Candidato | [Síntesis v0.1](iteration-01/SINTESIS.md#vocabulario-mínimo-propuesto-para-contrastar-v01) |
| Conciliación de identidad | Afirmación justificada de que dos objetos físicos de fuente representan la misma ocurrencia. | Candidato | [Síntesis v0.1](iteration-01/SINTESIS.md#vocabulario-mínimo-propuesto-para-contrastar-v01) |
| Correspondencia físico–analítica | Vínculo trazable entre un estado físico y una idealización analítica. | Candidato | [`RELATIONSHIPS.md`](RELATIONSHIPS.md#correspondencia-físicoanalítica) |

## Convención de uso

Hasta que el equipo cierre la ambigüedad de «estructura», usar expresiones precisas:
`estructura física`, `sistema estructural`, `contenedor espacial`, `modelo analítico`
o `tipo de estructura`.

## Precisiones de la sesión del 23 de septiembre

Aportación de Luis para contraste, sin aprobación canónica.

| Término | Significado breve | Fuente propietaria |
|---|---|---|
| Versión de diseño | Estado técnico del conjunto, distinto de emisión documental. | [Reglas](RULES.md#versiones-de-conjuntos-y-cargas--propuesta-para-contraste) |
| Revisión documental | Identificación de emisión al cliente asociada a estados como IFR o IFC. | [Reglas](RULES.md#versiones-de-conjuntos-y-cargas--propuesta-para-contraste) |
| Conjunto versionado | Estructura o cimentación conservada completa por versión, sin ciclo independiente por pieza. | [Ocurrencia](domain-objects/DESIGN_OCCURRENCE.md#contraste-de-conjuntos-y-versiones-completas) |
| Pipe rack como conjunto | PR-05 persiste al modularizar e incluye cimentaciones en el caso descrito. | [Ocurrencia](domain-objects/DESIGN_OCCURRENCE.md#contraste-de-conjuntos-y-versiones-completas) |
| Módulo | Parte del pipe rack con versiones independientes; inclusión de cimentación pendiente. | [Ocurrencia](domain-objects/DESIGN_OCCURRENCE.md#contraste-de-conjuntos-y-versiones-completas) |
| Unidad | Puede delimitar zona o proceso; no equivale siempre a contenedor espacial. | [Evidencia](iteration-02/ENUNCIADO.md#identidad-alcance-y-códigos) |
| Aceptación sin modificación | Compatibilidad reconocida frente a cambio del proveedor de cargas conservando versión receptora. | [Relaciones](RELATIONSHIPS.md#dependencias-de-cargas-entre-versiones) |

Las fichas anteriores emplean «revisión» según su contexto original; no se
reescriben retrospectivamente como si ya distinguieran estas acepciones.
