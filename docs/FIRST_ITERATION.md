# Primera iteración — conceptualización mediante ejemplos

> **Status:** DRAFT
> **Editable:** sí mientras figure como documento activo en `WORKING_SET.md`
> **Document owner:** equipo de dominio civil
> **Canonical for:** —
> **Sources:** [`IFC_CORE_CONCEPTS.md`](research/IFC_CORE_CONCEPTS.md), experiencia del equipo y casos de Footings
> **Supersedes:** —
> **Last reviewed:** 2026-09-10

## 1. Objetivo

Cada participante estudiará un ejemplo físico reconocible y lo describirá en los
distintos planos que pueden coexistir:

```text
realidad física
├── identidad, significado y lifecycle
├── tipo, clasificación y propiedades
├── partes, conjuntos, sistemas y ubicación
├── placement y representaciones geométricas
├── materiales
├── conexiones e interfaces
├── acciones relacionadas
└── una o varias representaciones analíticas
```

La finalidad de esta primera vuelta no es producir un modelo correcto ni completo.
Buscamos que las cuatro aportaciones sean comparables y revelen conceptos ambiguos,
relaciones diferentes y cuestiones que necesiten investigación.

## 2. Caso común de referencia

Para facilitar la discusión, todas las fichas pueden situarse dentro del mismo caso
ficticio:

```text
Equipo EQ-101
└── interfaces de apoyo y acciones
    └── estructura soporte ST-01
        ├── viga B-101
        └── columna C-101
            └── placa base BP-101 + pernos
                └── grout G-101
                    └── pedestal PD-101
                        └── zapata F-101
                            └── terreno
```

El esquema no afirma que todas las líneas sean la misma relación. Precisamente habrá
que distinguir composición, conexión, apoyo, pertenencia a sistema, ubicación y
transmisión de acciones.

Se puede cambiar el ejemplo si otro caso real permite explicar mejor el foco. Debe
conservarse una ocurrencia concreta —con nombre ficticio— para evitar respuestas
demasiado genéricas.

## 3. Entrega mínima

Cada persona traerá una ficha breve, preferiblemente de una a tres páginas, con:

1. nombre y dibujo o diagrama mínimo del ejemplo;
2. respuestas cortas a la batería común; `desconocido` o `no aplicable` son válidos;
3. un mapa de objetos y relaciones, sin tablas de base de datos;
4. hasta cinco conceptos candidatos;
5. tres dudas o decisiones que deban discutirse;
6. un ejemplo de simplificación válida y otro de diseño que considere frágil.

No se pide investigar todo IFC, crear código ni responder todas las variantes
posibles del elemento.

## 4. Batería común de preguntas

### A. Realidad, significado e identidad

1. ¿Qué objeto físico concreto estamos observando?
2. ¿Qué función cumple y qué lo diferencia de elementos con una forma parecida?
3. ¿Dónde empieza y termina? ¿Qué queda expresamente fuera?
4. ¿Necesita identidad propia? ¿Qué debe poder cambiar sin perder esa identidad?
5. ¿Puede existir de forma independiente o depende del lifecycle de otro objeto?

### B. Ocurrencia, tipo, clasificación y propiedades

6. ¿Qué información pertenece a esta ocurrencia concreta?
7. ¿Qué definición podría reutilizarse como tipo en otras ocurrencias?
8. ¿Qué términos son clasificaciones y no tipos propios del modelo?
9. ¿Qué propiedades son esenciales para su significado y cuáles son información
   adicional o dependiente de una fase?

### C. Jerarquías, sistemas y composición

10. ¿Quién posee el objeto durante su lifecycle?
11. ¿Dónde está contenido espacialmente?
12. ¿A qué estructura o sistema funcional pertenece? ¿Puede pertenecer a varios?
13. ¿Está compuesto por partes con identidad o contiene características sin
    lifecycle propio, como huecos o recrecidos?
14. ¿Qué relaciones del caso parecen jerárquicas y cuáles forman realmente un grafo?

### D. Placement, geometría y materiales

15. ¿Respecto a qué sistema de coordenadas se posiciona?
16. ¿Qué geometría expresa intención editable y cuál se obtiene por cálculo?
17. ¿Necesita representaciones distintas —eje, cuerpo, envolvente, detalle o estado
    construido— sin cambiar de identidad?
18. ¿Tiene un material único, varias partes materiales, capas, perfiles o armadura?

### E. Conexiones, interfaces y acciones

19. ¿Con qué objetos se conecta, apoya, une o entra en contacto?
20. ¿La conexión es un punto, línea, superficie, volumen o conjunto de componentes?
21. ¿La relación necesita datos propios —posición, rigidez, holgura, capacidad,
    estado o revisión—?
22. ¿Qué acciones recibe, genera o transmite? ¿Cuál es su origen y objetivo?

### F. Modelo analítico

23. ¿Necesita representación analítica para algún propósito concreto?
24. ¿Qué nodos, barras, superficies, sólidos, apoyos o resortes la representan?
25. ¿Podría representarse de formas diferentes en modelos analíticos distintos?
26. ¿La correspondencia físico–analítica es uno a uno, uno a varios o varios a uno?
27. ¿Qué información pertenece al modelo analítico y no al objeto físico?

