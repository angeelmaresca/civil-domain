# Ficha de Ángel — columna física y modelos analíticos

> **Status:** DRAFT
> **Editable:** sí; ficha individual de Ángel para la primera iteración
> **Document owner:** Ángel
> **Canonical for:** —
> **Sources:** [Enunciado](ENUNCIADO.md), conversación guiada y paquete de estudio offline
> **Supersedes:** copia de trabajo `offline/angel-first-iteration/02_ANGEL_WORKSHEET.md` como ficha activa
> **Last reviewed:** 2026-09-14

Caso elegido: columna `C-101`. `DESCONOCIDO` es una respuesta válida cuando falta
evidencia de los modelos externos. Esta ficha no aprueba entidades definitivas.

## 1. Caso elegido

**Nombre de la ocurrencia:** `C-101`, etiqueta usada en el ejercicio y posiblemente
en el modelo de origen; no se presupone que sea un TAG o identificador corporativo.

**Situación real o ficticia:** Caso ficticio común. `C-101` es una pieza estructural
de acero continua de la estructura soporte `ST-101`. Se extiende desde su conexión
con la placa base `BP-101` hasta una conexión superior concreta situada, a efectos
del ejercicio, en la cota `+6.000`.

**Función estructural:** Actuar como elemento vertical portante: recibir acciones de
los elementos conectados y transmitirlas de forma segura hacia la cimentación. Su
contribución concreta a la estabilidad lateral dependerá del sistema estructural.

**Dibujo rápido:**

```text
       viga / conexión superior (+6.000)
                    ───┬───
                       │
                    C-101       pieza física continua
                       │
                    ───┴───    BP-101, placa base separada
                    pedestal   objeto físico separado
```

## 2. Realidad física e identidad

**¿Qué objeto físico representa?**

Una pieza física fabricable y continua de acero que desempeña función de columna en
una estructura metálica. No representa toda posible «columna funcional» compuesta
por varios tramos y empalmes.

**¿Dónde empieza y termina?**

Empieza en el límite físico de su conexión con la placa base `BP-101` y termina en
el límite de una conexión superior concreta a cota `+6.000`. Los planos exactos de
corte y la pertenencia de soldaduras o chapas de extremo deberán precisarse al
estudiar las conexiones.

**¿Qué objetos cercanos quedan fuera?**

Las vigas que conectan con ella, la placa base, los pernos, el grout, el pedestal y
las conexiones. Que una pieza esté soldada o unida a `C-101` no implica por sí solo
que forme parte de la misma identidad.

**¿Por qué necesita —o no— identidad propia?** Necesita una identidad técnica interna
estable porque debe poder recibir relaciones, compararse entre revisiones y
corresponderse con objetos importados de diferentes programas. Esta identidad no
implica que la empresa le asigne un TAG. `C-101`, sus ejes y sus coordenadas son
formas de localizarla o mostrarla, pero no tienen por qué constituir su identidad
interna.

**¿Qué puede cambiar sin que deje de ser la misma ocurrencia?**

Dentro de una misma línea de diseño pueden cambiar el perfil, el material, el
placement, las conexiones y las acciones relacionadas, siempre que el equipo siga
reconociendo la misma intención estructural. Cada revisión conserva el estado
utilizado en ese momento. Dividir, fusionar, copiar a otra posición o sustituir su
función puede exigir identidades nuevas y relaciones de derivación.

**¿De quién depende su lifecycle?**

Para esta iteración, `C-101` es una ocurrencia de diseño cuyo estado pertenece a una
revisión del modelo físico. Se propone que `ST-101`, la estructura identificada por
la empresa, actúe como agregado de pertenencia primaria de la columna. Debe
contrastarse si también controla su lifecycle. La pieza fabricada, la instalación y
el activo operativo quedan fuera del alcance inicial, aunque podrán relacionarse con
una revisión de `C-101` en el futuro.

## 3. Ocurrencia, tipo, clasificación y propiedades

| Concepto | Respuesta del ejemplo |
|---|---|
| Ocurrencia concreta | C-101 |
| Tipo reutilizable posible | `ColumnType CT-01`, opcional y con alcance/procedencia conocidos. Puede venir definido por el modelo importado y agrupar intención común; no equivale al perfil HEB 200 ni a una plantilla de creación. Su contenido y política de overrides quedan abiertos. |
| Perfil o sección | HEB 200|
| Clasificaciones externas | Pendiente. Deben conservarse separadas del tipo y pueden coexistir varias. |
| Propiedades esenciales | Identidad interna y naturaleza de la ocurrencia física. Perfil, longitud, material y placement describen su estado en una revisión, no su identidad inmutable. |
| Propiedades variables por fase | Pendiente de validar; podrían variar estado, geometría, perfil, material, conexiones y referencias de fuente, conservando la revisión correspondiente. |

