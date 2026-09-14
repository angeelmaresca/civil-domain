# Ficha — Zapata

> **Status:** DRAFT
> **Editable:** sí; ficha individual de Luis para revisión dentro del alcance de `WORKING_SET.md`
> **Document owner:** Luis
> **Canonical for:** —
> **Sources:** [Primera iteración](FIRST_ITERATION.md), entrevistas con Luis del 2026-09-11 y 2026-09-14
> **Supersedes:** —
> **Last reviewed:** 2026-09-14

## Alcance y lectura

Borrador de la aportación de Luis, pendiente de su corrección y del contraste con
el equipo. Recoge sus criterios de dominio y experiencia; no establece reglas
normativas ni decisiones aprobadas. El encargo y la batería común pertenecen a
[FIRST_ITERATION.md](FIRST_ITERATION.md). Las soluciones de Footings V2 no se
trasladan automáticamente al dominio civil. La ampliación del 14 de septiembre
incorpora encepados, métodos de análisis y una propuesta transversal de validación
técnica para los elementos del ecosistema TR.

## 1. Ejemplo y significado

`F-101` es una zapata del conjunto de cimentación `CF-01`, situado en una unidad
de planta. Recibe cargas de uno o varios apoyos y las transmite al terreno mediante
una cimentación superficial. Puede recibir pedestales, una placa base, el skid de
un equipo directamente o acciones superficiales. La función de cimentación, y no
solo la forma de un sólido de hormigón, define el concepto.

```text
Estructura o equipo
      │ transmite acciones mediante sus apoyos
      ▼
Pedestal(es), placa base o apoyo directo del equipo
      │ apoyo / conexión; no implica composición
      ▼
Zapata F-101 = cuerpo de hormigón + armadura, cuando existe
      │ transmite acciones a través de su base
      ▼
Capas opcionales externas: limpieza, geotextil u otras
      ▼
Terreno
```

La zapata no incluye pedestales ni hormigón de limpieza. Puede ser de hormigón
armado o en masa. Según la explicación de Luis, la zapata distribuye las cargas
con trabajo a flexión, mientras que el pedestal se reconoce por su comportamiento
tipo columna y su armado longitudinal vertical con estribos. Este criterio es una
descripción de trabajo, no una regla exhaustiva para clasificar todos los casos.
Un bloque de cimentación de bomba que sobresale del pavimento puede seguir siendo
íntegramente zapata, sin inventar un pedestal separado.

## 2. Identidad, pertenencia y tipo

| Aspecto | Criterio de Luis para revisión |
|---|---|
| Identidad | Cambiar dimensiones, canto o armado mantiene la misma zapata, con una nueva revisión. |
| Fusión | Al combinar dos zapatas, las anteriores se sustituyen por otra con identidad nueva. Conservar el historial de esa sustitución queda fuera del alcance de esta ficha. |
| Pertenencia | Cada zapata pertenece a un conjunto de cimentación. Si ese conjunto desaparece del diseño, sus zapatas desaparecen con él. |
| Apoyo funcional | Puede dar apoyo a varias estructuras o equipos; esto no equivale a pertenecer exclusivamente a uno de ellos. |
| Identificador | Se propone un código único en el universo TR que permita reconocer proyecto, unidad, conjunto y numeración. Debe conservarse en intercambios. |
| Reasignación | Al cambiar de unidad o conjunto cambia el código, pero sigue siendo el mismo objeto. Queda por concretar cómo reconocer esa continuidad entre aplicaciones. |
| Tipo compartido | Misma geometría, materiales y armado, incluido el orden de capas. La orientación y el número de soportes no distinguen el tipo según Luis; es una propuesta controvertida que requiere debate. |

Una diferencia en la resistencia del hormigón distingue el tipo. Luis señala que,
en el escenario discutido de zapatas por lo demás idénticas, sería una situación
anómala o de obra que merecería atención particular; no se generaliza esa valoración
a cualquier uso de hormigones distintos.

«Aislada» y «combinada» son variantes del concepto zapata. La existencia de uno o
varios apoyos y la forma del contorno no cambian por sí solas su naturaleza.

## 3. Geometría, posición y materiales

La zapata admite formas parametrizadas y contornos libres por coordenadas. Ejemplos
aportados por Luis, ilustrativos y no correspondientes todos a `F-101`:

