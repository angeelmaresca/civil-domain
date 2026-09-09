# Inventario inicial de conceptos

> **Status:** DRAFT  
> **Editable:** no mientras `BIM_REFERENCE_MAP.md` sea el documento activo  
> **Document owner:** equipo de dominio civil  
> **Canonical for:** —  
> **Sources:** experiencia del equipo, Footings y referencias externas por incorporar  
> **Supersedes:** —  
> **Last reviewed:** 2026-09-08

## 1. Objetivo

Recoger con amplitud los conceptos que pueden intervenir en el dominio civil y
estructural de una planta industrial, sean físicos o no. El inventario debe ayudar a
descubrir vocabulario, categorías, relaciones y límites antes de decidir qué
conceptos serán entidades del modelo.

En esta fase importa más no olvidar conceptos relevantes que obtener una
clasificación perfecta.

## 2. Reglas del inventario

1. **Concepto no significa entidad.** Una entrada puede terminar siendo entidad,
   value object, catálogo, propiedad, relación, representación o quedar fuera del
   dominio.
2. **Las categorías son provisionales.** Sirven para repartir la exploración y
   detectar huecos; no constituyen todavía una jerarquía.
3. **Un concepto puede aparecer en varios grupos.** Se consolidará después sin
   forzarlo prematuramente a una única categoría.
4. **Se admiten dudas y contradicciones.** Deben quedar visibles en lugar de
   resolverse por intuición.
5. **No se exige el mismo detalle a todo.** Cada concepto comienza con una captura
   rápida. Solo los prioritarios o ambiguos pasan al análisis ampliado.
6. **Las fuentes aportan evidencia, no autoridad automática.** Footings, IFC,
   CADMATIC, Tekla u otros modelos pueden usar límites distintos de los nuestros.
7. **No se diseñan tablas ni clases durante el inventario.** Identidad conceptual no
   equivale todavía a una estrategia de persistencia.

## 3. Grupos de exploración

Los grupos utilizan familias reconocibles por el equipo de ingeniería. No definen
todavía módulos, agregados ni una jerarquía del modelo. Identidad, materiales,
geometría, relaciones, revisiones y ownership se revisan transversalmente mediante
la plantilla común.

### Grupo 1 — Tipos de estructuras y sistemas estructurales

**Qué busca:** conjuntos reconocibles como una estructura completa o como un sistema
estructural con una finalidad determinada.

**Qué debe aportar:** nombres utilizados por el equipo, finalidad de cada estructura,
elementos que normalmente la componen y límites con otras estructuras o sistemas.

**Semillas:** edificio industrial, nave, cubierta, pipe rack, rack eléctrico,
estructura soporte de equipos, plataforma, pórtico, galería de transportador, torre,
estructura enterrada y estructura de contención.

**Ejemplo:** describir `Pipe rack` como un sistema que puede agrupar columnas, vigas,
arriostramientos y cimentaciones; dejar abierta la diferencia entre el tipo «pipe
rack», una estructura concreta y cada uno de sus módulos.

### Grupo 2 — Equipos e interfaces con civil

**Qué busca:** equipos relevantes para civil y la información mediante la que se
apoyan, conectan o transmiten acciones a la estructura.

**Qué debe aportar:** tipos de equipo, información recibida de otras disciplinas,
puntos o superficies de interfaz y datos que civil necesita sin ser propietario del
equipo completo.

**Semillas:** equipo estático, equipo rotativo, recipiente, tanque, intercambiador,
bomba, compresor, skid, silo, transformador, soporte de equipo, punto de apoyo,
patrón de anclajes, centro de gravedad y envolvente.

**Ejemplo:** describir `Punto de apoyo de equipo` como una interfaz localizable que
puede entregar acciones a elementos civiles; dejar abierto si es un objeto con
identidad, una referencia externa o una propiedad del equipo.

### Grupo 3 — Elementos de superestructura

**Qué busca:** elementos físicos situados por encima o fuera de la cimentación que
forman las estructuras y sus uniones.

**Qué debe aportar:** elementos portantes y auxiliares, piezas que los componen,
conexiones y diferencias entre forma geométrica y función estructural.

**Semillas:** viga, columna, pilar, arriostramiento, tirante, cercha, losa, forjado,
muro, ménsula, capitel, plataforma, escalera, perfil, sección, chapa, cartela,
rigidizador, unión, soldadura y tornillo.

