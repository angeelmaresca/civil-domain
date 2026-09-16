# Síntesis transversal — primera iteración

> **Status:** DRAFT
> **Editable:** sí; documento de contraste previo a la reunión
> **Document owner:** equipo de dominio civil
> **Canonical for:** —
> **Sources:** [enunciado](ENUNCIADO.md), fichas de [Ángel](FICHA_ANGEL_COLUMNA.md), [Luis](FICHA_LUIS_ZAPATA.md) y [Miguel](FICHA_MIGUEL_ACCIONES_CARGAS.md)
> **Supersedes:** —
> **Last reviewed:** 2026-09-16

## Alcance de la fusión

Hay **tres fichas disponibles**: columna física y analítica, zapata/encepado, y
acciones del equipo. La ficha de Alberto sobre conexiones todavía no está aquí y
la de Luis sigue pendiente de corrección por su autor. Las tres aportaciones son
borradores individuales; «convergencia» significa que el mismo
problema aparece en varios ejemplos, **no** que el equipo haya aprobado una regla.
Los códigos `ST-01` y `ST-101` pertenecen a ejemplos ficticios distintos y no se
reconcilian como si fueran la misma estructura real.

Esta síntesis extrae distinciones y tensiones. No define tablas, clases, una
jerarquía de herencia ni una autoridad universal de datos.

## Lo que las fichas nos obligan a distinguir