| Forma | Dimensiones indicativas | Profundidad de cara superior respecto al pavimento |
|---|---|---|
| Rectangular | 7 × 3 m; canto 1 m | 0,50 m |
| Octogonal | Ancho 7 m; canto 0,80 m | 1,50 m |
| Libre, por ejemplo en L | Contorno por coordenadas; canto 0,70 m | 1,20 m |

La geometría puede incluir huecos, recrecidos y zonas de distinto espesor. Luis
menciona también mayores cantos perimetrales. El canto constante es frecuente,
pero no una condición de identidad. El significado exacto de «ancho» del octógono
queda por precisar cuando se formalice su parametrización.

El origen es el punto desde el que se define el contorno: normalmente el centro,
pero puede elegirse otro. La posición puede expresarse en coordenadas locales del
conjunto o globales de planta, con orientación angular respecto al sistema usado.
También se describe la profundidad de la cara superior respecto al pavimento.
El convenio de ejes debe ser explícito; Luis utiliza X y Z en planta e Y vertical
en su ejemplo. Mencionó la rotación alrededor del centro: la relación exacta entre
ese centro y un origen alternativo queda pendiente, sin imponer que coincidan.

La geometría puede proceder de Footings V2 u otra herramienta, por definición o
dimensionamiento. El dominio debe describirla independientemente de su origen;
los algoritmos de dimensionamiento y comprobación pertenecen a las aplicaciones.

El cuerpo es de hormigón. Cuando existe armadura, forma parte de la zapata y debe
describirse con su material y disposición. Luis destaca:

- armadura inferior y superior en las dos direcciones locales de planta;
- orden de superposición X sobre Z o Z sobre X, independiente abajo y arriba;
- estribos perimetrales en los casos que los requieran;
- armadura base y refuerzos localizados, incluidos cortante y punzonamiento.

Invertir el orden de capas distingue el tipo, aunque el resto del armado sea igual.
La disposición habitual inversa entre cara inferior y superior no es obligatoria.

## 4. Terreno y condiciones de emplazamiento

El hormigón de limpieza, el geotextil y los tratamientos superficiales son externos
y opcionales. Luis señala que pueden afectar al rozamiento utilizado en las
comprobaciones y al recubrimiento requerido; no cambian la identidad de la zapata.
Su tratamiento detallado no se desarrolla aquí.

Se propone reunir en unas **condiciones de emplazamiento** el perfil geotécnico,
el nivel freático y la cota de pavimento aplicables. La información procede del
proyecto y puede organizarse por zonas o perfiles. La asignación puede seguir
zonificación, cercanía o interpolación, según la regla que se adopte.

**Varias zapatas pueden compartir condiciones, pero la asignación debe resolverse
para cada zapata mediante una regla explícita.** Es probable que las de un módulo
compartan suelo; pertenecer al módulo no sustituye esa asignación individual.

Luis describe capacidades geotécnicas asociadas a los perfiles y utilizadas en
los cálculos. Queda para discusión qué información corresponde al perfil, a las
condiciones aplicables y a los resultados de una evaluación concreta; esta ficha
no fija una capacidad como propiedad intrínseca de la zapata.

## 5. Representaciones, cálculos y comprobaciones

Una zapata física puede tener un sólido de maqueta, contornos en planta, alzados,
secciones, detalles de armado y tablas de dimensiones para formas regulares.
Estas representaciones no crean zapatas distintas.

Se distinguen el método y sus hipótesis, la representación matemática y la
herramienta que ejecuta el análisis. Un análisis no requiere necesariamente una
malla de elementos finitos ni proceder de una aplicación externa.

Se recogen las siguientes alternativas, aplicables según el propósito del análisis:

| Alternativa | Correspondencia con la zapata física |
|---|---|
| Apoyo equivalente con muelles | Representación simplificada mediante objetos de apoyo y rigideces equivalentes; su formulación concreta queda pendiente. |
| Modelo de elementos finitos de placas con muelles | Las placas representan la zapata; los muelles representan la respuesta del terreno. Una zapata corresponde a múltiples objetos analíticos. |
| Formulación de sólido rígido | Análisis manual o algorítmico, por ejemplo mediante reparto por inercias o rigideces según la formulación adoptada; no exige una malla. |
| Formulación con hipótesis de plasticidad | Análisis manual o algorítmico con una consideración de distribución plástica del suelo; sus hipótesis deben identificarse. |
| Flexión o bielas y tirantes en encepados | Métodos que condicionan el análisis y la disposición del armado del encepado. |