**¿Qué términos estabas mezclando antes de hacer esta separación?**

Inicialmente se podían confundir `columna`, perfil HEB 200, tipo reutilizable y
plantilla de creación. Se adopta provisionalmente que el dominio permita almacenar
un tipo cuando la fuente lo declare, sin hacerlo obligatorio ni inferirlo solo porque
varias ocurrencias compartan propiedades.

## 4. Jerarquías y relaciones

| Pregunta | Respuesta |
|---|---|
| ¿Quién posee el elemento? | Propuesta: `ST-101` como agregado estructural dentro de una revisión del modelo físico. Falta validar qué debe ocurrir al mover o eliminar la estructura. |
| ¿Dónde está contenido espacialmente? | Planta/área pendiente; se localiza además mediante alineaciones, ejes, cotas y coordenadas, sin convertirlas en ownership. |
| ¿A qué estructura pertenece? | A la estructura o pipe rack empresarialmente identificado como `ST-101`. |
| ¿A qué sistemas funcionales pertenece? | Pendiente; podría participar en sistemas gravitatorios o de estabilidad distintos de `ST-101`. |
| ¿De qué assembly o conjunto forma parte? | Posiblemente de un pórtico o módulo dentro de `ST-101`; queda por comprobar si ese conjunto controla lifecycle o solo composición. |
| ¿Qué partes posee? | En este ejemplo simplificado, ninguna con identidad separada; la placa base y sus componentes de unión quedan fuera de `C-101`. Pendiente de validar para casos con empalmes o chapas integradas. |
| ¿Con qué se conecta? | Con otros perfiles y con la placa base |
| ¿Sobre qué apoya o qué soporta? | soporta las cargas provenientes del resto de la estructura. Apoya sobre la placa base de su cimentación|

**Mapa sin utilizar una relación `parent` para todo:**

```text
PhysicalModelRevision R03
└── Structure ST-101                    identidad reconocida por la empresa
    └── contiene/compone ──► C-101      identidad técnica interna

Área / unidad de planta ──contiene espacialmente──► C-101
Ejes + cota + coordenadas ──localizan─────────────► C-101
Sistema resistente ────────agrupa funcionalmente─► C-101
Modelo externo/revisión ───referencia─────────────► C-101
```

**Propuesta provisional sobre identidad y pertenencia:**

La empresa identifica `ST-101` como unidad estructural, pero el dominio asigna a
`C-101` una identidad interna sin exigir un TAG corporativo. La columna pertenece
primariamente a `ST-101` y conserva referencias a los objetos que la representan en
cada modelo importado. Los ejes y coordenadas son localizadores sujetos a cambio, no
la clave definitiva de identidad.

**Preguntas concretas para debatir:**

1. Si una columna cambia de eje o coordenadas pero mantiene su función dentro de
   `ST-101`, ¿queremos reconocerla como la misma columna?
2. Si una columna pasa de `ST-101` a `ST-102`, ¿se ha movido el mismo elemento o debe
   crearse una nueva ocurrencia relacionada con la anterior?
3. Al eliminar o sustituir `ST-101`, ¿deben desaparecer también sus columnas o
   conservarse temporalmente como elementos sin estructura asignada?
4. Si STAAD, SAP2000 y un modelo BIM utilizan IDs diferentes, ¿quién o qué regla
   confirma que representan la misma columna?
5. ¿Puede una columna pertenecer primariamente a una sola estructura y participar a
   la vez en varios sistemas funcionales?
6. ¿Qué referencia debería ver una persona: un código local, la pareja
   `ST-101 + ejes/cota`, o una denominación generada por el sistema?

## 5. Placement, geometría y material

**Sistema global o de proyecto:** Cada revisión importada —proceda de STAAD, Tekla,
SP3D u otra aplicación— debe declarar sus unidades, origen, orientación y, cuando
exista, sistema de referencia. El repositorio conserva esos datos de fuente y la
transformación explícita utilizada para resolverlos en el sistema común del proyecto.

**Placement físico local:** Snapshot importado desde la aplicación que aporte esa
representación física. Debe permitir resolver la posición y orientación de `C-101`
mediante coordenadas y conservar, cuando exista, su referencia declarada a estructura,
ejes, alineaciones, offsets y cotas. Una referencia inferida por proximidad debe
distinguirse de una declarada por la fuente.

**Geometría editable:** No se edita inicialmente en la base de datos. La aplicación
autora de cada modelo conserva esa responsabilidad; una modificación llega al
repositorio mediante una nueva revisión importada. No se presupone una única
aplicación autora para todo el proyecto.

