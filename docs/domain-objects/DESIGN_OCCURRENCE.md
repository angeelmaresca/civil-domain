# Ocurrencia de diseño

> **Status:** DRAFT
> **Editable:** sí; definición conceptual para contraste del equipo
> **Document owner:** equipo de dominio civil
> **Canonical for:** —
> **Sources:** [síntesis de la primera iteración](../iteration-01/SINTESIS.md), fichas de [Ángel](../iteration-01/FICHA_ANGEL_COLUMNA.md), [Luis](../iteration-01/FICHA_LUIS_ZAPATA.md) y [Miguel](../iteration-01/FICHA_MIGUEL_ACCIONES_CARGAS.md), [estudio IFC](../research/IFC_CORE_CONCEPTS.md) y decisión del equipo del 2026-09-18
> **Supersedes:** —
> **Last reviewed:** 2026-09-18

## Decisión de partida

Conviene comenzar el modelo por `OcurrenciaDeDiseño` porque columna, zapata y equipo
necesitan una identidad estable mientras cambian sus datos y representaciones. No
conviene convertirla en una raíz universal de todo el CDM. Acciones, tipos, espacios,
sistemas funcionales, modelos analíticos, resultados y relaciones tienen criterios
de identidad distintos.

El nombre se mantiene por ahora por continuidad con la primera iteración. En este
documento significa específicamente una **ocurrencia física de diseño**. Si el CDM
necesita más adelante ocurrencias no físicas, se evaluará entonces una abstracción
más general; no se anticipa esa jerarquía.

## Definición candidata

Una **ocurrencia de diseño** es un individuo físico concreto que el proyecto pretende
crear, conservar, modificar o retirar y cuya identidad necesita seguirse a través
de uno o más estados de diseño.

La ocurrencia representa la continuidad del individuo proyectado, aunque todavía no
se haya fabricado o construido. No representa:

- la pieza fabricada o el activo instalado;
- un estado concreto de sus propiedades;
- su geometría, su TAG o su código en una aplicación;
- el tipo común que pueda compartir con otras ocurrencias;
- la barra, placa, nodo o formulación que lo idealiza en un análisis.

Esta frontera permite afirmar que `C-101 @ R03` y `C-101 @ R04` son estados de una
misma columna sin identificar esa columna con `C-44` de SP3D, `T-9` de Tekla o una
barra de STAAD.

## Identidad y estado

La separación mínima es:

```text
OcurrenciaDeDiseño O-017                   continuidad e identidad
├── EstadoDeDiseño R03                     definición aceptada en un contexto
│   ├── clase funcional: columna
│   ├── geometría, materiales y placement
│   └── relaciones vigentes en R03
└── EstadoDeDiseño R04
    ├── clase funcional: columna
    ├── geometría, materiales y placement modificados
    └── relaciones vigentes en R04
```

La ocurrencia no debe convertirse en una bolsa mutable con «los valores actuales».
Los datos que pueden cambiar y que explican una decisión de ingeniería pertenecen
al estado, a una relación versionada o a una evidencia de fuente. El estado aceptado
tampoco se deduce automáticamente de la última importación.

### Responsabilidades conceptuales mínimas

| Responsabilidad | Pertenece a la ocurrencia | Pertenece a otro concepto |
|---|---|---|
| ID interno estable y opaco | Sí | — |
| Naturaleza física pretendida y alcance de diseño | Sí | Se concretan mediante vocabulario o clasificación enlazada |
| Datos geométricos, materiales y placement | No | Estado de diseño y representaciones |
| TAG, código o GUID de una aplicación | No | Referencia externa contextualizada |
| Revisión aceptada | No como valor sobrescribible | Estado de diseño y decisión de aceptación |
| Tipo reutilizable | No | Definición de tipo y relación de tipado |
| Pertenencia, composición, apoyo o conexión | No como un único `parent` | Relaciones tipadas y, cuando cambien, versionadas |
| Forma analítica | No | Modelo/objeto analítico y correspondencia físico–analítica |
| Pieza construida | No | Futuro objeto de realización/activo y su correspondencia |

No se proponen todavía columnas de base de datos, clases de implementación ni una
API. La tabla reparte responsabilidades semánticas.

## Prueba para decidir quién es una ocurrencia

Un candidato debe cumplir las tres condiciones necesarias:

1. **Individualidad de proyecto:** se habla de este individuo y no solo de una clase,
   propiedad o selección de objetos.
2. **Referente físico intencional:** el proyecto pretende que exista como objeto o
   conjunto físico reconocible, aunque aún no esté construido.
3. **Continuidad:** tiene sentido preguntar si sigue siendo el mismo individuo tras
   cambiar geometría, material, posición, código o relaciones.

Además, debe existir al menos una razón de negocio para darle identidad separada:

