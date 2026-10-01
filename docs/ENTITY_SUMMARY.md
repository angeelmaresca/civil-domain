# Entidades y conceptos candidatos — resumen de lo tratado

> **Status:** DRAFT  
> **Editable:** sí; resumen derivado dentro del alcance de `WORKING_SET.md`  
> **Document owner:** equipo de dominio civil  
> **Canonical for:** —; documento de consulta, no fuente de definiciones  
> **Sources:** documentos propietarios y fichas enlazados en cada apartado  
> **Supersedes:** —  
> **Last reviewed:** 2026-10-01

## Qué recoge este documento

Resumen de los objetos y conceptos a los que se ha hecho referencia en el repositorio,
con su descripción y los datos que se han mencionado para describirlos. **No es una
lista de entidades aprobadas ni un esquema de campos obligatorios.** Las fuentes
conceptuales siguen en `DRAFT`; lo confirmado con un autor durante una entrevista
no equivale a aprobación del equipo.

«Propiedades» se utiliza aquí en sentido conceptual: incluye datos descriptivos y
referencias a otros conceptos. Las relaciones se identifican como tales; incluirlas
en una fila no significa que deban almacenarse dentro de ese objeto. Cuando no hay
detalle suficiente se indica expresamente, sin completar atributos por intuición.

Cada fila es una síntesis de lectura. La definición, los ejemplos y sus cambios
pertenecen a la fuente enlazada. Los nombres ingleses de las fichas son etiquetas
de trabajo, no clases de software adoptadas.

## Relación con `ELEMENT_INVENTORY.md`

| Documento | Pregunta que responde | Papel |
|---|---|---|
| [ELEMENT_INVENTORY.md](ELEMENT_INVENTORY.md) | ¿Qué conceptos podrían intervenir en el dominio civil? | Inventario amplio de exploración, con semillas y preguntas; una entrada no implica una entidad. |
| Este resumen | ¿Qué hemos mencionado o desarrollado y qué datos conocemos de cada candidato? | Vista de consulta transversal, con propiedades documentadas y vacíos visibles. |
| [VOCABULARY.md](VOCABULARY.md) | ¿Qué significa brevemente un término y dónde se define? | Índice terminológico. |
| [domain-objects/DESIGN_OCCURRENCE.md](domain-objects/DESIGN_OCCURRENCE.md), [domain-objects/ENGINEERING_SYSTEM.md](domain-objects/ENGINEERING_SYSTEM.md) y futuras definiciones individuales | ¿Cuál es la definición, identidad y frontera de un objeto concreto? | Fuente propietaria por objeto; actualmente están desarrollados la ocurrencia y el sistema de ingeniería candidato. |
| [RELATIONSHIPS.md](RELATIONSHIPS.md) | ¿Qué significan los vínculos entre objetos? | Fuente propietaria de la semántica de relaciones. |

El inventario es el punto de partida amplio; las fichas han profundizado en una
parte de él. Este resumen hace consultable ese avance sin trasladar conclusiones
al inventario, que permanece fuera del frente editable actual. Se crea en `docs/`
sin abrir carpetas: aporta una vista conjunta de propiedades que el vocabulario
breve y la definición individual de ocurrencia no pretenden ofrecer.

## 1. Identidad, estado y organización del diseño