**Geometría derivada:** Coordenadas normalizadas, localizadores por ejes calculados,
envolventes, representaciones simplificadas o proyecciones analíticas obtenidas a
partir del snapshot importado. Deben conservar procedencia y no sobrescribir el dato
de origen.

**Comportamiento ante cambios de placement:** La base de datos no desplaza
automáticamente `C-101` cuando cambia un eje. Importa una nueva revisión de la fuente,
reconcilia la columna con su identidad anterior y registra si cambiaron eje,
coordenadas, orientación o relaciones. Si la fuente mueve el eje y la columna, ambos
cambios se reciben; si solo mueve uno, el repositorio conserva esa diferencia y
puede validarla o advertirla sin corregirla silenciosamente.

**Representaciones que podrían coexistir:**

La identidad y función de `C-101` —columna portante de `ST-101`— no se deducen
únicamente de su forma. Su perfil, material y geometría describen el estado de la
ocurrencia en una revisión. «Separar significado y geometría» no exige crear una
entidad adicional llamada `Semántica`: significa conservar explícitamente qué
elemento es, aunque cambie o se sustituya su representación geométrica.

| Representación | Propósito | Procedencia posible |
|---|---|---|
| Eje físico de referencia | Localizar la trayectoria y orientar el perfil cuando esa descripción exista | Declarado por la fuente o derivado con procedencia; no es el eje de un modelo analítico |
| Cuerpo 3D | Mostrar o consultar la forma ocupada por la pieza | Sólido original importado o generado desde perfil y trayectoria; indicar cuál es cuál |
| Envolvente | Selección, detección preliminar o visualización simplificada | Derivada del cuerpo; no reemplaza la geometría original |
| Detalle | Mostrar cortes, perforaciones u otros rasgos relevantes cuando la fuente los aporte | Representación de mayor detalle ligada a la fuente y revisión |

**Material o composición material:** En el caso sencillo, la pieza principal tiene
un material estructural asociado; su grado concreto queda pendiente de confirmar.
No se presupone que todos los elementos físicos del dominio tengan un único material:
otros pueden ser compuestos o requerir asignaciones por parte o región. Una forma 3D
con material permite representar muchos casos, pero no indica por sí sola si el
objeto es una columna, una zapata, un pedestal o parte de un equipo.

**Generalización provisional:** Los elementos físicos deben poder conservar una
geometría 3D general procedente de la fuente, incluso si no conocemos una definición
paramétrica. Cuando exista una descripción más informativa —por ejemplo, perfil y
trayectoria para `C-101`— también conviene conservarla. No se impone una única forma
geométrica a todas las familias, ni se reduce la definición del elemento a
`sólido 3D + material`. Los objetos no físicos, como cargas o ejes de replanteo,
requieren sus propios conceptos y no se fuerzan a esta generalización.

## 6. Conexiones físicas

| Extremo o zona | Objeto relacionado | Tipo de relación | Información propia de la relación |
|---|---|---|---|
| Inicio | Placa base | Conexion| |
| Final | Viga| | |
| Otra | No incluida en el caso simplificado | Pendiente | Corresponde al estudio de conexiones |

**¿La conexión es un objeto físico, una interfaz o ambas cosas?**
Respuesta inicial: objeto físico. Matiz provisional: una conexión puede incluir
componentes físicos —placas, pernos o soldaduras— y una relación o interfaz de
conectividad entre elementos. Su definición corresponde al trabajo de conexiones.

**¿Qué no debe confundirse con una condición analítica de extremo?**

La conexión física y sus componentes no equivalen directamente a un release, una
restricción o una rigidez de extremo. Estos últimos pertenecen a cada modelo
analítico y pueden idealizar de maneras diferentes la misma conexión física.

### Alcance de los ejemplos analíticos

Los modelos A y B siguientes son **escenarios pedagógicos de dos revisiones externas
hipotéticamente importadas**. Su propósito es comprobar si el dominio puede conservar
dos idealizaciones distintas, no afirmar que STAAD o Tekla exporten exactamente estos
objetos. Civil Domain no los propone generar ni los fusiona en una idealización
canónica. Sus detalles deberán validarse mediante intercambios reales.

## 7. Modelo analítico A

**Nombre y propósito:** Modelo analítico A para el análisis global de la estructura
`ST-101` mediante elementos lineales.

**Revisión física utilizada:** `PhysicalModelRevision R03` en este ejemplo. La
referencia a una revisión física concreta es el estado deseable para poder reproducir
y revisar la idealización. Si la fuente no permite conocerla, debe registrarse como
`UNKNOWN`; no se inventa y la alineación no podrá considerarse demostrada.

**Aplicación de origen:** Desconocida en el caso real. Para materializar el escenario
se supone una revisión externa denominada `STAAD S05`; no se afirma que un intercambio
real de STAAD tenga esta estructura o estos identificadores.