### G. Procedencia, intercambio y límites

28. ¿Qué disciplina o aplicación es propietaria de los datos originales?
29. ¿Qué identidad externa debería conservarse al importar desde otro sistema?
30. ¿Qué información podríamos traducir de forma exacta y cuál sería aproximada o
    podría perderse?
31. ¿Qué estamos suponiendo por comodidad y qué extensión futura podríamos bloquear?

## 5. Focos provisionales

Estos encargos delimitan una primera exploración. Se revisarán en la siguiente
reunión y no asignan ownership permanente del futuro dominio.

### Alberto — Conexiones e interfaces

**Ejemplo físico sugerido:** placa base `BP-101` y su encuentro con columna, pernos,
grout y pedestal.

**Objetivo:** distinguir las piezas físicas de las relaciones e interfaces que las
unen.

Preguntas prioritarias:

- ¿Qué es parte de un conjunto y qué es un elemento relacionado?
- ¿Conectar, apoyar, anclar, adherir y estar en contacto son relaciones diferentes?
- ¿Dónde se localiza la conexión: en un punto, eje, superficie o patrón?
- ¿Qué propiedades pertenecen a la conexión y no a sus extremos?
- ¿Puede una misma interfaz participar en varios modelos analíticos?
- ¿Qué parte de la transmisión de cargas es intención persistente y cuál es cálculo?

**Resultado buscado:** un pequeño vocabulario de relaciones y un diagrama donde no
se utilice un `parent` genérico para expresar todo.

### Luis — Zapata

**Ejemplo físico sugerido:** zapata aislada `F-101` del caso común.

**Objetivo:** comprobar cómo una zapata conserva significado e identidad admitiendo
geometrías, materiales, relaciones con terreno y modelos analíticos diferentes.

Preguntas prioritarias:

- ¿Qué hace que el objeto sea una zapata y no solo un sólido de hormigón?
- ¿Qué variantes son tipos y cuáles son diferencias geométricas de una ocurrencia?
- ¿Pedestal, armadura, huecos y recrecidos son partes, características o elementos?
- ¿Cómo se expresa la interfaz con el terreno?
- ¿Qué geometría es editable, calculada o importada?
- ¿Cómo puede representarse como apoyo, superficie, placas o sólidos analíticos?

**Resultado buscado:** mapa de la zapata física y al menos dos representaciones
analíticas alternativas sin duplicar su identidad.

### Miguel — Acciones y cargas

**Ejemplo físico sugerido:** equipo `EQ-101` y una de sus interfaces de apoyo como
origen del paquete de acciones que llega a la estructura.

**Objetivo:** separar el objeto físico que origina o recibe acciones de la definición
de acción, su agrupación y su aplicación analítica.

Preguntas prioritarias:

- ¿Qué diferencia hay entre acción, valor de carga, caso o hipótesis, combinación y
  envolvente?
- ¿Dónde se aplican fuerza, momento, presión o desplazamiento impuesto?
- ¿En qué sistema de coordenadas y con qué convenio de signos se expresan?
- ¿Cómo se conserva el origen: equipo, peso propio, viento, sismo u otra disciplina?
- ¿Cómo cambia una misma acción al proyectarse sobre modelos analíticos diferentes?
- ¿Qué es input y qué combinación, propagación o resultado es derivado?

**Resultado buscado:** recorrido de una acción desde su fuente física hasta dos
posibles aplicaciones analíticas, sin guardar la carga como propiedad de la zapata.

### Ángel — Elemento estructural físico y analítico

**Ejemplo físico sugerido:** viga `B-101` o columna `C-101` de la estructura soporte.

**Objetivo:** estudiar la separación y correspondencia entre elemento construido y
objetos analíticos importados o generados para distintos modelos.

Preguntas prioritarias:

- ¿Qué identidad, tipo, perfil, material, placement y geometría tiene el físico?
- ¿Cómo se representa mediante eje, barra, superficies o sólidos?
- ¿Puede participar simultáneamente en modelos de STAAD, SAP2000 u otros programas?
- ¿Cómo se resuelven correspondencias uno a varios y varios a uno?
- ¿Qué ocurre con nodos, offsets, ejes locales, releases y conexiones?
- ¿Cómo se registra una traducción exacta, normalizada, aproximada o no soportada?

**Resultado buscado:** dos modelos analíticos alternativos del mismo elemento físico
y las correspondencias necesarias para conservar procedencia.

## 6. Ejemplo resuelto — pedestal PD-EX-01

Este ejemplo es una guía de nivel de detalle, no una definición aprobada.

### 6.1 Situación

`PD-EX-01` es un pedestal de hormigón armado que nace sobre la zapata `F-EX-01` y
recibe una placa base mediante una capa de grout y un conjunto de pernos.

```text
Columna C-EX-01
└── Placa BP-EX-01 + pernos
    └── Grout G-EX-01
        └── Pedestal PD-EX-01
            └── Zapata F-EX-01
```

### 6.2 Respuestas al mapa mínimo