**Ejemplo:** describir `Viga` como un elemento físico que participa en una estructura
y puede estar formado por un perfil o varias chapas; diferenciarla de su eje
geométrico y de la barra que la representa analíticamente.

### Grupo 4 — Elementos de cimentación y subestructura

**Qué busca:** elementos que reciben la superestructura o los equipos y transmiten
sus acciones hacia el terreno.

**Qué debe aportar:** tipos de cimentación, elementos intermedios, componentes de
anclaje, composición física y relaciones con superestructura y terreno.

**Semillas:** zapata aislada, combinada y corrida, losa de cimentación, encepado,
pilote, micropilote, pedestal, dado, muro de sótano, socket, viga de atado, viga
centradora, placa base, grout, perno, conjunto de anclaje, llave de cortante,
armadura y relleno sobre cimentación.

**Ejemplo:** describir `Zapata` como un elemento con identidad y función propias que
puede admitir distintas geometrías; anotar qué recibe, cómo se relaciona con el
terreno y qué papel desempeña Footings.

### Grupo 5 — Terreno, geotecnia y movimiento de tierras

**Qué busca:** el medio natural, su caracterización y las actuaciones que lo
modifican para construir.

**Qué debe aportar:** objetos observados o investigados, modelos e interpretaciones
geotécnicas, parámetros adoptados y obras de preparación o mejora.

**Semillas:** terreno, suelo, roca, estrato, perfil geotécnico, sondeo, muestra,
ensayo, nivel freático, relleno, terreno mejorado, excavación, terraplén, talud,
contención, capacidad portante, presión admisible y módulo de balasto.

**Ejemplo:** distinguir en `Estrato de terreno` el volumen físico, su clasificación
a partir de ensayos y los parámetros adoptados para un cálculo; dejar abierto si son
perspectivas de un mismo concepto o conceptos diferentes.

### Grupo 6 — Acciones y organización de cargas

**Qué busca:** las acciones que afectan a estructuras y equipos y la forma de
agruparlas para estudiar situaciones de diseño.

**Qué debe aportar:** origen, naturaleza, objetivo y representación de cada acción;
significado y relación entre cargas, casos o hipótesis, combinaciones y envolventes.

**Semillas:** fuerza, momento, presión, carga puntual, lineal y superficial, peso
propio, viento, sismo, temperatura, empuje del terreno, desplazamiento impuesto,
caso de carga, hipótesis, grupo, situación de diseño, combinación y envolvente.

**Ejemplo:** describir `Caso de carga` como el contexto que agrupa acciones
compatibles; relacionarlo con acciones y combinaciones y dejar abierta su diferencia
exacta con «hipótesis».

Durante el inventario se mantiene explícitamente:

```text
acción ≠ caso o hipótesis ≠ combinación ≠ envolvente
```

### Grupo 7 — Modelo analítico y resultados

**Qué busca:** las idealizaciones utilizadas para analizar el comportamiento y los
resultados obtenidos bajo unas hipótesis concretas.

**Qué debe aportar:** objetos analíticos, condiciones de contorno, correspondencia
con elementos físicos, operaciones de cálculo, comprobaciones y resultados.

**Semillas:** modelo analítico, nodo, barra, superficie, sólido analítico, elemento
finito, malla, apoyo, restricción, liberación, resorte, vínculo rígido, rigidez, masa,
excentricidad, esfuerzo, reacción, desplazamiento, comprobación, utilización,
resultado y warning.

**Ejemplo:** describir `Barra analítica` como una idealización lineal que representa
uno o más elementos físicos; anotar nodos, propiedades y liberaciones sin
confundirla con la viga o columna construida.

### Grupo 8 — Coordenadas, geometría y representación

**Qué busca:** conceptos utilizados para localizar y representar los objetos de los
demás grupos.

**Qué debe aportar:** sistemas de referencia, reglas de placement, primitivas
geométricas, representaciones paramétricas o libres y posibles niveles de detalle.

**Semillas:** sistema de coordenadas, origen, datum, norte, elevación, nivel, eje,
rejilla, placement, orientación, transformación, punto, línea, curva, superficie,
sólido, perfil, sección, contorno, hueco, volumen, geometría paramétrica, geometría
libre, geometría importada y nivel de detalle.

**Ejemplo:** describir `Sistema de coordenadas local` como una referencia respecto a
la que se expresan posiciones y geometrías; dejar abierta su identidad, su relación
con sistemas superiores y qué ocurre cuando cambia su transformación.

## 4. Un mismo escenario visto por los grupos