La [aclaración de Luis del 15 de septiembre](FICHA_LUIS_ZAPATA.md#10-aclaración-de-luis-acciones-escenarios-y-summaries)
es la fuente de su aportación sobre acciones, reacciones, escenarios, matriz,
envolvente y summaries. Queda para contraste con Miguel y el equipo; no sustituye
las preguntas abiertas sobre identidad de acción y aplicaciones analíticas.

La [continuación del 16 de septiembre](FICHA_LUIS_ZAPATA.md#11-esfuerzos-desplazamientos-y-representaciones-analíticas)
recoge esfuerzos, EsfuerzosPlaca, desplazamientos y distintas idealizaciones de
zapata, con su relación con escenarios y envolventes. Incluye el summary de
EsfuerzosPlaca confirmado con Luis y señala qué summaries siguen pendientes.

### Propuesta de organización documental pendiente del equipo

En la conversación con Luis se explicó Civil Domain como vocabulario compartido
más objetos, relaciones, reglas y contexto/procedencia de los datos de ingeniería.
El glosario es una puerta de entrada al modelo conceptual, no su contenido completo.
Esto no define todavía tablas, clases ni una entidad por término.

Se propuso organizar progresivamente cuatro documentos:

| Parte propuesta | Contenido previsto |
|---|---|
| Vocabulario | Significados breves, sinónimos, ambigüedades y enlaces al detalle. |
| Objetos del dominio | Identidad, revisiones, límites y naturaleza de los objetos; distinguir candidatos de definiciones acordadas. |
| Relaciones | Significado de los vínculos entre objetos y su contexto. |
| Reglas del dominio | Condiciones que deben cumplirse, con ejemplos y fuentes. |

La propuesta conservaría una fuente propietaria por definición, enlaces entre
documentos y trazabilidad a las fichas de conversación. Se sugirieron identificadores
estables y una indicación de si cada entrada es propuesta, confirmada en entrevista
o pendiente de contraste; estas indicaciones de consenso no reemplazarían los
estados documentales existentes. El inventario previo sería un punto de partida,
no una lista de entidades aprobadas.

**Estado:** Luis lo consultará con el equipo. No se ha aprobado la reorganización
ni creado estos catálogos. Las fichas actuales conservan las aportaciones y su
procedencia; la estructura documental vigente sigue activa.

### Contraste de las fichas

| Distinción transversal | Evidencia en las fichas | Conclusión provisional para interiorizar |
|---|---|---|
| Identidad / estado / código | Ángel §2 distingue ocurrencia y revisión; Luis §2 conserva la zapata al cambiar dimensiones o pertenencia, aunque cambie su código; Miguel A.4 usa el TAG del equipo. | El identificador interno, la etiqueta externa y el estado revisado responden a preguntas distintas. No usar perfil, coordenadas, TAG ni código compuesto como única identidad universal. |
| Qué es / cómo se dibuja | Ángel §5 admite perfil y geometría 3D libre; Luis §§1 y 3 define la zapata por su función, no por ser un sólido de hormigón; Miguel A.1–A.3 delimita el equipo y su apoyo. | Una geometría sirve para representar un objeto físico, pero no determina sola su función ni sus límites. Materiales y partes pueden variar por familia. |
| Pertenencia / ubicación / conexión / apoyo | Ángel §4 separa estructura, área, ejes y sistema; Luis §§1–2 distingue conjunto de cimentación y estructuras apoyadas; Miguel E.19–E.21 localiza la interfaz del equipo. | No expresar todo mediante un único `parent`. Cada relación debe decir qué significa y, cuando proceda, conservar posición, revisión y demás datos propios. |
| Acción / caso / aplicación / resultado | Miguel §§1–3 separa origen físico, acción, `LoadCase` y `AppliedLoad`; Luis §5 vincula análisis y comprobaciones; Ángel §10 sitúa resultados en una ejecución analítica. | La carga no es un número fijo en la zapata, viga o columna. Su procedencia, agrupación, aplicación al modelo y resultados calculados son planos diferentes. |
| Físico / idealización analítica | Ángel §§7–8 representa una columna con una o dos barras; Luis §5 ofrece apoyo equivalente, placas, cálculo manual y algoritmos; Miguel F.24–F.25 aplica una acción a nodo o barra. | Un objeto físico puede participar en varios análisis con topologías o métodos diferentes. La diferencia analítica no modifica automáticamente el objeto físico. |
| Procedencia / revisión / vigencia | Ángel §§8–9 separa snapshot, mapping y evaluación de alineación; Luis §5.2 pide evidencias y aprobación técnica; Miguel F y su pregunta de signos exigen contexto del modelo. | Conservar de dónde salió cada dato y frente a qué revisión se usó. Relación histórica, vigencia técnica y aprobación humana son evaluaciones distintas. |
| Coordenadas y condiciones de contexto | Ángel §5 resuelve placement sin convertir ejes en identidad; Luis §§3–4 sitúa la zapata y asigna condiciones geotécnicas por regla; Miguel pregunta adicional fija marco y signo de la acción. | Posición, sistema de referencia, unidades, signo y regla de asignación deben poder explicarse. Compartir área o conjunto no prueba igualdad de terreno o carga. |

La estructura de razonamiento que emerge es:

```text
Objeto físico y su revisión
├── forma, materiales, placement y relaciones físicas
├── puede originar o recibir acciones con contexto propio
└── se corresponde con una o varias representaciones/modelos de análisis
      └── cada ejecución produce resultados y evidencias
            └── algunas evidencias sustentan comprobaciones y validación
```

Las flechas no son todas composición. Una acción no es parte material del objeto;
un modelo analítico no es hijo de la columna o de la zapata; una comprobación no es
una propiedad intrínseca del sólido.

## Conceptos transversales candidatos, sin fijar entidades

1. **Ocurrencia física y revisión.** Identidad continuada frente a estado concreto
   de diseño. Hay que declarar la política de continuidad para división, fusión,
   traslado y sustitución; las tres fichas no la resuelven igual.
2. **Representación y composición física.** Forma paramétrica o libre, distintos
   niveles de detalle, material único o por partes. Conservar la función del elemento
   aunque cambie su forma o el formato recibido.
3. **Relaciones físicas tipadas.** Pertenencia, composición, conexión, interfaz,
   apoyo, localización y asignación geotécnica no son sinónimos. Falta el contraste
   de Alberto antes de definir su vocabulario.
4. **Acción y aplicación analítica.** Una acción con origen y contexto puede
   proyectarse sobre modelos distintos; la aplicación concreta pertenece al modelo
   y debe conservar posición, unidades y convenio de signos.
5. **Análisis con propósito y procedencia.** Distinguir idealización, método,
   ejecución, resultado, comprobación y validación. El cálculo manual o algorítmico
   de Luis impide exigir nodos y barras a *todo* análisis.
6. **Correspondencia y evaluación.** Relacionar físico y analítico en revisiones
   concretas, con cardinalidad y evidencia. Evaluar aparte si sigue alineado con
   cambios posteriores; eso no equivale a validar técnicamente el elemento.

Estos son focos de discusión, no seis tablas propuestas. En particular, no se
deduce que una única clase `AnalyticalModel` deba representar sin pérdida tanto un
mallado externo como un cálculo manual de sólido rígido.

## Vocabulario mínimo propuesto para contrastar (v0.1)

Los términos siguientes son **significados compartidos candidatos**, no nombres de
entidades de base de datos. Se proponen a partir de las tres fichas y de la lectura
de Ángel del 14 de septiembre; Luis, Miguel y Alberto aún deben contrastarlos.

| Término | Significado operativo | Ejemplo y límite |
|---|---|---|
| **Ocurrencia de diseño** | Elemento concreto que el proyecto pretende definir y seguir entre revisiones, con identidad interna distinta de sus etiquetas visibles. | La ocurrencia mostrada como `C-101` puede cambiar perfil o posición; no equivale a la pieza fabricada ni al activo instalado. |
| **Estado de diseño aceptado** | Definición física de la ocurrencia que el CDM reconoce para una revisión, con evidencia y responsable. No se obtiene automáticamente de la última importación. | `C-101 @ R03` y `@ R04` pueden ser estados de la misma columna; antes de aceptarlos pueden coexistir datos de fuente contradictorios. |
| **Modelo fuente y revisión** | Entrega concreta de una aplicación o proceso, con alcance —completo o parcial— y procedencia conocidos. | `SP3D P12` puede contener una representación física; `STAAD S05`, una analítica. El nombre del programa no fija por sí solo el rol de todos sus objetos. |
| **Snapshot importado** | Lo que una fuente afirmó sobre un objeto en una revisión, aunque aún no se haya aceptado como estado de diseño. | `SP3D P12 / C-44` puede diferir de `Tekla T07 / T-9`; ninguna copia sobrescribe silenciosamente a la otra. |
| **Referencia externa** | Identificador de un objeto dentro de su aplicación, modelo y revisión. | `C-44` en SP3D no es el ID interno del CDM ni tiene significado global por sí solo. |
| **Conciliación de identidad** | Afirmación justificada de que dos objetos *físicos* importados representan la misma ocurrencia de diseño. | Útil si Tekla y SP3D modelaron físicamente `C-101` por separado; puede quedar ambigua y requerir confirmación. |
| **Representación física** | Forma o descripción recibida/derivada de la ocurrencia en una revisión. | Un sólido o perfil con trayectoria muestra `C-101`; no sustituye su identidad ni su función. |
| **Idealización analítica** | Objeto o formulación creada para un análisis y un propósito concretos. | Una barra de STAAD o dos barras de otro modelo pueden idealizar `C-101`; no son piezas físicas adicionales. |
| **Correspondencia físico–analítica** | Relación trazable entre un estado físico —o su fuente identificada si aún no está aceptado— y objetos/zonas analíticos, con cardinalidad y evidencia. | Si `C-1` de STAAD es una **barra analítica** y `C-44` de SP3D una **columna física**, necesitamos esta correspondencia, no afirmar que son el mismo objeto. |
| **Acción / aplicación analítica** | La primera expresa el efecto con origen y contexto; la segunda indica cómo entra en una revisión de análisis. | El peso transmitido por `EQ-101` no es un campo fijo de `F-101`; en un cálculo puede aplicarse a nodo o barra. Magnitud por caso sigue en debate. |
| **Tipo intencional / agrupación derivada** | El tipo se declara para reutilizar una intención dentro de un alcance conocido; la agrupación se obtiene comparando propiedades. | Dos zapatas idénticas pueden quedar en el mismo grupo calculado sin que se les haya declarado el mismo tipo. |
| **Baja propuesta / baja aceptada** | La desaparición en una fuente es evidencia que puede proponer una baja; solo una decisión del CDM retira la ocurrencia del diseño. | Si `C-44` falta en `SP3D P13`, primero se verifica alcance y continuidad. Si se acepta la baja, se retira la ocurrencia sin borrar su historia ni reutilizar su ID interno. |

La precisión más importante para la conversación `STAAD C-1` ↔ `SP3D C-44` es
preguntar **qué representa cada ID**. Dos objetos físicos se *concilian en una
ocurrencia*; un objeto analítico se *corresponde con* una ocurrencia física. Son
relaciones diferentes aunque ambas permitan navegar hacia `C-101`.

### Prueba de convergencia para la reunión

1. Para cada término, acordar una frase de definición y probarla con `C-101`,
   `F-101` y `EQ-101` cuando aplique. Anotar al menos un caso que **no** cubre. Si
   falla, separar significados en vez de buscar un nombre más vago.
2. Marcar cada definición como **acordada en reunión**, **provisional** o **abierta**;
   anotar quién debe contrastarla y qué evidencia falta. Ninguna pasa a `CANONICAL`
   automáticamente.
3. Probar el flujo de baja: modelo completo anterior → objeto ausente en nueva
   revisión → propuesta con evidencia → aceptación/rechazo en CDM. La ausencia en
   una exportación parcial no basta para dar de baja la ocurrencia.
4. Probar el flujo de semilla y el de importaciones independientes. Preferir que el
   CDM distribuya referencias estables cuando los conectores lo permitan, pero
   conservar una conciliación explícita y revisable para modelos ya creados por
   separado. No prometer que cualquier programa pueda abrir o reconstruir el modelo
   del CDM sin comprobar su intercambio real.

### Simulación de mesa: tres fuentes y una baja

Caso **ficticio**, no comportamiento verificado de STAAD, SP3D ni Tekla. En este
proyecto se acepta temporalmente `SP3D P12` como semilla física de `ST-101`. Eso
define la autoridad de este ejemplo, no una regla universal del CDM.

| Paso | Lo que llega u ocurre | Lo que registra o decide el CDM |
|---|---|---|
| 1. Semilla | `SP3D P12` es una entrega completa de `ST-101` y contiene la columna física `C-44`, HEB 200. | Crea la ocurrencia interna `O-017`, mostrada en el ejercicio como `C-101`; conserva el snapshot `P12/C-44` y, tras aceptarlo, el estado físico `O-017 @ R03`. `C-44` sigue siendo solo la referencia externa. |
| 2. Modelo analítico | Llega `STAAD S05 / C-1`, una barra que idealiza esa columna. Si el conector conservó el ID del CDM, lo aporta; de lo contrario, la coincidencia necesita evidencia y confirmación. | Conserva el snapshot analítico y una **correspondencia físico–analítica** `O-017 @ R03 ↔ S05/C-1` (aquí `1:1`). No convierte la barra en la columna física ni exige que compartan nombre. |
| 3. Segundo físico independiente | Llega `Tekla T07 / T-9`, pieza física semejante sin referencia CDM conservada. | Propone una **conciliación de identidad** con `O-017`; compara ubicación, perfil, estructura y relaciones. Si se confirma, enlaza `T07/T-9` sin sobrescribir `P12/C-44`. Si es dudosa, permanece ambigua. |
| 4. Desaparición | En `SP3D P13`, entrega comprobada como completa para `ST-101`, ya no aparece `C-44`. | Primero comprueba que no sea un cambio de ID, una sustitución o un error de intercambio. Si no encuentra continuidad, abre **propuesta de baja** de `O-017`. `STAAD S05` y `Tekla T07` todavía existen; la columna no se borra automáticamente. |
| 5. Decisión | El responsable autorizado acepta que la intención de diseño eliminó la columna. | Registra **baja aceptada**: `O-017` deja de estar activa desde esa revisión, pero conserva historia y correspondencias. Avisa que las representaciones externas que aún la contienen deben revisarse; no edita esos programas por su cuenta. |

Si `P13` fuese una exportación parcial, o `C-44` simplemente hubiese pasado a otro
ID nativo, la propuesta se rechazaría o quedaría pendiente: `O-017` seguiría activa.
Si después se diseña otra columna en las mismas coordenadas tras aceptar la baja,
sería una **nueva ocurrencia** con otro ID interno. La posible reutilización de la
etiqueta visible `C-101` es una política de códigos todavía abierta.

La simulación permite preguntar en cada paso: ¿es una identidad de diseño, una
referencia de fuente, una representación física, una idealización analítica, una
correspondencia o una decisión? Si dos personas responden distinto, ese término
todavía no ha convergido.

**Ensayo de la conversación de vocabulario:**

- «`C-1` de STAAD es la misma columna que `C-44` de SP3D». Se pregunta qué es cada
  objeto. Si `C-1` es una barra analítica, se sustituye «misma columna» por
  «correspondencia físico–analítica». Si ambos son piezas físicas, se estudia la
  «conciliación de identidad».
- «La columna desapareció de SP3D; ya no existe». Se comprueba cobertura de la
  importación y continuidad de IDs. Se anota «ausente en esa fuente» y, si procede,
  «baja propuesta»; solo una decisión aceptada cambia el estado de la ocurrencia.
- «Estas dos zapatas tienen el mismo tipo porque son iguales». Se pregunta si el
  tipo fue declarado dentro de un alcance común. Si solo coinciden sus propiedades,
  se habla de «agrupación derivada», no de tipo intencional compartido.

El resultado de este ensayo no es imponer palabras: es descubrir en qué frases
distintas personas estaban afirmando cosas distintas con el mismo término.

## Tensiones que no debemos esconder

| Tema | Lecturas que aún no encajan | Pregunta concreta para la reunión |
|---|---|---|
| Identidad, TAG y lifecycle | Ángel propone identidad interna de ocurrencia de diseño sin TAG empresarial para la columna; la baja se aceptaría en CDM tras una desaparición detectada en fuente. Luis propone un código de zapata que cambia con su pertenencia; Miguel utiliza TAG estable y habla de sustitución física del equipo. | ¿Puede el equipo aceptar identidad de diseño separada de códigos y reservar pieza fabricada/activo instalado para una extensión posterior? ¿Quién tiene autoridad para aceptar la baja? |
| Tipo reutilizable | Luis asocia compartir tipo a igualdad de geometría, materiales y armado; Ángel propone tipo **intencional**, de alcance contextual (proyecto, assignment, entregable o plano), separado de una agrupación derivada por propiedades. | ¿Llamamos `tipo` solo a la intención explícita y damos otro nombre a la firma de igualdad? ¿Qué alcance real tiene cada tipo de las fuentes actuales? |
| Interfaz física y rigidez analítica | Miguel E.21 describe el apoyo como articulado y lo aproxima a un release; Ángel §6 advierte que conexión física y condición analítica no equivalen directamente. | ¿Qué observamos físicamente en la pata/placa y qué decide cada cálculo sobre su rigidez? Esperar la ficha de Alberto antes de fijarlo. |
| Identidad de acción y valor por estado | Miguel usa `ACC-EQ101-V` en los casos vacío y lleno, que implican magnitudes diferentes. | ¿La identidad de la acción es común y el valor depende del estado/caso, o son dos acciones relacionadas? No fijar el esquema de carga antes de aclararlo. |
| Cardinalidad de una acción | Miguel F.26 propone una sola aplicación por modelo para su carga puntual; Ángel permite mappings físicos `1:N` y Luis contempla varios apoyos y análisis. | ¿La regla `1:1` es solo del ejemplo de una pata, o queremos admitir repartos y varias aplicaciones de una misma acción en un modelo? |
| Qué cuenta como «modelo analítico» | Ángel trata topologías importadas con nodos/barras; Miguel distingue aplicación nodo/barra; Luis añade formulaciones manuales, algoritmos y elementos finitos. | ¿Qué comparten todas estas formas: hipótesis, entradas, propósito y revisión? ¿Qué solo existe en un modelo discretizado? |
| Vigencia frente a validación | Ángel evalúa si un modelo sigue alineado con el físico; Luis requiere aprobación humana de comprobaciones y puede sustituir evidencias parcialmente. | Si cambia una carga o un perfil, ¿qué se marca para revisar: mapping, análisis, comprobación, validación o varios, y quién decide? |
| Geotecnia y propiedad de datos | Luis exige asignación de condiciones por zapata/pilote; Ángel no presupone una fuente maestra universal. | ¿Qué fuente y regla determinan las condiciones aplicables y cómo queda la procedencia de una capacidad geotécnica calculada? |

Estas discrepancias son material de trabajo, no errores que deban corregirse
silenciosamente en las fichas individuales.

## Prioridad sugerida para la reunión

1. Contrastar primero el vocabulario de identidad, fuente y correspondencia con la
   simulación anterior; después precisar acción, aplicación, resultado,
   comprobación y validación. No debatir todavía estructuras de base de datos.
2. Resolver con ejemplos los dos cruces más peligrosos: `TAG/código` frente a
   identidad interna y `conexión física` frente a condición de extremo analítica.
3. Contrastar un único recorrido completo: `EQ-101` → apoyo/interfaz → acción →
   representación de `B-101/C-101` → apoyo de `F-101` → análisis/comprobación.
   Indicar en cada flecha si es dato declarado, importado, inferido o calculado.
4. Registrar lo que falte de Alberto y seleccionar **una prueba de intercambio
   real** antes de profundizar en adaptadores o en un modelo analítico maestro.

**Salida esperada:** glosario provisional de términos con significado compartido,
lista corta de relaciones distintas, preguntas asignadas y un ejemplo cuya
trazabilidad podamos verificar. Ni las fichas ni esta síntesis pasan a `CANONICAL`
por el mero hecho de reunirse.