Los modelos de elementos finitos también son modelos analíticos. Pueden utilizarse
para estudiar la interacción terreno–cimiento y obtener resultados para las
comprobaciones. **Una misma zapata puede vincularse a varios modelos de cálculo;
cada comprobación se vincula a la zapata y al modelo del que procede.** Luis pide
conservar un histórico de comprobaciones, distinto del historial del objeto físico
que se dejó fuera de esta ficha. La vinculación necesaria para la validación se
describe en el apartado 5.2.

El apoyo equivalente puede servir para representar la cimentación en un modelo
global de estructura; no agota las formas de analizar y comprobar la cimentación.
STAAD, SAP2000 u otro software de elementos finitos son posibles herramientas,
al igual que un algoritmo implementado en Footings V2 u otra aplicación. Los
análisis manuales y algorítmicos requieren la misma trazabilidad hacia el elemento
y sus comprobaciones que los de elementos finitos. Distintos análisis y ámbitos
de trabajo pueden aportar comprobaciones coexistentes sobre el mismo elemento.

### 5.1. Encepados y elementos de cimentación profunda

Luis propone debatir un concepto general compartido por **zapatas, losas y
encepados**, distinguiendo sus relaciones de apoyo con el terreno superficial,
los elementos profundos o ambos. No se fija todavía el nombre de ese concepto ni
una jerarquía canónica. «Cimentación superficial» no cubriría por sí sola todo
este alcance ampliado.

El encepado comprende su cuerpo de hormigón y su armadura. Pilotes, micropilotes,
barretas y los demás elementos profundos con los que interacciona son objetos
separados. Luis menciona también anclajes entre los elementos a considerar; sus
funciones y relaciones particulares quedan para el contraste del equipo.

La separación tiene una expresión constructiva: los pilotes suelen ejecutarse
primero, con un plano de implantación propio que identifica cada uno y sus
coordenadas; posteriormente se construye el encepado. Corresponden a partidas de
trabajo diferentes. Los pilotes pueden conservarse y relacionarse con un encepado
sustituto si se elimina o rediseña el original.

Según la experiencia descrita por Luis, los pilotes suelen ser elementos
cilíndricos que alcanzan estratos competentes a profundidades significativas
(por ejemplo 15 o 20 m, o más). Son ejemplos, no límites del dominio. Su definición
se establece en proyecto y sus capacidades proceden del informe geotécnico o de
cálculos basados en los estratos. Cada pilote tiene una asignación geotécnica
mediante una regla, pudiendo compartir perfil con otros. No se impone un perfil
único por encepado: una losa pilotada de 30 × 20 m podría encontrar el estrato
rocoso a 15 m en una zona y a 20 m en otra, con capacidades y comportamientos
diferentes.

La geometría del encepado está muy condicionada por la disposición de los pilotes:

- disposiciones normalizadas, por ejemplo 2 × 2 o 2 × 3, con separaciones entre
  pilotes y distancias al borde que condicionan el contorno;
- otras configuraciones, como un encepado octogonal de cinco pilotes;
- definición general mediante un polígono exterior y una lista de pilotes con
  sus coordenadas, admitiendo distribuciones no regulares.

Las separaciones y distancias mínimas responden a los criterios aplicables y no
se fijan numéricamente en esta ficha. La disposición normalizada genera posiciones
iniciales que después pueden ajustarse individualmente para reflejar la ejecución.
Se conservan por separado la posición prevista y la ejecutada de cada pilote
para comparar desviaciones. Un mismo encepado puede relacionarse con pilotes de
distinto diámetro, longitud, material o procedimiento, e incluso combinar
tecnologías; Luis considera estos casos muy excepcionales.

Los tirantes entre cabezas de pilotes y las vigas embebidas forman parte del
encepado. Su disposición depende del modelo elegido, por flexión o por bielas y
tirantes. Cambiar ese modelo y el armado conserva la identidad del encepado con
una revisión. También se conserva la identidad si las desviaciones de pilotes
obligan a modificar geometría o armado, pero se pierde la pertenencia al tipo
anterior. Según la propuesta de Luis, compartir tipo exige igualdad de geometría,
materiales y armado, además de disposición y tipos de pilotes relacionados.