Para saber dónde empezar, todos pueden observar el mismo caso sin intentar describir
todo el sistema. Supongamos un equipo apoyado mediante placa base y pernos sobre un
pedestal, una zapata y el terreno.

| Grupo | Conceptos que podría detectar | Aportación esperada |
|---|---|---|
| 1 — Tipos de estructuras | estructura soporte, pórtico o módulo | qué conjunto estructural existe y qué finalidad tiene |
| 2 — Equipos e interfaces | equipo, punto de apoyo, patrón de anclajes, centro de gravedad | qué necesita conocer civil del equipo y cómo interactúa con él |
| 3 — Superestructura | columna, viga, arriostramiento, placa o unión | qué elementos conducen las acciones hacia la cimentación |
| 4 — Cimentación y subestructura | placa base, grout, pernos, pedestal, zapata | qué elementos forman la cimentación y cómo se componen o conectan |
| 5 — Terreno y geotecnia | excavación, estrato, nivel freático, parámetro geotécnico | sobre qué medio se construye y cómo se caracteriza |
| 6 — Acciones y cargas | fuerza, momento, caso, combinación, envolvente | qué acciones existen, de dónde proceden y cómo se organizan |
| 7 — Modelo analítico | nodo, barra, apoyo, resorte, reacción, comprobación | cómo se idealiza y qué resultados se obtienen |
| 8 — Coordenadas y geometría | sistemas local y global, placement, sólidos, superficies | cómo se localizan y representan los objetos anteriores |

Que un concepto aparezca en una columna no lo convierte en propiedad exclusiva de
ese grupo. Si dos personas detectan `Zapata`, ambas la registran con su perspectiva y
la consolidación posterior preserva la información complementaria.

## 5. Flujo de trabajo por concepto

### Paso 1 — Captura rápida

Se aplica a todos los conceptos. Debe poder completarse en pocos minutos y no exige
resolver todas las preguntas.

```markdown
### Nombre provisional

**Otros nombres o sinónimos:**
**Grupo donde apareció:** 1 / 2 / 3 / 4 / 5 / 6 / 7 / 8 / varios
**Fuente o ejemplo de uso:**

**¿Qué representa?**
Una frase en lenguaje del equipo.

**Naturaleza provisional:**
Sistema / físico / espacial / material / geométrico / analítico / acción /
informativo / relación / por determinar. Se pueden marcar varias.

**¿Por qué necesitamos conocerlo?**
Operación, decisión o intercambio de información que lo utiliza.

**¿Parece necesitar identidad propia? ¿Por qué?**
Sí / no / por determinar.

**¿Puede existir de forma independiente o forma parte de otro concepto?**

**Relaciones conocidas, expresadas con verbos:**

**Relación conocida con Footings:**
Entrada / salida / calculado / referenciado / ninguna conocida / por determinar.

**Dudas y casos límite:**
```

### Paso 2 — Análisis ampliado

Se aplica únicamente cuando el concepto sea prioritario, ambiguo o necesario para
entender otros. No completar por obligación durante la primera ronda.

1. ¿Qué lo hace reconocible como el mismo objeto a lo largo del tiempo?
2. ¿Qué cambios conserva su identidad y cuáles crean otro objeto o revisión?
3. ¿Quién lo crea, modifica, aprueba, sustituye o elimina?
4. ¿Tiene partes? ¿Es parte de algo? ¿Pueden esas partes vivir por separado?
5. ¿Qué relaciones mantiene y qué significado tiene cada relación?
6. ¿Posee geometría o solamente referencia una representación geométrica?
7. ¿Puede tener varias geometrías, niveles de detalle o estados temporales?
8. ¿Cómo se le asignan materiales cuando contiene varias partes o regiones?
9. ¿Tiene representación analítica? ¿La correspondencia es uno a uno, uno a varios
   o varios a uno?
10. ¿Puede participar en distintos modelos de análisis o alternativas de diseño?
11. ¿Qué reglas deben cumplirse siempre?
12. ¿Qué información es introducida, importada, derivada o calculada?
13. ¿Qué otros contextos o aplicaciones son propietarios de parte de su información?
14. ¿Qué necesita recibir Footings y qué podría devolver sobre este concepto?
15. ¿Qué ejemplo real pone en tensión la definición propuesta?

## 6. Ejemplos seleccionados de captura rápida

Los ejemplos muestran el nivel de detalle esperado en la captura inicial. Contienen
hipótesis y dudas deliberadas; no son definiciones aprobadas.