**Idealización del elemento:** Una barra 1D situada sobre el eje analítico adoptado
para la columna. En este modelo, el nodo inferior está en la cara superior de la
placa base y el nodo superior en la intersección de los ejes analíticos de columna y
viga. Esta idealización no modifica los límites ni la geometría de `C-101` física.

**Objetos analíticos necesarios:**

```text
AnalyticalModel A
├── AnalyticalNode N-INF
├── AnalyticalMember AM-C101
└── AnalyticalNode N-SUP

C-101 @ Physical R03 ──representada_en──► AM-C101 @ STAAD S05
```

**Nodos, ejes locales, offsets y extremos:** El nodo analítico inferior se sitúa,
para este modelo, en la intersección del eje analítico de la columna con la cara
superior de la placa base `BP-101`. Esta decisión fija su posición, pero no implica
por sí sola que el apoyo sea articulado, empotrado o elástico. La condición analítica
de apoyo se definirá separadamente dentro de este modelo.

El nodo superior se sitúa en la intersección de los ejes analíticos de la columna y
la viga conectada. Esta es una decisión propia del modelo A: otro modelo podría
terminar la barra en la cara física de la conexión y representar la distancia hasta
la intersección mediante un offset o una zona rígida.

El eje de `AM-C101` pasa por la línea centroidal del perfil HEB 200. Las diferencias
respecto a ejes de replanteo, caras de conexión o puntos de apoyo se conservan como
offsets o excentricidades explícitas del modelo analítico; no se altera la geometría
de la columna física para forzar la coincidencia.

**Correspondencia con el físico:** `1:1` en este caso simplificado: `C-101` no tiene
conexiones intermedias y se representa mediante una única barra `AM-C101`. Esta
cardinalidad es una decisión del modelo A, no una regla general para las columnas.

**Información que existe solo en este modelo:** Identificadores y coordenadas de los
nodos, eje analítico, orientación local y, si la fuente los aporta, offsets, releases
y restricciones. Son decisiones de la idealización supuesta, no propiedades de la
columna física. La disponibilidad real de cada dato deberá comprobarse.

### Qué demuestra el caso A y cómo se generaliza

El caso concreto no pretende definir la forma universal de analizar una columna.
Sirve como prueba para separar tres planos que el dominio debe conservar:

1. La ocurrencia física y la revisión de su geometría y propiedades.
2. Cada modelo analítico, con propósito, procedencia y revisión propios.
3. La correspondencia explícita entre objetos físicos y analíticos.

La relación físico–analítica no puede reducirse a un único `analyticalId` guardado
en la columna. Debe admitir varios modelos simultáneos y cardinalidades `1:1`, `1:N`,
`N:1` y `N:M`. También debe declarar qué revisión física se idealizó, qué parte o
zona del físico cubre la correspondencia, cómo se obtuvo y si continúa vigente.

La alineación con el físico no significa igualdad geométrica. Significa que la
idealización es trazable a una revisión física concreta y que sus diferencias —eje,
extremos, offsets, simplificaciones o agrupaciones— son explícitas y justificables
para el propósito del modelo. Cuando cambia la revisión física, el modelo analítico
anterior no se modifica: conserva su trazabilidad y puede marcarse como pendiente de
revisión, compatible o desactualizado según el impacto del cambio.

### Quién crea o actualiza una revisión analítica

En el alcance inicial, Civil Domain no edita el modelo analítico externo. Lo modifica
el ingeniero o proceso responsable dentro de su aplicación autora y una importación
posterior registra una nueva revisión. La revisión anterior permanece inmutable.

La proyección normalizada utilizada para consultar y comparar no es por sí sola un
nuevo modelo de cálculo. En el futuro podría existir un transformador que generase
una topología analítica destinada a un flujo concreto. Solo entonces existiría otro
modelo analítico, con procedencia `GENERATED`, reglas identificadas y revisiones
propias; no sustituiría silenciosamente a los modelos importados.

Tener varios modelos analíticos no implica necesariamente tener varios programas:

- dos aplicaciones distintas pueden aportar modelos analíticos diferentes;
- una misma aplicación puede mantener varios modelos con propósitos o ciclos de vida
  independientes;
- hipótesis, casos y combinaciones dentro de una misma topología no obligan por sí
  solos a crear modelos analíticos separados.

Se considera otro modelo cuando tiene identidad, propósito, topología o ciclo de
revisión independiente, no simplemente porque cambie una combinación de cargas.

## 8. Modelo analítico B

**Nombre y propósito:** Ejemplo pedagógico de un modelo analítico B importado desde
un modelo de análisis de Tekla para el cálculo global de `ST-101`. No se afirma aún
que este sea el comportamiento real de un intercambio concreto.