La participación del terreno es una hipótesis de cálculo. Luis describe como
habitual atribuir la transmisión a los pilotes sin colaboración de la base; un
análisis particular puede incluirla, como en una losa pilotada. Esta elección puede
establecerse en proyecto o para justificar un caso con nuevas cargas o condiciones.
No cambia por sí sola la identidad física del encepado.

### 5.2. Comprobaciones y validación técnica — propuesta transversal

Luis propone aplicar a cualquier elemento físico del ecosistema TR la separación
entre **requisitos de comprobación**, **evidencias de análisis** y **validación
final del elemento**. El proyecto define los requisitos, diferenciados para
zapatas, losas y encepados; el número de comprobaciones no es fijo para todos.

Como ejemplos de la práctica de zapatas, Luis enumera presión en la base, vuelco,
deslizamiento, levantamiento, porcentaje comprimido, subpresión, flexión en las
cuatro direcciones principales, cortante al menos en dos direcciones principales,
punzonamiento y fisuración. Se normalizan aquí los términos de la explicación
oral para que Luis los revise; esta lista no constituye un catálogo normativo
obligatorio ni exhaustivo.

Una comprobación obtiene sus datos de un modelo matemático o de análisis: por
ejemplo, la presión en la base puede evaluarse mediante un algoritmo de sólido
rígido o mediante elementos finitos. Ambos resultados pueden coexistir. Obtener
un resultado favorable no equivale por sí solo a validar el elemento.

La propuesta acordada con Luis durante la entrevista es:

| Aspecto | Criterio propuesto para el equipo |
|---|---|
| Responsable | Siempre debe haber un técnico responsable que apruebe finalmente los cálculos automáticos y la suficiencia de las evidencias. |
| Base de la aprobación | El técnico selecciona expresamente los resultados aceptados e identifica los sustituidos. |
| Trazabilidad | Se registra quién valida, cuándo y sobre qué revisión del elemento y de sus datos, junto con los análisis y resultados que sustentan su decisión. |
| No aplicable | El técnico puede declarar una comprobación no aplicable, dejando registrada la justificación. |
| Cambios físicos o de entrada | Cambios en geometría, cargas o condiciones del terreno dejan la validación pendiente de revisión. |
| Cambios de análisis | Cambiar el modelo o sus hipótesis también requiere revisar la validación, aunque el objeto físico no cambie. |
| Nueva consideración | Si un cálculo B incorpora una consideración importante omitida en A, el elemento queda pendiente de validación y B pasa a ser la nueva referencia para lo afectado. |
| Sustitución parcial | B sustituye únicamente las comprobaciones afectadas. El técnico determina cuáles son y cuáles conserva de A; después valida el conjunto resultante. |

Ejemplo: A sustentó una validación; B aborda una consideración antes omitida.
Las comprobaciones anteriores conservan su existencia histórica, pero las
afectadas dejan de sustentar la aprobación. Las no afectadas pueden mantenerse
si así lo determina el técnico. La validación se recupera cuando este aprueba
las evidencias resultantes, no simplemente al ejecutar B.

La conversación de A y B se resolvió bajo el supuesto de una nueva consideración
relevante; no se ha definido una política separada para pruebas exploratorias
sin efecto sobre la base aceptada. Tampoco se propone aún un campo concreto,
un catálogo formal de estados o un mecanismo de firma: lo requerido es que la
suficiencia y la aprobación humana queden explícitas y sean trazables.

Las acciones y su aplicación analítica se contrastarán con la
[ficha de Miguel](FICHA_ACCIONES_CARGAS.md), que mantiene la propuesta de ese frente;
no se duplica aquí su definición.

## 6. Mapa de objetos y relaciones

Las etiquetas siguientes sirven para discutir conceptos, no son tablas ni clases.