### Grupo 4 — Zapata

**Otros nombres o sinónimos:** cimentación superficial; footing en documentación en
inglés. Debe comprobarse si «cimentación» se usa también con un alcance más amplio.

**Grupo donde apareció:** 4; también se relaciona con 3, 5, 6, 7 y 8.

**Fuente o ejemplo de uso:** Footings; experiencia del equipo; zapata aislada que
recibe un pedestal y transmite acciones al terreno.

**¿Qué representa?**  
Elemento de cimentación superficial cuya función principal es distribuir y
transmitir acciones de la estructura al terreno.

**Naturaleza provisional:** físico; desempeña una función estructural. Puede disponer
de representaciones geométricas y analíticas diferenciadas.

**¿Por qué necesitamos conocerlo?**  
Debe poder localizarse, relacionarse con otros elementos, definirse geométricamente,
asignarse a condiciones geotécnicas, calcularse, comprobarse y revisarse.

**¿Parece necesitar identidad propia? ¿Por qué?**  
Probablemente sí: puede nombrarse, cambiar de geometría, recibir revisiones y
conservar resultados o referencias durante su ciclo de vida.

**¿Puede existir de forma independiente o forma parte de otro concepto?**  
Puede formar parte de una solución estructural o de cimentación, pero no está
decidido si ese contenedor determina su lifecycle. Puede relacionarse con uno o más
pedestales, muros, columnas, vigas de atado, pilotes u otros elementos.

**Relaciones conocidas, expresadas con verbos:**

- recibe o soporta pedestales, muros u otros elementos;
- transmite acciones al terreno;
- puede conectarse con otras cimentaciones mediante vigas;
- posee o referencia una geometría;
- utiliza uno o varios materiales;
- puede representarse mediante uno o varios modelos analíticos;
- puede ser calculada o comprobada por Footings.

**Relación conocida con Footings:** entrada, objeto dimensionable y comprobable, y
origen de resultados. Permanece abierto si Footings modifica la misma revisión civil
o propone otra.

**Dudas y casos límite:**

- zapata combinada para varios soportes;
- geometría libre o formada por varios cuerpos;
- diferencia entre zapata, losa de cimentación, encepado y macizo;
- zapata ejecutada por fases o con materiales diferentes;
- conservación de identidad cuando cambia sustancialmente su geometría.

### Grupo 4 — Conjunto de anclaje

**Otros nombres o sinónimos:** sistema de anclaje; anchor bolt assembly. Debe
comprobarse si el equipo usa «pernos» para referirse tanto al conjunto como a sus
piezas individuales.

**Grupo donde apareció:** 4; se relaciona especialmente con 2, 6 y 8.

**Fuente o ejemplo de uso:** Footings; conjunto formado por pernos, tuercas,
arandelas y posibles elementos auxiliares que vincula una placa base con un elemento
de hormigón.

**¿Qué representa?**  
Conjunto físico de piezas que materializa parte de la unión y transmite determinadas
acciones entre elementos.

**Naturaleza provisional:** físico, compuesto y participante en una conexión.

**¿Por qué necesitamos conocerlo?**  
Debe poder definirse, posicionarse, comprobarse, cuantificarse y relacionarse con la
placa base y el hormigón donde queda anclado.

**¿Parece necesitar identidad propia? ¿Por qué?**  
Por determinar. El conjunto probablemente necesita ser identificable; no está claro
si cada perno necesita identidad durante todas las fases o solo posición dentro del
conjunto.

**¿Puede existir de forma independiente o forma parte de otro concepto?**  
Puede ser un conjunto perteneciente a una conexión o a un elemento soportado. Sus
piezas forman parte de él, pero algunas podrían sustituirse o comprobarse
individualmente.

**Relaciones conocidas, expresadas con verbos:**

- contiene pernos, tuercas y arandelas;
- conecta o ancla una placa base a un elemento de hormigón;
- sigue un patrón de posiciones;
- transmite tracción, cortante u otras acciones;
- puede derivar de un estándar o catálogo.

**Relación conocida con Footings:** puede ser input, objeto dimensionable y objeto de
comprobación; Footings ya diferencia pernos y otros componentes auxiliares.

**Dudas y casos límite:**

- diferencia entre conjunto, patrón geométrico y pernos instalados;
- pernos con geometrías, materiales o longitudes diferentes en el mismo conjunto;
- piezas compartidas por varias placas;
- sustitución de un perno sin sustituir el conjunto completo.