**Por qué necesita una idealización diferente:** La fuente ha introducido un nodo de
cálculo intermedio en la cota `+3.000`, aunque no exista allí una discontinuidad de
la pieza física, para aplicar una carga o discretizar el análisis.

**Idealización del elemento:** Dos barras 1D consecutivas representan la misma
columna física continua.

**Objetos analíticos necesarios:**

```text
AnalyticalModel B
├── AnalyticalNode NB-INF
├── AnalyticalMember AM-C101-1
├── AnalyticalNode NB-MID   (+3.000, sin corte físico)
├── AnalyticalMember AM-C101-2
└── AnalyticalNode NB-SUP

C-101 @ Physical R03 ──representada_en──►
    {AM-C101-1, AM-C101-2} @ Tekla T12
```

**Correspondencia con el físico:** `1:N`; una ocurrencia física se representa mediante
dos objetos analíticos dentro de la revisión del modelo B.

**Diferencias relevantes respecto al modelo A:** El modelo A utiliza una barra y el
modelo B dos. Ambos pueden estar alineados con la misma revisión física porque el
nodo intermedio de B es una decisión analítica explícita y no afirma que la columna
física esté dividida.

### Lenguaje común frente a modelo analítico canónico

El dominio sí necesita conceptos internos comunes para consultar y relacionar la
información: modelo, revisión, nodo, miembro, representación, procedencia y
correspondencia físico–analítica. Esto constituye un **núcleo semántico común**.

No se propone todavía un **modelo analítico maestro** que transforme todos los
modelos externos en una única representación considerada completa, editable y apta
para volver a exportarse sin pérdida a cualquier aplicación. Esa ambición exigiría
resolver de antemano diferencias de topología, offsets, releases, restricciones,
ejes locales, mallas y capacidades específicas de cada herramienta.

Para la primera etapa se propone conservar simultáneamente:

1. El snapshot fiel de cada revisión externa y su procedencia.
2. Una proyección normalizada mínima para identificar, consultar y comparar los
   conceptos que entendemos con suficiente certeza.
3. La correspondencia con la revisión física y las pérdidas, aproximaciones o datos
   no interpretados.

La proyección normalizada no sustituye al original ni promete round-trip. Un modelo
canónico generado podría añadirse más adelante para un flujo concreto —por ejemplo,
crear un modelo global destinado a Footings— cuando se conozcan las fuentes, la
semántica necesaria y los criterios de aceptación.

Los ejemplos A y B permanecen en la capa de modelos importados:

```text
Physical C-101 @ R03
├── Mapping M-A ──► STAAD S05 / una barra
└── Mapping M-B ──► Tekla T12 / dos barras
                         │
                         ▼
                proyección común parcial
       identidad, tipo de objeto, extremos,
      sección y correspondencia
```

La proyección inferior no elige entre A y B, no fusiona sus topologías y no se
considera un tercer modelo analítico. Solo expone el subconjunto de información que
el dominio puede interpretar y comparar con seguridad.

No se presupone que esta proyección sea una entidad persistida. Puede ser una vista
de consulta o el resultado de adaptadores de importación. Solo se normalizarán los
campos exigidos por casos de uso concretos; el resto seguirá ligado al snapshot de
fuente.

### Materialización de la correspondencia y la alineación

La correspondencia histórica y la evaluación de alineación son conceptos distintos:

```text
PhysicalAnalyticalMapping M-A
├── physical: C-101 @ Physical R03
├── analytical: Member 25 @ STAAD S05
├── coverage: WHOLE_ELEMENT
├── cardinality: 1:1
└── evidence: referencia declarada o reconciliación confirmada

AlignmentAssessment AA-01
├── mapping: M-A
├── comparedAgainst: C-101 @ Physical R04
├── status: REVIEW_REQUIRED
└── reasons: cambió el perfil físico de HEB 200 a HEB 240
```

`M-A` no se reescribe al aparecer `R04`: continúa documentando que `S05` representa
la revisión física `R03`. La evaluación `AA-01` expresa si esa representación sigue
siendo utilizable frente a una revisión posterior. Si STAAD se actualiza, se importa
`S06` y se crea otra correspondencia hacia `C-101 @ R04`.

### Cómo consultar las representaciones analíticas de una entidad física

Los modelos analíticos no son hijos ni partes propiedad de `C-101`. Son agregados
independientes que pueden representar simultáneamente muchos elementos físicos. La
navegación se realiza atravesando la correspondencia:

```text
PhysicalElement C-101
└── PhysicalElementRevision R03
    ├── Mapping M-A
    │   └── AnalyticalModelRevision STAAD S05
    │       └── participante: AnalyticalObject Member 25
    └── Mapping M-B
        └── AnalyticalModelRevision Tekla T12
            ├── participante: AnalyticalObject Member 70
            └── participante: AnalyticalObject Member 71
```

Para obtener todas las representaciones históricas se buscan mappings que incluyan
cualquier revisión de `C-101`. Para saber cuáles corresponden a `R03` se filtra esa
revisión exacta. Para saber cuáles siguen alineadas con la revisión física vigente se
consulta además la evaluación de alineación más reciente.

La consulta también funciona en sentido inverso: desde un miembro analítico puede
averiguarse qué elemento o conjunto de elementos físicos representa.

### Responsabilidad de cada concepto

| Concepto | Por qué hace falta |
|---|---|
| `PhysicalElement` | Mantiene la identidad estable de `C-101` a través del tiempo |
| `PhysicalElementRevision` | Congela perfil, material, geometría y placement utilizados por una idealización |
| `AnalyticalModel` | Agrupa una idealización con propósito y ciclo de vida propios; no pertenece a una sola columna |
| `AnalyticalModelRevision` | Permite reproducir exactamente la topología y datos usados en un cálculo |
| `AnalyticalObject` o snapshot | Representa el nodo, barra o superficie concreto dentro de una revisión analítica |
| `PhysicalAnalyticalMapping` | Resuelve la correspondencia potencialmente `1:1`, `1:N`, `N:1` o `N:M` y conserva cobertura, origen, evidencia y revisión física de base cuando sea conocida |
| `AlignmentAssessment` | Evalúa una correspondencia histórica frente a otra revisión física sin reescribir la historia |
| `ExternalObjectReference` | Conserva el identificador y contexto del objeto en la aplicación de origen |

`PhysicalAnalyticalMapping` se trata como una entidad asociativa porque la relación
tiene información y trazabilidad propias. Un simple enlace no podría explicar qué
revisiones relaciona, si cubre todo el elemento, cómo se obtuvo o si fue confirmado.

### Diseños más simples pero frágiles

| Diseño | Problema |
|---|---|
| `C-101.analyticalId` | Solo admite una representación y pierde modelo, revisión y cardinalidad |
| `AnalyticalObject.physicalId` | Puede cubrir varios objetos analíticos para un físico, pero no expresa bien `N:1` o `N:M` ni información conjunta del mapping |
| Lista JSON de IDs analíticos en `C-101` | Debilita integridad, consultas, versionado y explicación de cada emparejamiento |
| Nodos, offsets y releases dentro de `C-101` | Mezcla decisiones analíticas potencialmente contradictorias con la realidad física |
| Modelo analítico como hijo de la columna | Es falso: un modelo representa la estructura y contiene objetos asociados a muchas entidades físicas |
| Sobrescribir la revisión anterior | Impide reproducir cálculos y saber qué estado físico fue analizado |
| Un único `isAligned` en `C-101` | La alineación depende del modelo, la revisión comparada, el propósito y el aspecto evaluado |

## 9. Importación desde aplicaciones externas

El modelo físico puede proceder de STAAD, Tekla, SP3D y, en el futuro, de otras
aplicaciones. Algunas fuentes también pueden aportar una representación analítica.
Por tanto, el rol físico o analítico pertenece al modelo importado y a sus objetos,
no queda fijado de manera universal por el nombre de la aplicación.

Un identificador del programa de origen nunca sustituye a la identidad interna de
`C-101`. Se conserva como referencia externa, acompañada por la aplicación, el modelo
y la revisión que le dan contexto.

| Fuente candidata | Información física posible | Información analítica posible | Estabilidad de ID | Evidencia pendiente |
|---|---|---|---|---|
| STAAD | Por comprobar según intercambio | Sí | Desconocida | Documentación y prueba controlada |
| Tekla | Sí | Sí, según modelo/intercambio | Desconocida | Documentación y prueba controlada |
| SP3D | Sí | Por comprobar | Desconocida | Documentación y prueba controlada |
| SAP2000 u otras | Según aplicación/intercambio | Según aplicación/intercambio | Desconocida | Documentación y prueba controlada |

### Conceptos internos candidatos para la importación

| Concepto | Responsabilidad |
|---|---|
| `ExternalModelRevision` | Identifica una entrega concreta de un modelo externo y su contexto |
| `ExternalObjectReference` | Conserva el ID nativo dentro de aplicación, modelo y revisión |
| `ImportedObjectSnapshot` | Conserva lo que la fuente afirmó sobre el objeto en esa revisión |
| `IdentityMatch` | Explica por qué un snapshot se asocia —o no— con `C-101` |
| `SourcePlacement` | Conserva placement, unidades y sistema de coordenadas declarados |
| Transformación normalizada | Permite comparar la posición en el sistema común sin perder el original |