```text
Conjunto de cimentación CF-01
  └─ posee durante su ciclo de vida → Zapata F-101
       ├─ se clasifica / comparte definición → Tipo propuesto T-01
       ├─ tiene → origen, orientación, geometría y composición material
       ├─ incluye → cuerpo de hormigón y armadura, si existe
       ├─ da apoyo a → uno o varios pedestales, estructuras o equipos
       ├─ tiene asignadas por una regla → Condiciones de emplazamiento CE-01
       │                                  ↑ pueden compartirse con otras zapatas
       ├─ se representa mediante → sólido, planos y tablas
       ├─ se corresponde con → AM-01: apoyo equivalente con muelles
       └─ se corresponde con → AM-02: placas de la zapata
                                      + muelles de respuesta del terreno

Comprobación CH-01 ── corresponde a → F-101
                  └─ procede de → AM-02

Encepado EC-01 ── incluye → hormigón, armado, tirantes / vigas embebidas
              └─ se conecta con → Pilotes P-01…P-06 (objetos separados)
                                   ├─ posición prevista y ejecutada
                                   └─ asignación geotécnica individual por regla

Elemento F-101 o EC-01 ── se analiza mediante → cálculo manual / algoritmo / EF
Proyecto ── define por clase de elemento → requisitos de comprobación
Validación técnica ── identifica → técnico, fecha, revisión física y datos
                   └─ acepta → comprobaciones seleccionadas de uno o varios análisis
```

## 7. Cinco conceptos candidatos y tres cuestiones para el equipo

Conceptos candidatos: **zapata física**, **tipo de zapata**, **condiciones de
emplazamiento**, **modelo de cálculo y su correspondencia física**, y
**comprobación y validación técnica vinculadas al elemento y sus análisis**.
El primer candidato se amplía al concepto físico común zapata/losa/encepado para
debatirlo, y el segundo a sus criterios de tipo. Son candidatos para comparar
con las otras fichas, no una propuesta de estructura de software.

1. **Tipo compartido.** Contrastar el criterio de igualdad de geometría, materiales
   y armado, incluido orden de capas, independientemente de orientación y número
   de soportes. Resolver también la distinción entre identidad del objeto y código
   que cambia con su pertenencia.
2. **Zapata, losa y encepado.** Luis identifica una diferencia de denominación,
   flexibilidad y tratamiento de cálculo, con refuerzos locales frecuentes en las
   losas. Esas posibilidades también existen en zapatas. Propone estudiar un concepto
   común que incluya también encepados, con elementos profundos separados y
   colaboración del terreno definida en el análisis (apartado 5.1). Los ejemplos
   de número de apoyos, anchura o relación entre dimensiones y canto comentados en
   la entrevista no se adoptan como umbrales universales. La necesidad de elementos
   finitos tampoco se convierte aquí en una regla obligatoria por el nombre.
3. **Emplazamiento, análisis y validación.** Acordar la asignación geotécnica por
   elemento, incluidos los pilotes, y la procedencia de las capacidades. Contrastar
   la propuesta transversal del apartado 5.2: requisitos por proyecto y clase de
   elemento, evidencias de distintos métodos, sustitución parcial de comprobaciones
   y aprobación humana trazable. No heredar automáticamente la implementación de
   Footings V2.

## 8. Simplificación inicial y decisión frágil

Luis acepta empezar por geometrías rectangulares y octogonales de canto constante.
Los contornos libres son menos habituales y pueden incorporarse después, sin
excluirlos de la definición conceptual.

Como estrategia de diseño, describe empezar con zapatas individuales e ir
combinándolas cuando no se alcance el cumplimiento o aparezcan solapes. Considera
un error de partida suponer una única zapata que cubra todo el conjunto. Este es
su criterio de trabajo, no una restricción que prohíba representar una losa común
cuando corresponda. Tampoco implica limitar el dominio a un pedestal por zapata.

## 9. Aspectos aún no respondidos

Para completar la batería común quedan por precisar el detalle geométrico y los
datos propios de las interfaces, la procedencia y fidelidad de cada intercambio,
la autoridad sobre los datos originales y el mecanismo concreto para identificar
revisiones físicas y de datos, análisis y evidencias aceptadas. El criterio de
validación ya está recogido como propuesta en el apartado 5.2. Sigue pendiente
concretar el ownership de los elementos profundos fuera de su relación con el
encepado. No se han definido asociaciones a clasificaciones
externas ni un catálogo exhaustivo de propiedades. Estos vacíos se mantienen
visibles para la revisión; no se completan mediante suposiciones.