| Plano | Respuesta provisional |
|---|---|
| Realidad física | Elemento de hormigón armado que eleva y conecta el apoyo superior con la cimentación |
| Identidad | `PD-EX-01`; puede cambiar de dimensiones sin convertirse necesariamente en otro pedestal |
| Límite | No incluye automáticamente zapata, grout, placa, pernos ni columna |
| Lifecycle | Puede diseñarse y revisarse junto a la cimentación; queda por decidir si puede sustituirse de forma independiente |
| Ocurrencia | El pedestal concreto `PD-EX-01` dentro de este diseño |
| Tipo | Podría reutilizar una definición paramétrica de pedestal, si varios comparten reglas y propiedades |
| Clasificación | Códigos IFC, bSDD o corporativos serían asociaciones externas, no su identidad ni su tipo interno |
| Propiedades | Dimensiones nominales, recubrimiento o resistencia requerida; debe decidirse cuáles son intención y cuáles derivadas |
| Ownership | Probablemente pertenece al conjunto o diseño de cimentación, no al sistema espacial donde está situado |
| Contención espacial | Área o unidad de planta en la que se localiza |
| Sistema | Puede pertenecer a la estructura soporte de un equipo sin que esta sea su propietaria |
| Composición | Hormigón y armadura; huecos e insertos pueden ser características o partes según su lifecycle |
| Placement | Sistema local respecto a la zapata o al sistema del conjunto de cimentación |
| Representación | Prisma paramétrico, sólido detallado y envolvente de coordinación pueden coexistir |
| Materiales | Hormigón en el cuerpo y acero en la armadura; no basta un único material para describir todo el conjunto |
| Conexiones | Apoyo o unión con la zapata; interfaz superior con grout, placa y pernos; no son necesariamente la misma relación |
| Acciones | Recibe acciones desde la superestructura y las transmite; los valores no son propiedades permanentes del pedestal |
| Analítico global | Puede idealizarse como tramo rígido, barra o simplemente como offset entre apoyo y estructura |
| Analítico local | Puede representarse mediante sólido o volumen de hormigón con contactos y pernos simplificados |
| Correspondencia | Un pedestal físico puede mapear a varios objetos dentro de un modelo y a modelos alternativos diferentes |
| Procedencia | Debe conservarse qué revisión física originó cada representación y qué aplicación la creó |

### 6.3 Posible mapa conceptual

```text
PhysicalElement PD-EX-01
├── kind: Pedestal
├── placement
├── GeometryRepresentation: paramétrica
├── GeometryRepresentation: cuerpo detallado
├── MaterialComposition
│   ├── hormigón
│   └── armadura
├── pertenece a System ST-EX-01
├── PhysicalConnection con F-EX-01
└── PhysicalConnection/Interface con G-EX-01 y anclajes

AnalyticalModel AM-GLOBAL
├── AnalyticalMember/Offset AO-01
└── PhysicalAnalyticalMapping: PD-EX-01 -> AO-01

AnalyticalModel AM-LOCAL
├── AnalyticalSolid AO-20..AO-35
├── contactos y condiciones de contorno
└── PhysicalAnalyticalMapping: PD-EX-01 -> AO-20..AO-35
```

Los nombres anteriores son etiquetas de discusión, no propuestas de tablas o clases.

### 6.4 Simplificación que podría ser válida

En una primera aplicación especializada, conservar una única geometría paramétrica
editable y generar el sólido detallado puede ser suficiente, siempre que la
identidad del pedestal no dependa del formato de esa geometría y quede documentado
qué representación es derivada.

### 6.5 Diseño frágil

```text
Pedestal
- footingParentID
- areaID
- structureID
- width / length / height
- concreteMaterialID
- rebarMaterialID
- loadN / loadVx / loadVy / loadMx / loadMy
- analyticalNodeTopID / analyticalNodeBottomID
```

El problema no es el número de campos. El diseño mezcla en una misma estructura:

- ownership, ubicación, pertenencia a sistema y apoyo físico;
- cuerpo de hormigón y armadura;
- acciones variables con propiedades físicas;
- una única idealización analítica con el elemento físico;
- una geometría rectangular concreta con el significado de pedestal.

Sería difícil incorporar otro modelo analítico, una geometría irregular, cargas por
casos o una relación diferente con la zapata sin modificar la identidad conceptual.

## 7. Discusión de la siguiente reunión

La reunión no debe comparar quién ha producido el modelo más completo. Debe buscar
coincidencias y contradicciones entre las cuatro fichas:

1. ¿Qué conceptos aparecen en al menos dos ejemplos con el mismo significado?
2. ¿Qué palabra se ha utilizado para significados diferentes?
3. ¿Qué relaciones no caben en una jerarquía única?
4. ¿Qué objetos físicos admiten varias representaciones analíticas?
5. ¿Qué conceptos parecen entidades y cuáles podrían ser valores, partes o
   relaciones?
6. ¿Qué diferencias dependen de la herramienta externa y no deberían entrar en el
   núcleo?
7. ¿Qué necesitamos investigar antes de la siguiente iteración?

El resultado será una revisión del alcance de cada foco, no la aprobación del modelo
de entidades.