Hay dos reconciliaciones diferentes:

1. Determinar si dos snapshots de revisiones sucesivas de una misma fuente son el
   mismo objeto.
2. Determinar si objetos procedentes de fuentes distintas representan la misma
   ocurrencia de diseño `C-101`.

La segunda no debe resolverse automáticamente solo por proximidad geométrica o por
coincidencia de nombre. Puede combinar estructura, ejes, coordenadas, geometría,
perfil, conectividad y confirmación humana. Los estados candidatos son:
`NATIVE_ID`, `RULE_MATCH`, `CONFIRMED`, `AMBIGUOUS` y `NEW`. Un caso ambiguo no se
fusiona silenciosamente.

### Prueba mínima pendiente por cada aplicación

Exportar un modelo pequeño y repetir la exportación después de: no cambiar nada,
renombrar un elemento, moverlo, cambiar su perfil, copiarlo y eliminarlo/recrearlo.
Comparar identificadores, geometría y relaciones permitirá saber qué señales son
estables en cada fuente. Hasta realizar esta prueba, la estabilidad de sus IDs queda
declarada como desconocida.

### Alineación entre modelos externos

El objetivo operativo es que las distintas representaciones de una estructura estén
coordinadas, pero el repositorio no debe asumir que una herramienta es siempre la
fuente maestra ni modificar automáticamente los modelos externos. Debe conservar qué
revisión de cada fuente se comparó y contra qué revisión o hito de coordinación.

Una fecha anterior no basta para declarar que un modelo está desactualizado. Para
afirmar que está «por detrás» debe existir una dependencia conocida, una revisión de
referencia o un cambio aceptado que todavía no se haya incorporado. Si solo se detectan
diferencias sin conocer cuál es correcta, el estado es `INCONSISTENT`, no `OUTDATED`.

Estados provisionales de coordinación:

| Estado | Significado |
|---|---|
| `ALIGNED` | Las revisiones comparadas satisfacen las reglas de coordinación definidas |
| `OUTDATED` | La fuente no incorpora un cambio aceptado o una revisión de la que depende |
| `INCONSISTENT` | Existen diferencias, pero aún no se ha decidido cuál representa la intención vigente |
| `UNCHECKED` | Todavía no existe una comparación válida entre esas revisiones |
| `NOT_APPLICABLE` | La fuente no pretende representar ese dato o elemento |

La alineación debe poder evaluarse por aspecto —identidad, placement, geometría,
perfil, material, conectividad o idealización analítica— porque dos modelos pueden
coincidir en la posición de `C-101` y diferir legítimamente en su representación.

**Decisión pendiente para el equipo:** definir por proyecto y por familia de datos
qué fuente propone el cambio, quién lo acepta y cuál es la revisión de coordinación.
No se presupone todavía un propietario universal del modelo físico.

La matriz siguiente no se considera resuelta por el ejemplo ficticio. `PV` significa
«pendiente de verificar con un intercambio real»; no se atribuyen capacidades a una
aplicación sin evidencia.

| Dato normalizado | STAAD | Tekla | SP3D | Concepto interno propuesto |
|---|---|---|---|---|
| Modelo/revisión de origen | PV | PV | PV | `ExternalModelRevision` |
| ID externo | PV | PV | PV | `ExternalObjectReference` |
| Nodos o geometría | PV | PV | PV | Snapshot físico o analítico con procedencia |
| Sección y material | PV | PV | PV | Asignaciones normalizadas y dato original |
| Ejes locales | PV | PV | PV | Sistema local de la representación correspondiente |
| Offsets/excentricidades | PV | PV | PV | Propiedad física o analítica según semántica de fuente |
| Releases/rigideces | PV | PV | PV | Propiedad del modelo analítico, no de la columna física |
| Conexiones/apoyos | PV | PV | PV | Relación física o condición analítica diferenciadas |
| Cargas | PV | PV | PV | Acción/asignación dentro de un modelo analítico |

**Ejemplo de traducción exacta:** Pendiente de inspeccionar un intercambio real. Como
regla, copiar el identificador de fuente o una coordenada sin cambiar su significado
es una preservación fiel, no una prueba de que todo el modelo se haya traducido.

**Ejemplo de normalización:** Si una fuente declara `6000 mm`, exponer `6 m` para
comparar, conservando `6000 mm`, la unidad declarada y la regla de conversión. Es un
ejemplo conceptual; no atribuye ese formato a ninguna aplicación.

**Ejemplo de aproximación con pérdida:** Reducir un cuerpo complejo a una línea o
envolvente. Debe etiquetarse como derivación aproximada y nunca reemplazar el cuerpo
original. La pérdida concreta por adaptador sigue pendiente de prueba.

