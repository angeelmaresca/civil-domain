# Relaciones del dominio civil

> **Status:** DRAFT
> **Editable:** sí; catálogo conceptual dentro de `WORKING_SET.md`
> **Document owner:** equipo de dominio civil
> **Canonical for:** —
> **Sources:** [síntesis de la primera iteración](iteration-01/SINTESIS.md), [ocurrencia de diseño](domain-objects/DESIGN_OCCURRENCE.md), fichas de la primera iteración y [estudio IFC](research/IFC_CORE_CONCEPTS.md)
> **Supersedes:** —
> **Last reviewed:** 2026-09-23

## Propósito

Este documento separa las relaciones del vocabulario de objetos. Una relación debe
expresar un verbo del dominio, sus participantes, cardinalidad, contexto, vigencia y
procedencia. No se implementará todo mediante `parentId` ni mediante listas sin
semántica.

Las relaciones siguientes son candidatas. Los nombres técnicos definitivos y su
representación en tablas, clases o grafos permanecen abiertos.

## Familias iniciales

| Relación candidata | Origen → destino | Significado | No significa |
|---|---|---|---|
| `tiene estado de diseño` | ocurrencia → estado | El estado define esa ocurrencia en un contexto/revisión aceptados. | Que el último dato importado esté aceptado. |
| `se compone físicamente de` | ocurrencia todo → ocurrencia parte | La parte contribuye al todo físico y existe dependencia de composición durante una vigencia. | Contención espacial o mera pertenencia funcional. |
| `es miembro de sistema` | objeto → sistema funcional | El objeto colabora en una función del sistema. | Que el sistema sea dueño del lifecycle del objeto. |
| `está contenido espacialmente en` | objeto → contexto espacial | Establece su contenedor espacial principal dentro de un alcance. | Que el espacio sea su todo físico. |
| `está referenciado espacialmente en` | objeto → contexto espacial | Declara otros espacios relevantes sin cambiar el contenedor principal. | Composición. |
| `se conecta con` | ocurrencia/interfaz → ocurrencia/interfaz | Describe una conexión física identificada y sus participantes. | Rigidez o comportamiento analítico por defecto. |
| `da apoyo a` | ocurrencia → ocurrencia | Expresa el papel físico/funcional de soporte. | Pertenencia o aplicación analítica de una reacción. |
| `transmite acciones a` | ocurrencia/interfaz → ocurrencia/interfaz | Expresa una ruta física prevista para acciones. | Un valor de carga o resultado calculado fijo. |
| `está tipado por` | estado u ocurrencia contextualizada → tipo | Declara intención común reutilizable dentro de un alcance. | Igualdad derivada de propiedades. |
| `está clasificado como` | objeto → referencia de clasificación | Sitúa el objeto en un vocabulario externo o acordado. | Crear su identidad o tipo intencional. |
| `está representado por` | estado → representación | Vincula un objeto con una forma o descripción para un propósito. | Identidad entre representación y objeto. |
| `está documentado por` | estado/afirmación → snapshot de fuente | Conserva evidencia y procedencia de una afirmación. | Que la fuente tenga autoridad universal. |
| `sustituye a` | ocurrencia nueva → ocurrencia anterior | Conserva trazabilidad cuando no hay continuidad de identidad. | Una nueva revisión de la misma ocurrencia. |

## Composición física

La composición responde «¿qué partes constituyen este todo físico durante este
estado?». Debe distinguirse de:

- sistema: membresía funcional potencialmente muchos-a-muchos;
- contención: localización principal;
- conexión: interfaz entre objetos que pueden conservar lifecycle independiente;
- apoyo: papel funcional o mecánico;
- agrupación de consulta: selección sin identidad propia.

Una parte no se duplica para aparecer en varios contextos. Si parece pertenecer a
dos todos físicos simultáneamente, se debe comprobar si uno de los vínculos es en
realidad sistema, conexión, apoyo o referencia espacial. No se fija aún como regla
un único todo físico universal: debe probarse con cimentaciones, módulos y conexiones.

## Correspondencia físico–analítica

`se corresponde con objeto analítico` relaciona un estado físico —o un snapshot
físico todavía no aceptado— con uno o varios objetos o zonas de un modelo analítico.
La relación debe poder conservar:

- propósito y modelo/revisión de análisis;
- cardinalidad `1:1`, `1:N`, `N:1` o `N:M`;
- evidencia y autor de la correspondencia;
- sistemas de referencia y transformaciones relevantes;
- vigencia o evaluación de alineación con el estado físico;
- rol de cada participante, sin declarar que ambos son el mismo objeto.

Una columna representada por dos barras y una zapata representada por varias placas
son casos normales, no excepciones del esquema.

## Relaciones que necesitan entidad propia

Una relación debe poder objetivarse cuando tiene datos o decisiones propios. Son
candidatas claras:

- conexiones con interfaces, geometría o condiciones;
- correspondencias físico–analíticas con evidencia y cardinalidad;
- asignaciones geotécnicas basadas en una regla;
- aplicaciones de acciones a un modelo;
- composición o membresía cuya vigencia cambia entre estados;
- conciliaciones de identidad entre snapshots de fuentes.

«Objetivar» no obliga todavía a crear una tabla por relación. Obliga a no perder su
semántica tratándola como una referencia desnuda.

## Matriz de prueba para `ST-01`

| Afirmación | Relación adecuada |
|---|---|
| `ST-01` es el conjunto físico formado por `C-101` y `B-101`. | `se compone físicamente de` |
| `C-101` participa en el sistema resistente principal. | `es miembro de sistema` |
| `C-101` se considera contenido en el módulo `M-01`. | `está contenido espacialmente en` |
| `C-101` apoya sobre `F-101`. | `da apoyo a` o una conexión más precisa; no composición automática |
| Dos barras de `AM-02` idealizan `C-101 @ R04`. | `se corresponde con objeto analítico` |
| `SP3D P12/C-44` aporta la forma de `C-101 @ R03`. | `está documentado por` y `está representado por` |

La prueba se considera fallida si todas las afirmaciones solo pueden expresarse con
`parent`, `contains` o `relatedTo`.

## Dependencias de cargas entre versiones

Fuente: [sesión del 23 de septiembre](iteration-02/ENUNCIADO.md#11-sesión-del-23-de-septiembre-conjuntos-y-versiones),
aportación `DRAFT`. La ruta física de transmisión no expresa por sí sola qué
versión suministró las cargas usadas por el receptor.

| Relación candidata | Participantes | Pendiente |
|---|---|---|
| Se basa en cargas de | Versión receptora y versión concreta proveedora. | Referencia precisa al paquete de cargas/análisis y multiplicidad de proveedores. |
| Se acepta sin modificación frente a | Versión receptora conservada y nueva versión proveedora evaluada. | Registro, autoridad y evidencia; distinguir base utilizada de compatibilidad aceptada posteriormente. |

PR-05 conserva composición con módulos e incluye cimentaciones según el caso
aportado; no se fija si cada módulo incluye su cimentación. Pertenecer a PR-05
no obliga a sincronizar versiones ni a crear ya una configuración global versionada.