- posee ciclo de vida o revisión propios;
- participa directamente en relaciones que deben trazarse;
- se diseña, entrega, valida, fabrica o sustituye de forma independiente;
- actúa como un todo físico con significado distinto de la mera suma consultada de
  sus miembros.

Si cumple las tres condiciones necesarias pero ninguna razón práctica exige
seguirlo separadamente, puede mantenerse como parte descrita dentro de un estado.
Se promociona a ocurrencia cuando aparezca esa necesidad, sin inventar identidades
para cada detalle geométrico.

### Casos iniciales

| Candidato | ¿Ocurrencia de diseño? | Motivo provisional |
|---|---|---|
| Columna `C-101` | Sí | Individuo físico proyectado con revisiones, conexiones y representación analítica propias. |
| Zapata `F-101` | Sí | Conserva identidad al cambiar dimensiones o armado y participa en apoyos, análisis y validaciones. |
| Equipo `EQ-101` | Sí, dentro del alcance compartido | Es un individuo físico de proyecto; que otra disciplina gobierne parte de sus datos no elimina su identidad. |
| Pilote `P-01` | Sí cuando se identifica, posiciona y controla individualmente | Puede conservarse al sustituir el encepado y tener posición prevista/ejecutada propia. |
| Armadura completa de una zapata | Abierto | Puede ser una composición del estado o una ocurrencia/assembly si se entrega y controla como conjunto independiente. |
| Cada barra de armadura | No por defecto | Evitar identidad individual si solo materializa una disposición; sí podría serlo si fabricación, montaje o trazabilidad lo requieren. |
| Perfil HEB 300 | No | Es una definición reutilizable o clasificación, no el individuo `C-101`. |
| Sólido de `C-101` | No | Es una representación física de un estado. |
| Barra analítica de STAAD | No | Es un objeto analítico que idealiza uno o varios estados físicos. |
| Acción, combinación o resultado | No | Son conceptos de análisis o información, no individuos físicos proyectados. |
| Selección «todas las columnas del área A» | No | Es un conjunto derivado por consulta, sin identidad física propia. |

## ¿Una estructura es una ocurrencia?

«Estructura» es un término polisémico. La respuesta depende de qué se esté afirmando,
no de la etiqueta utilizada.

### 1. Estructura como conjunto físico concreto

Sí puede ser una ocurrencia de diseño. Una estructura soporte `ST-01`, un pórtico o
un módulo pueden tener identidad, límite, revisión y ciclo de vida propios y estar
compuestos por columnas, vigas, arriostramientos y uniones que son a su vez
ocurrencias.

```text
OcurrenciaDeDiseño ST-01  --se compone físicamente de--> C-101, B-101, BR-101…
```

El todo no necesita una geometría duplicada: su forma puede derivarse de sus partes.
Tampoco debe crearse automáticamente una ocurrencia para cualquier agrupación. El
conjunto físico debe superar la prueba de individualidad, referente, continuidad y
utilidad de identidad.

### 2. Estructura como sistema funcional

No es la misma entidad. Si «estructura» significa «conjunto de elementos que
participan en el sistema resistente», se modela como sistema o agrupación funcional.
La pertenencia puede ser muchos-a-muchos, no implica propiedad física y no determina
por sí sola el ciclo de vida de los miembros.

```text
SistemaEstructural SYS-01  <--es miembro de--  C-101, B-101, F-101…
```

Puede coexistir con una ocurrencia física `ST-01` si ambos conceptos aportan valor,
pero no se deben crear dos objetos por rutina ni compartir un ID para ocultar que
responden a preguntas distintas.

### 3. Estructura como contenedor espacial

No es una ocurrencia física por ese solo hecho. Área, planta, nivel, edificio o parte
de instalación organizan dónde se considera contenido un elemento. Un contenedor
espacial puede tener identidad y placement propios, pero pertenece a otra familia
conceptual. La relación de contención espacial no sustituye a la composición física.

### 4. Estructura como modelo analítico

No. Un modelo estructural de STAAD, SAP2000 u otra herramienta es un modelo analítico
con propósito, hipótesis, revisión, objetos y ejecuciones. Se corresponde con
ocurrencias físicas, pero no es una de ellas.

### 5. Estructura como tipo

No. «Pipe rack tipo PR-A» o «pórtico tipo» es una definición reutilizable. Una
estructura concreta que adopte esa intención sí puede ser una ocurrencia.

## Entidades vecinas necesarias

Empezar por la ocurrencia no significa modelarla aislada. El primer corte conceptual
necesita al menos estas responsabilidades, aunque varias aún no tengan archivo propio:

| Concepto candidato | Pregunta que responde | Relación con la ocurrencia |
|---|---|---|
| `EstadoDeDiseño` | ¿Cómo se definió el individuo en una revisión aceptada? | Estado versionado de una ocurrencia. |
| `DefinicionDeTipo` | ¿Qué intención común se declara reutilizable? | Puede tipar estados u ocurrencias dentro de un alcance. |
| `RevisionDeModeloFuente` y `SnapshotImportado` | ¿Qué afirmó una fuente concreta? | Aporta evidencia; no sobrescribe la ocurrencia. |
| `RepresentacionFisica` | ¿Cómo se muestra o describe la forma? | Representa un estado para un propósito. |
| `SistemaFuncional` | ¿Qué objetos colaboran para una función? | Agrupa ocurrencias sin poseerlas. |
| `ContextoEspacial` | ¿Dónde se contiene principalmente el objeto? | Contiene o referencia ocurrencias. |
| `ModeloAnalitico` y `ObjetoAnalitico` | ¿Cómo se idealiza para calcular? | Se enlazan mediante correspondencias trazables. |
| `RelacionDeDiseño` | ¿Qué vínculo semántico existe y cuándo? | Conecta ocurrencias u otros objetos sin reducirse a `parentId`. |
| `DecisionDeAceptacion` | ¿Quién aceptó qué estado y con qué evidencia? | Determina vigencia técnica sin borrar historia. |

Esta lista es un mapa de dependencias, no una lista aprobada de tablas.

## Relaciones de primer nivel

La semántica y cardinalidad candidatas viven en
[`RELATIONSHIPS.md`](../RELATIONSHIPS.md). Para esta entidad son esenciales:

- `tiene estado de diseño`;
- `se compone físicamente de`;
- `es miembro de sistema`;
- `está contenido espacialmente en`;
- `se conecta con`, `da apoyo a` y `transmite acciones a`;
- `está tipado por` y `está clasificado como`;
- `está representado por`;
- `se corresponde con objeto analítico`;
- `está documentado por snapshot de fuente`;
- `sustituye a`, cuando hay fusión, división o reemplazo sin continuidad de identidad.

No todas unen dos ocurrencias ni todas comparten lifecycle, cardinalidad o autoridad.

## Reglas candidatas de identidad

Las reglas propietarias se mantienen en [`RULES.md`](../RULES.md). Las consecuencias
más importantes para esta definición son:

- cambiar propiedades no crea automáticamente otra ocurrencia;
- dividir, fusionar o sustituir exige una decisión explícita de continuidad;
- desaparecer de una fuente no equivale a causar baja en el CDM;
- el ID interno no se recicla ni se deriva de TAG, geometría o posición;
- una relación cambiante pertenece a un contexto o estado, no a una verdad eterna;
- objeto físico y objeto analítico nunca se concilian como si fueran la misma cosa.

## Correspondencia con IFC sin copiar su jerarquía

La propuesta adopta varias lecciones de IFC:

- separar ocurrencia y tipo;
- distinguir objeto, representación y placement;
- usar relaciones con semántica explícita;
- separar composición física, agrupación funcional y contención espacial;
- admitir que un assembly físico tenga identidad y partes propias;
- mantener el modelo analítico separado del producto físico.

La equivalencia no es uno-a-uno. IFC usa «ocurrencia» para objetos físicos,
espaciales, conceptuales, procesos, controles y actores. El CDM restringe por ahora
`OcurrenciaDeDiseño` al individuo físico intencional porque ese es el problema de
identidad demostrado por las fichas. Un adaptador IFC deberá decidir el significado
de cada objeto recibido; no basta con comprobar que hereda de `IfcObject` o
`IfcProduct`.

Una estructura física compuesta se aproxima al patrón de producto/assembly; un
sistema funcional, al patrón de grupo/sistema; una instalación o edificio usado
como estructura espacial, al patrón de facility/spatial structure. Estas analogías
orientan la separación, pero no determinan las entidades internas del CDM.

## Preguntas que debe resolver el siguiente ejemplo

1. ¿`ST-01` tiene una identidad física que sobreviva a sustituir una columna, o solo
   es una agrupación funcional nombrada?
2. ¿Qué partes poseen lifecycle independiente y cuáles son detalle del estado del
   conjunto?
3. ¿Puede una ocurrencia formar parte físicamente de más de un todo a la vez, o esa
   aparente pertenencia mezcla composición con sistema, apoyo o conexión?
4. ¿El tipo se aplica a la continuidad completa o puede cambiar entre estados? La
   segunda opción parece necesaria para la zapata de Luis.
5. ¿Qué autoridad acepta un estado y qué autoridad decide continuidad, sustitución,
   división, fusión y baja?
6. ¿Cómo se enlaza en un caso real la estructura física, su contenedor espacial y su
   sistema resistente sin usar un único `parent`?

El siguiente contraste recomendado es modelar `ST-01` con `C-101`, `B-101` y
`F-101` en dos variantes: como conjunto físico con identidad y como sistema funcional.
Si el equipo obtiene las mismas respuestas en ambas, una entidad sobra; si cambian
lifecycle, cardinalidades o responsabilidades, deben permanecer separadas.