Fuentes: [ocurrencia de diseño](domain-objects/DESIGN_OCCURRENCE.md),
[vocabulario propuesto en la síntesis](iteration-01/SINTESIS.md#vocabulario-mínimo-propuesto-para-contrastar-v01)
y [relaciones](RELATIONSHIPS.md). Todas las filas son candidatas.

| Concepto | Descripción resumida | Propiedades o referencias mencionadas | Frontera o pendiente |
|---|---|---|---|
| **Ocurrencia de diseño** | Individuo físico proyectado cuya continuidad interesa seguir entre estados. | ID interno estable y opaco; naturaleza física pretendida; alcance de diseño; vínculo a sus estados. | Geometría, material, posición y TAG no son su identidad. No es la pieza fabricada ni el activo instalado. |
| **Estado de diseño** (`PhysicalElementRevision` en la ficha de Ángel) | Definición de una ocurrencia para una revisión o contexto aceptado. | Ocurrencia; revisión/contexto; clase funcional; geometría; materiales; placement; relaciones vigentes; evidencia y responsable de aceptación. | No se deduce de la última importación; falta definición propia. |
| **Definición de tipo / tipo intencional** | Intención común declarada reutilizable. | Definición compartida; alcance —proyecto, assignment, entregable o plano—; relación de tipado. | Falta acordar qué propiedades controla y si tipa la ocurrencia o su estado. El criterio de igualdad de Luis sigue en debate. |
| **Agrupación derivada** | Conjunto calculado por similitud de propiedades. | Propiedades comparadas; miembros obtenidos. | No equivale a tipo declarado ni necesariamente necesita identidad propia. |
| **Estructura física / conjunto físico** | Todo físico concreto que puede tener continuidad y partes propias. | Identidad, límite, revisión y ciclo de vida; relaciones de composición con columnas, vigas u otras partes. | Debe justificar identidad separada; su forma puede derivarse de las partes. |
| **Sistema funcional / sistema estructural** | Objetos que colaboran para una función. | Función; miembros mediante relaciones potencialmente muchos-a-muchos. | La membresía no implica composición ni propiedad del ciclo de vida. |
| **Sistema de ingeniería** | Contexto de negocio candidato que relaciona ocurrencias, modelos y conciliaciones dentro de una frontera explícita. | Identidad; propósito; límite; ocurrencias contextualizadas; modelos asociados con rol, cobertura y vigencia; políticas/casos aplicables. | Debe distinguirse del conjunto físico, sistema funcional y espacio; cardinalidades y obligatoriedad abiertas. |
| **Contexto o contenedor espacial** | Organización espacial de objetos: área, planta, nivel o instalación. | Identidad y placement cuando procedan; contención principal y referencias espaciales adicionales. | No es una ocurrencia física por el solo hecho de contener objetos. |
| **Decisión de aceptación** | Decisión que reconoce un estado y su evidencia. | Quién acepta; estado/revisión; evidencia que fundamenta la decisión. | Autoridades y procedimiento aún abiertos; distinguirla de la validación de cálculos. |
| **Propuesta y aceptación de baja** | Proceso de decidir si una ocurrencia se retira del diseño. | Ocurrencia; evidencia de ausencia y alcance de la fuente; decisión responsable; revisión desde la que deja de estar activa. | Son conceptos de decisión; no se ha fijado una entidad independiente por cada paso. |

## 2. Elementos físicos e interfaces estudiados

Estas filas describen familias y ejemplos físicos, no una jerarquía de entidades
aprobada. Sus datos variables corresponden al estado de diseño, a sus partes o a
relaciones contextualizadas.

| Concepto | Descripción resumida | Propiedades o referencias mencionadas | Fuente y grado de desarrollo |
|---|---|---|---|
| **Columna / pilar** | Elemento físico estructural continuo, distinto de las barras que lo idealizan. | Perfil/sección —HEB 200 en el ejemplo—, longitud, material, geometría y placement; conexiones y pertenencias como relaciones. | [Ángel, §§2–6](iteration-01/FICHA_ANGEL_COLUMNA.md). Desarrollado; grado de material pendiente. |
| **Viga** | Elemento físico que participa en la estructura y puede recibir el apoyo de un equipo. | Perfil o composición mediante chapas mencionados en el inventario; posición del contacto como dato de la relación de apoyo. | [Inventario, grupo 3](ELEMENT_INVENTORY.md#grupo-3--elementos-de-superestructura) y [Miguel, bloque E](iteration-01/FICHA_MIGUEL_ACCIONES_CARGAS.md). Sin ficha propia de propiedades. |
| **Zapata** | Cimentación que recibe uno o varios apoyos y transmite acciones al terreno. | Contorno paramétrico o libre, dimensiones, canto, huecos/recrecidos, origen, orientación, sistema de coordenadas, profundidad respecto al pavimento, hormigón y armado; vínculos a apoyos y condiciones de emplazamiento. | [Luis, §§1–4](iteration-01/FICHA_LUIS_ZAPATA.md). No incluye automáticamente pedestal ni hormigón de limpieza. |
| **Losa de cimentación** | Cimentación discutida junto con zapatas y encepados como posible concepto común. | Geometría, materiales, armado y refuerzos locales mencionados; posible interacción con terreno y pilotes. | [Luis, §§5.1 y 7](iteration-01/FICHA_LUIS_ZAPATA.md). No hay definición independiente ni umbrales aprobados para separarla de zapata. |
| **Encepado** | Cuerpo de cimentación conectado a elementos profundos separados. | Contorno, hormigón, armado, tirantes/vigas embebidas; disposición de pilotes, separaciones y distancias al borde como datos de su configuración. | [Luis, §5.1](iteration-01/FICHA_LUIS_ZAPATA.md#51-encepados-y-elementos-de-cimentación-profunda). Colaboración del terreno: hipótesis del análisis. |
| **Pilote** | Elemento profundo que puede identificarse y controlarse individualmente, conservándose al cambiar el encepado. | Diámetro, longitud, material, procedimiento; posiciones prevista y ejecutada; asignación geotécnica individual; procedencia de capacidades. | [Luis, §5.1](iteration-01/FICHA_LUIS_ZAPATA.md#51-encepados-y-elementos-de-cimentación-profunda). Ownership pendiente. |
| **Pedestal** | Elemento de apoyo diferenciado de la zapata, descrito con comportamiento tipo columna. | Armado longitudinal vertical y estribos; relaciones con zapata, placa base o equipo. | [Luis, §1](iteration-01/FICHA_LUIS_ZAPATA.md#1-ejemplo-y-significado). Sin catálogo dimensional propio. |
| **Armadura** | Componente físico de una cimentación cuando está armada. | Material; disposición inferior/superior en dos direcciones; orden de capas; estribos perimetrales; armadura base y refuerzos locales. | [Luis, §3](iteration-01/FICHA_LUIS_ZAPATA.md#3-geometría-posición-y-materiales). Identidad del conjunto o de cada barra abierta; no automática. |
| **Equipo** | Individuo físico relevante para civil aunque otra disciplina gobierne parte de su definición. | Referencias externas, dimensiones, material, soportes, geometría relevante e interfaces; especificación del líquido opcional en el ejemplo de depósito. | [Miguel, bloque A](iteration-01/FICHA_MIGUEL_ACCIONES_CARGAS.md), matizado por [ocurrencia](domain-objects/DESIGN_OCCURRENCE.md). El TAG no sustituye al ID interno. |
| **Interfaz de apoyo** | Contacto localizable entre equipo y estructura u otros participantes. | Participantes; posición; geometría de contacto puntual o superficial en el ejemplo. | [Miguel, bloque E](iteration-01/FICHA_MIGUEL_ACCIONES_CARGAS.md). Independencia de identidad/ciclo de vida por contrastar; no equiparar contacto con nodo analítico. |
| **Conexión física** | Unión o contacto entre objetos físicos o interfaces. | Participantes, interfaces, geometría/posición y condiciones cuando correspondan. | [Relaciones](RELATIONSHIPS.md) y [Ángel, §6](iteration-01/FICHA_ANGEL_COLUMNA.md#6-conexiones-físicas). Falta ficha de Alberto; rigidez analítica no se deduce solo de la conexión. |
| **Conjunto de cimentación** | Agrupación del ejemplo de Luis a la que pertenece una zapata. | Código de conjunto, unidad y proyecto en la propuesta de identificación; miembros. | [Luis, §2](iteration-01/FICHA_LUIS_ZAPATA.md#2-identidad-pertenencia-y-tipo). Dependencia de ciclo de vida propuesta por Luis, aún por contrastar. |

## 3. Geometría, materiales y emplazamiento

No se ha decidido que cada concepto de esta tabla deba ser una entidad autónoma.

| Concepto | Descripción resumida | Propiedades o referencias mencionadas | Fuente / pendiente |
|---|---|---|---|
| **Representación física** | Forma o descripción de un estado para un propósito. | Estado representado, propósito, geometría paramétrica o libre, sólido, planos, secciones, detalles o tablas; procedencia/revisión. | [Síntesis](iteration-01/SINTESIS.md) y [Luis, §5](iteration-01/FICHA_LUIS_ZAPATA.md#5-representaciones-cálculos-y-comprobaciones). No es la identidad física. |
| **Placement / sistema de coordenadas / transformación** | Localización y orientación respecto a una referencia. | Origen, posición, orientación, sistema local/global y transformación; unidades y dato original en importación. | [Ángel, §§5 y 9](iteration-01/FICHA_ANGEL_COLUMNA.md), [Luis, §3](iteration-01/FICHA_LUIS_ZAPATA.md). No hay convenio universal adoptado. |
| **Material / composición material** | Descripción material de una pieza o sus partes. | Material estructural; grado o resistencia cuando se conoce; asignación por parte; hormigón y acero de armadura en cimentaciones. | [Ángel, §5](iteration-01/FICHA_ANGEL_COLUMNA.md#5-placement-geometría-y-material) y [Luis, §§2–3](iteration-01/FICHA_LUIS_ZAPATA.md). Catálogo no definido. |
| **Perfil / sección** | Descripción reutilizable de una sección; no es la columna individual. | Designación de perfil, como HEB 200/300; geometría de sección mencionada. | [Ángel, §3](iteration-01/FICHA_ANGEL_COLUMNA.md#3-ocurrencia-tipo-clasificación-y-propiedades). Propiedades geométricas exhaustivas no documentadas. |
| **Condiciones de emplazamiento** | Contexto geotécnico y de cotas aplicable a un elemento. | Perfil geotécnico, nivel freático, cota de pavimento y procedencia de proyecto. | [Luis, §4](iteration-01/FICHA_LUIS_ZAPATA.md#4-terreno-y-condiciones-de-emplazamiento). Pueden compartirse. |
| **Asignación geotécnica** | Relación que determina qué condiciones se aplican a cada cimentación o pilote. | Elemento destinatario, condiciones/perfil y regla: zonificación, cercanía o interpolación. | [Luis, §§4 y 5.1](iteration-01/FICHA_LUIS_ZAPATA.md) y [relaciones](RELATIONSHIPS.md). No se deduce de pertenecer al mismo módulo. |
| **Perfil geotécnico / estrato** | Caracterización del terreno relevante para cimentar. | Estratos y profundidades; capacidades asociadas a perfiles según Luis, con procedencia en informe o cálculo. | [Luis, §§4 y 5.1](iteration-01/FICHA_LUIS_ZAPATA.md) e [inventario, grupo 5](ELEMENT_INVENTORY.md#grupo-5--terreno-geotecnia-y-movimiento-de-tierras). Reparto entre dato observado, parámetro adoptado y resultado pendiente. |

## 4. Acciones, escenarios y consultas

Fuentes: [ficha de Miguel](iteration-01/FICHA_MIGUEL_ACCIONES_CARGAS.md) y
[aclaración de Luis, §10](iteration-01/FICHA_LUIS_ZAPATA.md#10-aclaración-de-luis-acciones-escenarios-y-summaries).
Son aportaciones para contraste; no una unificación ya resuelta.

| Concepto | Descripción resumida | Propiedades o referencias mencionadas | Frontera o pendiente |
|---|---|---|---|
| **Acción** | Efecto con origen y contexto que actúa sobre un elemento. | Origen, objetivo, magnitud/dirección, escenario, ejes, signos y unidades; fuerzas y momentos `Fx, Fy, Fz, Mx, My, Mz` en un punto; aplicación puntual, lineal o superficial. | Identidad entre casos y propiedad de la magnitud por caso pendientes. No es un campo fijo de la zapata. |
| **Caso de carga / hipótesis simple** | Escenario que agrupa acciones; Luis incluye acciones y reacciones de distintos elementos y puntos. | Identificación del escenario y acciones/resultados asociados; ejemplos lleno/vacío. | Equivalencia exacta entre los términos por cerrar. No hay una hipótesis por apoyo. |
| **Combinación** | Escenario definido mediante hipótesis simples y coeficientes. | Hipótesis participantes y coeficientes; resultados por punto separados de la definición. | La superposición de resultados depende de la linealidad; no se asume universal. |
| **Matriz de combinaciones** | Organización conjunta de las definiciones de combinación. | Filas por combinación, columnas por hipótesis, coeficientes. | Puede ser una representación de definiciones; no se ha decidido identidad propia. |
| **Envolvente** | Lista común y ordenada de combinaciones completas para consultar o comprobar, según Luis. | Combinaciones y orden; valores asociados en cada punto mediante resultados. | No es un vector artificial de máximos de distintos escenarios. |
| **Aplicación analítica de acción** (`AppliedLoad`) | Vínculo que lleva una acción a un modelo concreto. | Acción, modelo/revisión, objeto receptor —nodo, barra, superficie—, posición de aplicación y contexto de referencia. | La limitación a una aplicación por modelo de Miguel corresponde a su ejemplo puntual; no es regla general de todas las cargas. |
| **Summary / summary advanced** | Consulta reducida sobre una envolvente en un punto y ejes. | Envolvente, punto, ejes, criterios de selección y combinaciones completas seleccionadas; 12 entradas de extremos de fuerzas/momentos y 16 en advanced, según Luis. | Es una consulta, no una entidad física. Advanced añade extremos de `Mx/Fy` y `Mz/Fy`; detalles y singularidad en la fuente. |

## 5. Análisis, resultados y validación

Fuentes: [Ángel, §§7–10](iteration-01/FICHA_ANGEL_COLUMNA.md),
[Luis, §5](iteration-01/FICHA_LUIS_ZAPATA.md#5-representaciones-cálculos-y-comprobaciones)
y [Luis, §11](iteration-01/FICHA_LUIS_ZAPATA.md#11-esfuerzos-desplazamientos-y-representaciones-analíticas).

| Concepto | Descripción resumida | Propiedades o referencias mencionadas | Frontera o pendiente |
|---|---|---|---|
| **Modelo de ingeniería** | Artefacto con identidad, propósito, cobertura y revisiones propios. | Rol físico, analítico, documental u otro; propósito; cobertura; disciplina/herramienta; revisiones; sistemas asociados. | Abstracción común todavía por demostrar; no pertenece a una ocurrencia individual. |
| **Modelo analítico** | Idealización con propósito y ciclo de vida propios que puede representar múltiples elementos físicos. | Propósito, hipótesis, objetos, revisiones y procedencia/herramienta cuando exista. | No pertenece a una sola columna ni exige siempre malla; falta decidir su relación exacta con el candidato general `ModeloDeIngeniería`. |
| **Revisión de modelo analítico** | Versión identificada de la topología y datos empleados. | Modelo, revisión, objetos/conectividad y datos de cálculo utilizados. | Diferente de la revisión física. |
| **Objeto analítico / idealización** | Nodo, barra, placa, superficie u otra representación para analizar. | Identidad contextual en el modelo/revisión; geometría/topología; propiedades analíticas según su naturaleza. | No todos los métodos precisan los mismos objetos; también hay formulaciones sin discretización. |
| **Nodo / nudo** | Objeto puntual de la topología analítica. | Posición en el modelo; conectividad; condiciones de apoyo si corresponden. | Desplazamientos y reacciones son resultados contextualizados, no propiedades físicas de la columna. |
| **Barra analítica** | Idealización lineal que puede representar todo o parte de uno o varios físicos. | Nodos, sección, material, offsets/excentricidades, liberaciones y conexiones según la idealización. | Una columna puede corresponder a varias barras. |
| **Placa analítica** | Idealización superficial; varias placas pueden representar una zapata. | Geometría y ejes locales; relación con la zona física representada; resultados evaluados por punto y escenario. | No hay catálogo completo de atributos adoptado. |
| **Apoyo, restricción, resorte / muelle** | Condiciones analíticas de contorno o respuesta equivalente. | Restricciones, rigideces y localización según el modelo. | No equivalen automáticamente a un apoyo físico. |
| **Método / formulación de cálculo** | Forma de analizar: sólido rígido, elementos finitos, plasticidad, flexión o bielas y tirantes. | Método, hipótesis y propósito. | No confundir método con programa ni imponer una única representación matemática. |
| **Ejecución de análisis** | Cálculo concreto que genera resultados. | Modelo/revisión, hipótesis y entradas utilizadas; resultados producidos. | Debe distinguirse del modelo y permitir trazabilidad; estructura definitiva pendiente. |
| **Resultado** | Evidencia obtenida en un análisis. | Análisis/modelo, hipótesis o combinación, objeto/lugar de evaluación, ejes, unidades y valores. | No queda definido por el elemento físico únicamente. |
| **Reacción** | Respuesta de fuerzas y momentos ante acciones recibidas. | Componentes, punto, ejes, unidades, escenario y análisis de origen. | Puede convertirse en acción para otro dominio conservando procedencia y convenio de signos. |
| **Esfuerzos: resultantes** | Fuerzas y momentos internos referidos a una sección o zona. | `Fx, Fy, Fz, Mx, My, Mz`; sección/punto, escenario, análisis, ejes y unidades. | Distinguir de acciones y reacciones aunque compartan componentes. |
| **Tensiones / presiones** | Valores locales de fuerza por superficie. | Valor o distribución; punto/sección/superficie; escenario, análisis, ejes y unidades. | Criterios de summary pendientes. |
| **EsfuerzosPlaca** | Resultados de placa por unidad de longitud. | `SQX`, `SQY`, `SX`, `SY`, `SXY`, `Mx`, `My`, `Mxy`; punto, ejes locales, unidades, escenario y análisis. | Summary de 16 extremos confirmado con Luis; sigue `DRAFT`. No equivale a advanced de fuerzas/momentos. |
| **Desplazamientos nodales** | Movimiento calculado de un nudo. | Tres traslaciones y tres giros; nudo, ejes, escenario y análisis. | No está confirmada la regla de summary de 12 entradas. |
| **Requisito de comprobación** | Exigencia que debe justificarse para un elemento. | Proyecto, clase de elemento y comprobaciones requeridas. | Catálogo variable; la lista de Luis es ilustrativa, no normativa universal. |
| **Comprobación** | Evaluación sustentada en un análisis y vinculada al elemento. | Elemento/revisión, análisis y resultados que la sustentan; aspecto comprobado e histórico. | Resultado favorable no equivale a validación final. |
| **Validación técnica** | Aprobación humana de la suficiencia de las evidencias de cálculo. | Técnico, fecha, revisión física y datos, comprobaciones aceptadas/sustituidas, justificación de no aplicabilidad. | Puede seleccionar evidencias de varios análisis; cambios relevantes requieren revisar la validación. |

## 6. Procedencia, intercambio y relaciones con trazabilidad

Fuentes: [Ángel, §§8–9](iteration-01/FICHA_ANGEL_COLUMNA.md),
[síntesis](iteration-01/SINTESIS.md) y [relaciones](RELATIONSHIPS.md).

| Concepto | Descripción resumida | Propiedades o referencias mencionadas | Frontera o pendiente |
|---|---|---|---|
| **Modelo fuente y revisión** (`ExternalModelRevision`) | Entrega concreta de una aplicación o proceso. | Aplicación/procedencia, modelo, revisión, alcance completo o parcial y rol de la información. | El programa de origen no determina por sí solo si todos sus objetos son físicos o analíticos. |
| **Referencia externa** (`ExternalObjectReference`) | Identificador contextual de un objeto en una fuente. | ID nativo/TAG/código, aplicación, modelo y revisión. | No sustituye al ID interno del CDM. |
| **Snapshot importado** (`ImportedObjectSnapshot`) | Afirmación conservada de una fuente sobre un objeto en una revisión. | Referencia de fuente y datos recibidos en esa revisión. | Evidencia que puede diferir de otra fuente; no es automáticamente estado aceptado. |
| **Representación** | Continuidad contextual que enlaza una ocurrencia con lo que un modelo expresa sobre ella para un propósito. | Ocurrencia; modelo; propósito; snapshots por revisión; referencias externas; forma y cobertura. | No es la ocurrencia ni el modelo; puede cambiar topología entre snapshots. |
| **Placement de fuente** (`SourcePlacement`) | Localización tal como la declara la fuente. | Placement, unidades, sistema de coordenadas; transformación normalizada conservando el original. | Concepto de intercambio; autonomía como entidad no decidida. |
| **Conciliación de identidad** (`IdentityMatch`) | Justificación de que objetos físicos de fuente corresponden a una ocurrencia. | Snapshots/referencias comparados, ocurrencia, criterio/evidencia y confirmación o ambigüedad. | Nombre o proximidad no bastan; no se usa para igualar físico con analítico. |
| **Correspondencia físico–analítica** (`PhysicalAnalyticalMapping`) | Relación trazable entre estados/snapshots físicos y objetos o zonas analíticos. | Participantes y roles, revisiones, propósito, cobertura, cardinalidad, evidencia, autor, referencias y transformaciones. | Admite `1:1`, `1:N`, `N:1`, `N:M`. La correspondencia histórica no se reescribe por un nuevo estado físico. |
| **Evaluación de alineación** (`AlignmentAssessment`) | Juicio sobre una correspondencia frente a una revisión física de comparación. | Correspondencia, revisión comparada, aspecto evaluado, estado y motivos. | No equivale a aprobar técnicamente el elemento. |
| **Relación de diseño** | Vínculo semántico contextualizado: composición, pertenencia, conexión, apoyo, tipado u otros. | Tipo de vínculo, participantes, contexto, vigencia, procedencia y datos particulares. | No sustituir toda la semántica por un único padre o vínculo genérico. |
| **Caso de conciliación** | Contexto histórico de una comparación y sus decisiones. | Alcance; propósito; sistemas; modelos y revisiones; políticas; aspectos comparados; discrepancias; decisiones y resultado. | Nombre y lifecycle abiertos; puede abarcar sistema, conjunto u ocurrencia. |
| **Vista resuelta de propiedades** | Selección o derivación de valores para una consulta, aspecto y momento concretos. | Fuentes y revisiones; política de autoridad; transformaciones; valor y procedencia resultantes. | No es una copia maestra dentro de la ocurrencia ni una autoridad universal. |
| **Referencia de clasificación** | Asociación a un vocabulario externo o acordado. | Objeto clasificado y referencia al vocabulario. | No crea identidad ni tipo intencional; catálogo y detalle pendientes. |

## 7. Otros conceptos mencionados, todavía sin desarrollo suficiente

El [inventario inicial, grupos 1–8](ELEMENT_INVENTORY.md#3-grupos-de-exploración)
contiene además las semillas siguientes. Se conservan agrupadas porque aún no hay
base documental para atribuirles una ficha completa de entidad y propiedades.
Algunas son familias físicas; otras son parámetros, geometrías o fenómenos.

| Familia | Conceptos mencionados | Descripción disponible y propiedades |
|---|---|---|
| Estructuras y sistemas | Edificio industrial, nave, cubierta, pipe rack, rack eléctrico, soporte de equipos, plataforma, pórtico, galería de transportador, torre, estructura enterrada y de contención. | Conjuntos o sistemas con una finalidad. Falta resolver individualmente si son tipo, todo físico, sistema o contexto espacial; sin catálogo propio de propiedades. |
| Equipos e interfaces | Equipo estático/rotativo, recipiente, tanque, intercambiador, bomba, compresor, skid, silo, transformador, soporte, patrón de anclajes, centro de gravedad, envolvente geométrica. | Equipos y datos de interfaz necesarios para civil. Solo el depósito y su apoyo tienen un caso desarrollado; no se documentan propiedades específicas para cada familia. |
| Superestructura y uniones | Arriostramiento, tirante, cercha, losa, forjado, muro, ménsula, capitel, escalera, chapa, cartela, rigidizador, unión, soldadura, tornillo. | Elementos o partes portantes/auxiliares y sus uniones. Sin definición ni propiedades individuales cerradas. |
| Cimentación y componentes | Zapata corrida, micropilote, barreta, dado, muro de sótano, socket, viga de atado, viga centradora, placa base, grout, perno, conjunto de anclaje, llave de cortante, relleno sobre cimentación. | Elementos, componentes e interfaces mencionados. Micropilotes/barretas se separan del encepado en la ficha de Luis; el resto no tiene catálogo propio. |
| Capas externas a cimentación | Hormigón de limpieza, geotextil y tratamientos superficiales. | Capas opcionales externas a la zapata; se menciona su influencia sobre rozamiento y recubrimiento, sin descripción detallada. |
| Terreno y obras de tierra | Terreno, suelo, roca, sondeo, muestra, ensayo, relleno, terreno mejorado, excavación, terraplén, talud, contención. | Medio físico, investigación o actuaciones. Sus propiedades individuales siguen pendientes. |
| Parámetros geotécnicos | Capacidad portante, presión admisible, módulo de balasto y nivel freático. | Parámetros/condiciones mencionados, no entidades asumidas; falta precisar contexto, procedencia y reparto de responsabilidades. |
| Acciones y escenarios adicionales | Peso propio, viento, sismo, temperatura, empuje del terreno, desplazamiento impuesto, grupo y situación de diseño. | Fenómenos u organización de acciones; sin definición particular desarrollada para cada uno. |
| Otros conceptos analíticos | Sólido analítico, elemento finito, malla, vínculo rígido, rigidez, masa, excentricidad, utilización y warning. | Objetos, propiedades o información de análisis; no se ha decidido cuáles requieren identidad autónoma. |
| Referencias y geometrías | Datum, norte, elevación, nivel, eje, rejilla, punto, línea, curva, superficie, sólido, contorno, hueco, volumen, geometría importada y nivel de detalle. | Referencias y recursos descriptivos de localización/representación; propiedades y autonomía pendientes. |
| Contexto organizativo y realización | Proyecto, unidad de planta, técnico responsable, pieza fabricada y activo instalado. | Proyecto/unidad contextualizan datos; el técnico interviene en la validación. La realización/activo es una extensión futura explícitamente separada de la ocurrencia de diseño. |

Las entidades de IFC y los objetos específicos de Footings, CADMATIC, Tekla, Revit,
STAAD o SP3D citados en los estudios son referencias comparativas. No se incorporan
como entidades propias por aparecer en la documentación externa. Véase el
[estudio IFC](research/IFC_CORE_CONCEPTS.md).

## 8. Cuestiones abiertas que afectan a este resumen

- **Identidad y códigos:** las fichas no coinciden completamente sobre TAG, código,
  sustitución y continuidad. La definición candidata de ocurrencia separa ID interno,
  estado y referencia externa; falta contraste humano de sus reglas.
- **Tipo y estado:** no está cerrado el criterio de tipo compartido ni el reparto de
  propiedades entre tipo y estado. Véanse las [notas de tipo/estado](iteration-02/NOTAS_TIPO_ESTADO_DISENO.md).
- **Conexiones y composición:** falta la aportación de Alberto y cerrar qué partes
  necesitan identidad independiente.
- **Acciones:** falta conciliar identidad y magnitud por escenario, y acordar unidades
  y convenios de intercambio. Los ejemplos con Y o Z vertical no fijan un eje universal.
- **Alineación y validación:** son decisiones distintas; la correspondencia histórica
  no acredita por sí sola vigencia técnica. Véanse las [notas físico–analíticas](iteration-02/NOTAS_CORRESPONDENCIA_FISICO_ANALITICA.md).
- **Propiedades y ownership:** no existe todavía un catálogo exhaustivo ni una matriz
  aprobada de responsables por dato. Este resumen no los introduce.
- **Sistemas de ingeniería:** falta demostrar que aportan identidad y responsabilidades
  distintas del conjunto físico, sistema funcional o espacio. También están abiertas
  la pertenencia múltiple, la cobertura parcial y la conciliación transversal.

Cuando se desarrolle un candidato, sus definiciones y propiedades se precisarán en
su fuente propietaria y aquí se actualizará únicamente la síntesis y el enlace.

## 9. Precisiones posteriores: sesión del 23 de septiembre

La [conversación](iteration-02/ENUNCIADO.md#11-sesión-del-23-de-septiembre-conjuntos-y-versiones)
matiza las tablas anteriores, procedentes de la primera ronda. Todo sigue `DRAFT`.

| Concepto | Precisión / propiedades o referencias | Fuente propietaria |
|---|---|---|
| Estado de pieza | Se describe dentro de una versión completa del conjunto; no exige versiones independientes por columna o zapata. | [Ocurrencia](domain-objects/DESIGN_OCCURRENCE.md#contraste-de-conjuntos-y-versiones-completas) |
| Estructura y cimentación | Versiones independientes, con dependencias técnicas de cargas. | [Reglas](RULES.md#versiones-de-conjuntos-y-cargas--propuesta-para-contraste) |
| PR-05 | Persiste al modularizar e incluye cimentaciones; configuración global versionada no requerida actualmente. | [Ocurrencia](domain-objects/DESIGN_OCCURRENCE.md#contraste-de-conjuntos-y-versiones-completas) |
| Módulo | Puede conservarse al cambiar composición o sustituirse; TAG reutilizable. Inclusión de cimentación pendiente del equipo. | [Ocurrencia](domain-objects/DESIGN_OCCURRENCE.md#contraste-de-conjuntos-y-versiones-completas) |
| Base de cargas / aceptación | Referencia a versión proveedora y aceptación explícita sin cambios como necesidad futura. | [Relaciones](RELATIONSHIPS.md#dependencias-de-cargas-entre-versiones) |
| Unidad | Zona o proceso; no asumir contención espacial por prefijo de TAG. | [Evidencia](iteration-02/ENUNCIADO.md#identidad-alcance-y-códigos) |

Se distingue ahora versión técnica de revisión de emisión documental. Sigue sin
responder el caso de cimentación compartida entre módulos. Conservar modelos
históricos sin vínculo pieza a pieza basta para la remodularización descrita;
no se adopta como simplificación universal.