### Grupo 2 — Punto de apoyo de equipo

**Otros nombres o sinónimos:** punto de soporte, support point, punto de entrega de
cargas. Los términos pueden representar conceptos diferentes y deben contrastarse.

**Grupo donde apareció:** 2; se relaciona especialmente con 4, 6, 7 y 8.

**Fuente o ejemplo de uso:** información recibida del modelo del equipo o del modelo
estructural para situar su interfaz con la obra civil.

**¿Qué representa?**  
Localización o interfaz mediante la cual un equipo se apoya, se conecta o comunica
acciones a la estructura civil.

**Naturaleza provisional:** espacial e informativa; podría representar también una
interfaz funcional. No se presupone que sea una pieza física.

**¿Por qué necesitamos conocerlo?**  
Permite ubicar apoyos, relacionar el equipo con elementos civiles y asociar acciones
sin incorporar necesariamente el modelo interno completo del equipo.

**¿Parece necesitar identidad propia? ¿Por qué?**  
Por determinar. Puede necesitar una referencia estable si recibe cargas, se revisa o
se intercambia entre aplicaciones; quizá baste una posición perteneciente al equipo
si no tiene ciclo de vida independiente.

**¿Puede existir de forma independiente o forma parte de otro concepto?**  
Probablemente pertenece a la interfaz o al equipo referenciado, pero puede
corresponder a una placa base, un soporte estructural o varios elementos físicos.

**Relaciones conocidas, expresadas con verbos:**

- pertenece o referencia a un equipo;
- se localiza mediante un sistema de coordenadas;
- corresponde a uno o más elementos de apoyo físicos;
- recibe o entrega acciones;
- puede ser representado mediante un punto, una línea o una superficie.

**Relación conocida con Footings:** posible entrada estructural equivalente o
relacionada con `Support`; no debe asumirse que ambos conceptos sean idénticos.

**Dudas y casos límite:**

- un único apoyo representado por varios pernos o varias superficies;
- cambio de coordenadas sin cambio de identidad;
- diferencia entre punto geométrico, interfaz mecánica y origen de una carga;
- ownership cuando la información procede de otra disciplina.

### Grupo 6 — Caso de carga

**Otros nombres o sinónimos:** load case; hipótesis de carga. Debe comprobarse si
«hipótesis» incluye condiciones adicionales y no es un sinónimo exacto.

**Grupo donde apareció:** 6; se relaciona con elementos descubiertos por todos los
grupos.

**Fuente o ejemplo de uso:** modelos de análisis estructural y Footings; situación
que agrupa acciones compatibles para su análisis.

**¿Qué representa?**  
Contexto analítico que organiza una o más acciones bajo un significado y unas
condiciones determinados.

**Naturaleza provisional:** analítico e informativo; no físico.

**¿Por qué necesitamos conocerlo?**  
Permite interpretar las acciones, combinarlas, intercambiarlas y asociar resultados
con las hipótesis bajo las que fueron calculados.

**¿Parece necesitar identidad propia? ¿Por qué?**  
Probablemente sí dentro de un modelo analítico: debe poder nombrarse, referenciarse
desde combinaciones y conservar trazabilidad. Queda por determinar el alcance de esa
identidad entre aplicaciones y revisiones.

**¿Puede existir de forma independiente o forma parte de otro concepto?**  
Pertenece a algún modelo o contexto de análisis. Agrupa acciones y puede participar
en varias combinaciones.

**Relaciones conocidas, expresadas con verbos:**

- agrupa acciones;
- pertenece a un modelo analítico;
- participa en combinaciones;
- produce o contextualiza resultados;
- puede derivar de información de equipos, estructuras u otras disciplinas.

**Relación conocida con Footings:** entrada necesaria para organizar acciones y
combinaciones; Footings puede transformar o propagar sus acciones sin ser propietario
del caso original.

**Dudas y casos límite:**

- diferencia entre caso, hipótesis, grupo y combinación;
- acciones procedentes de varios modelos o fuentes;
- conservación de identidad cuando cambia una acción;
- caso importado frente a caso creado específicamente para Footings.

## 7. Ejemplos breves para los demás grupos

Estos ejemplos indican qué clase de respuesta se espera. Para incorporarlos como
conceptos deberán completar la plantilla del apartado 5.