**Ejemplo que declararíamos no soportado:** Cualquier condición analítica de una
fuente cuya semántica no sepamos interpretar. Se conserva el original y se informa
del límite; no se convierte en un release genérico por similitud de nombre.

## 10. Resultados

**¿A qué modelo y ejecución pertenecen?** En el ejemplo, a una ejecución concreta de
`STAAD S05` o `Tekla T12`, además de su caso o combinación. No son resultados
intrínsecos de `C-101`.

**¿Qué resultados se asocian a objetos analíticos?** Esfuerzos, desplazamientos o
reacciones se asocian a nodos, barras y demás objetos de la revisión y ejecución que
los produjo. La forma exacta depende del intercambio real.

**¿Qué resumen tendría sentido proyectar sobre el elemento físico?** Una consulta
podría mostrar los esfuerzos o una verificación relevante para `C-101` atravesando
el mapping. Si B la representa mediante dos barras, el resumen debe declarar cómo se
agregaron o seleccionaron sus resultados; no se copia un número desnudo a la columna.

**¿Qué procedencia debe conservarse?** Modelo, revisión, ejecución, caso/combinación,
objeto analítico, unidades, mapping y regla de resumen utilizada.

## 11. Conclusión para la reunión

### Mapa mental del caso

```text
ST-101 (estructura)
└── C-101 (identidad física de diseño)
    ├── R03: perfil, material, placement y geometría de la pieza continua
    ├── relaciones físicas: BP-101, viga y conexiones (objetos separados)
    ├── M-A: C-101 R03 ↔ una barra de STAAD S05 (ejemplo 1:1)
    └── M-B: C-101 R03 ↔ dos barras de Tekla T12 (ejemplo 1:N)
```

STAAD S05 y Tekla T12 son modelos analíticos independientes. Sus nodos, offsets,
condiciones y resultados permanecen en cada modelo. Los mappings permiten navegar
en ambos sentidos; una evaluación aparte indica si siguen siendo adecuados frente
a una revisión física posterior.

### Explicación breve para presentar

1. **Objeto físico:** `C-101` es una columna continua de `ST-101`. Su identidad no
   depende del perfil ni del sólido que la dibuja; ambos pueden cambiar por revisión.
2. **Dos idealizaciones:** un modelo analítico supuesto la representa con una barra
   y otro con dos. La división analítica no divide la pieza física.
3. **Puente:** `PhysicalAnalyticalMapping` relaciona participantes de revisiones
   concretas, admite `1:N` y conserva cobertura y evidencia; ningún modelo analítico
   es hijo de la columna.
4. **Cambio:** si el físico pasa a R04, los modelos anteriores no se reescriben.
   Se evalúa si deben revisarse y el responsable actualiza su aplicación autora.
5. **Límite inicial:** conservar fuentes y normalizar solo lo necesario para casos
   de uso; no inventar una topología analítica maestra ni prometer round-trip.

### Hasta cinco conceptos candidatos

1. `PhysicalElement` y su revisión: identidad de `C-101` y estado físico reproducible.
2. `AnalyticalModel` y su revisión: identidad, propósito y estado de cada modelo.
3. `AnalyticalObject`: nodo, barra, superficie u otro objeto dentro de esa revisión.
4. `PhysicalAnalyticalMapping`: correspondencia trazable `1:1`, `1:N`, `N:1` o
   `N:M` entre objetos de revisiones concretas.
5. `AlignmentAssessment`: evaluación separada de si una representación sigue siendo
   adecuada frente a una revisión física posterior.

La referencia externa del objeto y el snapshot de importación siguen siendo
necesarios para la procedencia, aunque no figuren entre estos cinco focos de debate.

### Simplificación inicial que aceptarías

Conservar los snapshots de fuente y las correspondencias. Normalizar de forma
incremental únicamente los datos requeridos por consultas concretas. No exigir
round-trip, persistir una proyección común completa ni generar un modelo analítico
maestro.

### Diseño que consideras frágil

Guardar un único `analyticalId` en `C-101`, fusionar los modelos externos en una sola
topología o copiar offsets, releases y nodos como si fueran propiedades físicas de
la columna.

### Tres preguntas para el equipo

1. ¿Qué consultas comunes necesitamos resolver inicialmente sobre todos los modelos?
2. ¿Qué datos de cada fuente comprendemos con suficiente certeza para normalizarlos?
3. ¿Qué criterio distingue una nueva revisión de un modelo analítico diferente?

### Lo que necesitas investigar después

Intercambios reales y estabilidad de identificadores en STAAD, Tekla y SP3D;
matriz de capacidades y pérdidas por fuente; criterios para evaluar si un cambio
físico afecta a cada idealización analítica.