| Grupo | Concepto | Qué debería describir | Duda que conviene conservar |
|---|---|---|---|
| 1 | Pipe rack | finalidad, estructura concreta, módulos y elementos que lo componen | tipo de estructura frente a instancia y módulo individual |
| 3 | Viga | función, composición, conexiones y pertenencia a una estructura | elemento físico frente a eje geométrico y barra analítica |
| 5 | Estrato de terreno | extensión, clasificación, investigación y parámetros asociados | estrato real frente a interpretación y valores adoptados |
| 7 | Barra analítica | nodos, propiedades, condiciones y elemento físico representado | correspondencia uno a uno o varios a varios con elementos físicos |
| 8 | Sistema de coordenadas local | origen, orientación, sistema padre y objetos posicionados | si cambiar la transformación cambia el sistema o solo su estado |

## 8. Aspectos transversales

No se crean grupos independientes para estos aspectos. La plantilla obliga a
considerarlos al describir conceptos de cualquier grupo:

- identidad y ciclo de vida;
- partes, conjuntos y relaciones;
- materiales y especificaciones;
- geometría, placement y coordenadas;
- representación física y analítica;
- fuente, ownership y procedencia;
- alternativas, revisiones y estados;
- relación con Footings y otras aplicaciones.

Si uno de estos aspectos acumula suficiente vocabulario y problemas propios, podrá
separarse como nuevo grupo explicando el motivo.

## 9. Vocabulario provisional de relaciones

Footings demuestra que varias relaciones visualmente parecidas tienen significados
distintos. Durante la captura deben utilizarse verbos concretos y evitar «está
relacionado con» cuando sea posible.

| Verbo provisional | Pregunta que ayuda a responder |
|---|---|
| contiene / posee | ¿Determina lifecycle u ownership? |
| está compuesto por | ¿Describe partes de un todo físico o lógico? |
| apoya sobre / soporta | ¿Existe contacto o función portante? |
| conecta con | ¿Une elementos sin que uno sea propietario del otro? |
| entrega acciones a | ¿Existe una asignación estructural explícita? |
| transmite acciones a | ¿Es una relación declarada o un recorrido calculado? |
| representa | ¿Vincula un objeto físico con una representación? |
| deriva de | ¿Expresa procedencia, copia, alternativa o revisión? |
| referencia | ¿Apunta a información cuyo ownership está fuera del contexto? |

La lista crecerá al encontrar relaciones reales. No se elegirá todavía una relación
universal ni cardinalidades definitivas.

## 10. Uso de Footings durante el inventario

Footings se revisará en tres capas:

1. **Vocabulario:** elementos, subentidades, inputs, resultados y configuraciones ya
   identificados.
2. **Relaciones:** ownership, parent físico, asignación estructural, endpoints y
   propagación calculada.
3. **Límites:** conceptos propios de una solución y cálculo de cimentaciones frente a
   conceptos potencialmente compartidos con el dominio civil.

Las decisiones de Footings se registrarán como evidencia. No se elevarán
automáticamente a decisiones del dominio civil, especialmente cuando dependan del
agregado `FoundationDesign` o de restricciones propias de la aplicación.

## 11. Reparto inicial posible

Los ocho grupos no implican ocho personas ni propietarios permanentes. Un posible
reparto inicial entre cuatro desarrolladores es:

| Frente | Grupos de exploración |
|---|---|
| 1 | Tipos de estructuras + elementos de superestructura |
| 2 | Cimentación y subestructura + terreno y geotecnia |
| 3 | Equipos e interfaces + coordenadas y representación |
| 4 | Acciones y cargas + modelo analítico y resultados |

Las coincidencias son esperables. Cada frente registra su perspectiva y la revisión
conjunta consolida posteriormente los conceptos.

## 12. Consolidación de la primera ronda

Cuando los ocho grupos hayan aportado conceptos:

1. reunir sinónimos sin borrar los términos utilizados por las fuentes;
2. separar homónimos cuando una palabra exprese significados diferentes;
3. marcar conceptos presentes en varios grupos;
4. revisar si la naturaleza provisional sigue siendo adecuada;
5. extraer y comparar los verbos de relación utilizados;
6. señalar conceptos externos que solo necesiten una referencia;
7. escoger los conceptos que requieren análisis ampliado;
8. comprobar el inventario con uno o más casos reales.

La primera ronda estará terminada cuando exista cobertura inicial de los ocho
grupos y el equipo pueda explicar los principales huecos y ambigüedades. No exige
haber encontrado todos los conceptos ni haber definido entidades canónicas.
