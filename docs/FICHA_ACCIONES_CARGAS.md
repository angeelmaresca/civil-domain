# Ficha — Acciones y cargas

> **Status:** DRAFT
> **Editable:** sí; ficha individual de preparación para la primera iteración
> **Document owner:** Miguel
> **Canonical for:** —
> **Sources:** [`FIRST_ITERATION.md`](FIRST_ITERATION.md) (foco "Miguel — Acciones y cargas"), batería común de preguntas y conversación de trabajo
> **Supersedes:** —
> **Last reviewed:** 2026-09-11

## Nota de alcance

Esta es la ficha individual de Miguel para el foco "Acciones y cargas" de
la primera iteración del equipo. Es una hipótesis `DRAFT`, construida
pregunta a pregunta sobre un ejemplo concreto (un depósito `EQ-101`); no
es una definición aprobada del dominio. Se aportará junto con las fichas
de Alberto (conexiones), Luis (zapata) y Ángel (elemento estructural) en
la reunión de contraste que describe `FIRST_ITERATION.md`, sección 7.

## 1. Mapa conceptual y ejemplo mínimo

Equipo `EQ-101` apoyado sobre la estructura soporte `ST-01` (viga `B-101` +
columna `C-101`), con cimentación mediante placa base, grout, pedestal
`PD-101` y zapata `F-101`.

```text
Equipo EQ-101
└── Interfaz de apoyo IF-EQ101-01 (contacto con la estructura)
        │
        ▼
   Acción ACC-EQ101-V (fuerza vertical, peso operativo)
        │
        ├── pertenece a LoadCase LC-LLENO          (depósito lleno)
        ├── pertenece a LoadCase LC-VACIO          (depósito vacío, peso propio)
        │
        ▼
   Estructura soporte ST-01 (viga B-101, columna C-101)
        │
        ├── AnalyticalModel AM-NODO (si IF-EQ101-01 coincide con la intersección viga-columna)
        │     └── AppliedLoad: ACC-EQ101-V -> Nodo N-05 (fuerza puntual)
        │
        └── AnalyticalModel AM-BARRA (si cae en un punto intermedio de B-101)
              └── AppliedLoad: ACC-EQ101-V -> Barra B-101 en posición x (fuerza puntual)
```

Ideas que debe transmitir este mapa, sin proponer todavía tablas ni clases:

- `EQ-101` e `IF-EQ101-01` son objetos físicos.
- `ACC-EQ101-V` es un objeto de otra naturaleza: sin geometría propia,
  con magnitud, dirección y procedencia.
- `LoadCase` agrupa acciones; una combinación agruparía varios casos, y
  una envolvente derivaría de varias combinaciones. Ninguno de los tres es
  la acción en sí.
- La relación acción → modelo analítico es explícita (`AppliedLoad`) y
  puede repetirse para varios modelos sin duplicar la acción.
- La zapata no aparece en este recorrido: la acción nunca se guarda como
  propiedad suya.

## 2. Enfoque: de lo concreto a lo abstracto

Esta ficha avanza deliberadamente en cuatro capas, de lo más concreto a lo
más abstracto:

1. el **objeto físico real** — algo que se puede señalar con el dedo (el
   equipo, su interfaz de apoyo);
2. el **concepto de acción** — algo que no tiene forma propia pero sí
   dirección y magnitud (la fuerza que el equipo transmite);
3. su **agrupación** — una construcción mental para diseñar con seguridad
   (caso de carga, combinación, envolvente), que ya no describe un hecho
   físico sino una manera de razonar sobre varios hechos a la vez;
4. su **aplicación en un modelo de cálculo** — algo que depende del
   programa y del propósito del análisis (nodo, superficie, elemento).

Es el mismo movimiento que hace IFC: no confunde el objeto, la relación y
la propiedad. Este frente añade una cuarta capa propia, la **vista
analítica**, que tampoco debe confundirse con las tres anteriores. El
error que esta ficha intenta evitar en cada pregunta es precisamente
colapsar estas capas entre sí — por ejemplo, guardar el valor de una acción
como si fuera una propiedad fija del objeto físico que la recibe.

## 3. Batería de preguntas

Se completa empezando por el objeto físico de origen (bloque A) y
avanzando después hacia la Acción como concepto propio (bloques E y F,
principalmente), que son los prioritarios de este foco.

### Bloque A — Realidad, significado e identidad (objeto físico de origen)

**A.1 — ¿Qué objeto físico concreto estamos observando?**

`EQ-101`: un depósito que contiene líquido, apoyado sobre la estructura
soporte `ST-01` mediante 4 patas. Esta ficha se centra en una única
interfaz de apoyo concreta, `IF-EQ101-01` (una de esas 4 patas), como
origen del paquete de acciones estudiado — no en las 4 a la vez.

**A.2 — ¿Qué función cumple y qué lo diferencia de elementos con una forma parecida?**

`EQ-101` alimenta a otro equipo aguas abajo (función de depósito de
alimentación). Lo que lo diferencia, de cara a las acciones que transmite,
es que su interfaz de apoyo no tiene un único peso fijo: transmite dos
estados claramente distintos — depósito vacío (peso propio) y depósito
lleno (peso propio + peso del líquido almacenado). Para esta primera
vuelta se deja fuera cualquier otra particularidad (presión interna,
dinámica del líquido/sloshing); el ejemplo se mantiene simple a propósito.

**A.3 — ¿Dónde empieza y termina? ¿Qué queda expresamente fuera?**

Frontera de `EQ-101`:

- **Dentro:** la envolvente física del depósito junto con su interfaz de
  apoyo `IF-EQ101-01`, tratada como parte del depósito como conjunto.
- **Dentro, como propiedad (opcional, fuera del foco de esta ficha):** el
  tipo de líquido de diseño — densidad, corrosividad, normativa
  aplicable. No varía con el tiempo, es especificación técnica del
  depósito, no origen de una acción.
- **Fuera:** la estructura soporte `ST-01` — pertenece a otro dominio (el
  elemento estructural físico).
- **Fuera:** la masa/peso del líquido *actualmente* contenido en un
  instante dado. No es una propiedad del depósito: es precisamente el
  dato de entrada que origina la Acción estudiada en esta ficha.

**Justificación:** si el peso del líquido contenido se tratara como
propiedad del depósito, la identidad de `EQ-101` cambiaría — o quedaría
ambigua — cada vez que varía su nivel de llenado. Es el mismo problema que
el diseño frágil ya identificado para el pedestal (guardar `loadN` como
campo fijo de la zapata, `FIRST_ITERATION.md` 6.5): mezcla algo estable
(la identidad del objeto) con algo variable (una acción). Mantener el peso
del líquido fuera de la frontera física permite que `EQ-101` conserve una
única identidad estable mientras origina acciones distintas (`LC-VACIO`,
`LC-LLENO`) según su estado en cada momento — exactamente la separación
entre objeto físico y acción que este frente debe demostrar.

**A.4 — ¿Necesita identidad propia? ¿Qué debe poder cambiar sin perder esa identidad?**

Sí, `EQ-101` necesita un identificador propio y estable (su TAG), para
poder referenciarse de forma consistente desde acciones, revisiones y
modelos distintos.

Puede cambiar **sin** perder identidad:

- el nivel de llenado (vacío/lleno), ya establecido en A.3;
- dimensiones, material o tipo de soportes entre revisiones de diseño —
  estas características pertenecen al tipo/especificación de cada
  revisión, no a la identidad de la ocurrencia.

Rompería la identidad:

- sustituir físicamente `EQ-101` por un depósito distinto (otro TAG); es
  decir, un reemplazo real del equipo, no una revisión de su diseño.

**A.5 — ¿Puede existir de forma independiente o depende del lifecycle de otro objeto?**

- `EQ-101` vs `IF-EQ101-01`: no aplica como dependencia entre dos objetos
  — desde A.3, la interfaz de apoyo forma parte de la frontera física de
  `EQ-101`, así que comparte necesariamente su mismo lifecycle.
- `EQ-101` vs `ST-01`: **lifecycles independientes**. `EQ-101` puede
  especificarse, diseñarse y fabricarse sin conocer aún qué estructura lo
  soportará; su identidad no depende de dónde se coloque. La relación no
  es simétrica, sin embargo: mientras `EQ-101` no depende de `ST-01`, el
  diseño de la estructura sí necesita conocer las acciones que `EQ-101`
  transmite para poder dimensionarse correctamente.

**Hallazgo relevante:** `EQ-101` y `ST-01` no dependen existencialmente
uno del otro, pero sí existe una dependencia de *información* entre
ambos — y esa dependencia de información es precisamente el papel que
cumple la Acción: un puente entre dos lifecycles independientes, sin que
ninguno de los dos objetos dependa físicamente del otro para existir.

*Cierre del bloque A: pasamos al bloque E (conexiones, interfaces y
acciones), el núcleo real de este frente.*

### Bloque E — Conexiones, interfaces y acciones

**E.19 — ¿Con qué objetos se conecta, apoya, une o entra en contacto?**

`IF-EQ101-01` (la pata de `EQ-101`) apoya sobre la viga física `B-101`, en
un punto concreto a lo largo de su longitud. Es un contacto físico real,
no todavía una idealización analítica — un "nodo" no existe a este nivel;
eso pertenece al bloque F.

**E.20 — ¿La conexión es un punto, línea, superficie o volumen o conjunto de componentes?**

Se idealiza como un contacto **puntual** (una pata concentrada, sin una
placa de apoyo con área significativa). Es una simplificación deliberada
del caso: si `IF-EQ101-01` fuera una placa de apoyo amplia, habría que
tratarla como un contacto superficial, no puntual.

*(Nota de vocabulario: aquí hablamos de la geometría física del contacto,
no todavía de "carga puntual" como tal — esa palabra pertenece al bloque
F. Pero como el contacto es puntual, es coherente que en el bloque F la
acción se represente de forma natural como una fuerza puntual, sin
necesidad de repartirla en una superficie.)*

**E.21 — ¿La relación necesita datos propios — posición, rigidez, holgura, capacidad, estado o revisión?**

- **Posición:** sí — la relación debe especificar en qué punto de la
  longitud de `B-101` se aplica la carga; es un dato de la conexión, no
  del depósito ni de la viga por separado.
- **Rigidez:** apoyo simple/articulado que solo transmite fuerza vertical,
  sin restricción de giro ni transmisión de momento (equivalente a una
  "rótula" o release de momento).
- **Holgura:** no aplica — contacto directo, sin apoyo deslizante.
- **Capacidad:** no se almacena en la conexión. Comprobar si la viga
  admite esa carga es un resultado del análisis estructural (frente de
  Ángel), no un dato propio de la relación.

**E.22 — ¿Qué acciones recibe, genera o transmite? ¿Cuál es su origen y objetivo?**

- **Genera:** `EQ-101` genera una fuerza vertical puntual, correspondiente
  a aproximadamente 1/4 del peso total del depósito (por simetría, al
  repartirse entre sus 4 patas), en cada uno de sus dos estados
  (`LC-VACIO` / `LC-LLENO`). Se mantiene el alcance de una única pata,
  no el reparto completo entre las 4.
- **Transmite:** a través de `IF-EQ101-01`, aplicada en el punto concreto
  donde esa pata apoya sobre `B-101` — no en el centroide del depósito
  (eso correspondería al peso total repartido entre las 4 patas, fuera
  del alcance de esta ficha).
- **Origen:** peso propio del depósito vacío, o peso propio + líquido
  almacenado cuando está lleno.
- **Objetivo:** entregar a la viga el dato de carga de entrada necesario
  para su dimensionamiento. El caso crítico para diseño es `LC-LLENO`
  (mayor peso) — la misma idea de "envolvente" vista al principio, aquí
  trivial por haber solo dos casos. El esfuerzo interno que esa carga
  produce en la viga (momento, cortante, axil) es un **resultado** del
  análisis, no parte de esta acción; pertenece al frente del elemento
  estructural.

*Cierre del bloque E: pasamos al bloque F (modelo analítico), donde
reutilizamos directamente lo ya avanzado sobre nodo vs. barra.*

### Bloque F — Modelo analítico

**F.23 — ¿Necesita representación analítica para algún propósito concreto?**

Sí. Se necesita para dimensionar los perfiles de la estructura, calcular
su resistencia según normativa y comprobar que cumple. Sin la
representación analítica, el peso del depósito no podría traducirse en un
dato utilizable por el proceso de diseño estructural.

**F.24 — ¿Qué nodos, barras, superficies, sólidos, apoyos o resortes la representan?**

Dos representaciones alternativas, según dónde caiga físicamente
`IF-EQ101-01` sobre `B-101`:

1. **Modelo A (nodo):** si coincide exactamente con la intersección
   viga-columna, se representa como fuerza puntual aplicada en un
   **nodo** del modelo.
2. **Modelo B (barra):** si cae en un punto intermedio de la viga (lo más
   habitual), se representa como fuerza puntual aplicada sobre un
   **elemento barra**, en una posición concreta de su longitud.

**F.25 — ¿Podría representarse de formas diferentes en modelos analíticos distintos?**

Sí. `AM-NODO` y `AM-BARRA` no son la misma representación con otro
nombre: son dos idealizaciones genuinamente distintas del mismo hecho
físico, y la elección depende de dónde caiga la pata respecto a la malla
de nodos del modelo. Además, esto puede depender del propio programa de
cálculo: dos programas distintos (p. ej. STAAD y SAP2000) podrían
discretizar la viga con nodos en posiciones distintas, de modo que lo que
en uno es "nodo" podría ser "punto intermedio de barra" en otro.

**F.26 — ¿La correspondencia físico–analítica es uno a uno, uno a varios o varios a uno?**

Depende del nivel en el que se mire:

- **Dentro de un mismo modelo analítico:** uno a uno. Una carga puntual
  como `ACC-EQ101-V` se aplica a un único elemento (un nodo, o un punto
  concreto de una barra) — nunca se reparte simultáneamente entre varios
  elementos dentro del mismo modelo. Eso sería propio de otro tipo de
  acción (distribuida o superficial), que sí podría abarcar varias partes
  estructurales a la vez.
- **Entre modelos analíticos alternativos:** uno a varios. La misma acción
  física puede tener varias representaciones posibles según el modelo
  (`AM-NODO`, `AM-BARRA`), pero nunca más de una a la vez dentro de un
  mismo modelo.

**F.27 — ¿Qué información pertenece al modelo analítico y no al objeto físico?**

- **Conectividad de malla** (qué barra conecta con qué nodo): construcción
  propia del modelo, no existe como tal en la realidad física.
- **Asignación a un nodo o barra concretos** (y la posición local dentro
  de esa barra): depende del mallado de cada modelo, cambia entre
  `AM-NODO` y `AM-BARRA`.
- **Esfuerzo interno resultante en la viga** (momento, cortante, axil):
  resultado del análisis, no un dato de entrada.

**No pertenece a esta lista:** la magnitud de la carga. Su valor no
cambia según el modelo elegido — es información de la Acción
(`ACC-EQ101-V`), que existe antes de decidir su representación analítica.

*Cierre del bloque F: quedan cerradas las preguntas numeradas
prioritarias. Queda una pregunta específica del foco de este frente que
aún no hemos resuelto de forma explícita: sistema de coordenadas y
convenio de signos.*

### Pregunta adicional del foco — sistema de coordenadas y convenio de signos

Para este ejemplo: **eje Z del sistema global del proyecto, positivo
hacia arriba** (convención habitual en muchos programas de cálculo). El
peso del depósito, al actuar en sentido de la gravedad (hacia abajo), se
expresa con **signo negativo** en `Z`.

**Hallazgo a vigilar (no cerrado, depende del programa):** el convenio de
signos y el sistema de referencia no son universales — dependen del
programa de cálculo, y cada usuario decide además si trabaja en
coordenadas locales o globales dentro de su modelado. Para que una Acción
sea trasladable entre modelos y programas distintos, debería declarar
explícitamente en qué sistema y con qué signo fue definida; de lo
contrario, dos modelos podrían combinar mal los mismos valores.

## 4. Conceptos candidatos (hasta 5)

1. **Acción** — objeto con identidad propia, independiente del objeto
   físico que la origina y del modelo analítico que la consume.
2. **Acción como puente de información** entre dos objetos con lifecycles
   independientes (`EQ-101` y `ST-01` no dependen existencialmente uno del
   otro, pero sí hay una dependencia de información entre ambos).
3. **Posición de aplicación** como dato propio de la conexión, no del
   objeto físico ni de la acción en sí.
4. **Correspondencia acción–analítico uno a varios entre modelos
   alternativos**, pero uno a uno dentro de un mismo modelo.
5. **Convenio de signos y sistema de coordenadas declarados
   explícitamente** en la Acción, por depender del programa de cálculo
   usado en cada caso.

## 5. Tres dudas para discutir en equipo

1. En A.4 decidimos que `EQ-101` conserva su identidad aunque cambien
   dimensiones, material o soportes entre revisiones — pero es una
   convención, no una regla universal. ¿Bajo qué circunstancias el
   equipo consideraría que un cambio sí merece un TAG nuevo?
2. ¿Dónde debe vivir de forma persistente el sistema de coordenadas y
   convenio de signos de una Acción — declarado en la propia Acción, o
   dependiente de lo que asuma cada modelo en cada momento?
3. Elegimos estudiar una única pata (1/4 del peso) en vez del reparto
   completo entre las 4. ¿Cuándo conviene ampliar el alcance de una
   acción "por apoyo individual" al reparto entre varios apoyos de un
   mismo objeto?

## 6. Simplificación válida vs. diseño frágil

**Simplificación que podría ser válida:** tratar el apoyo del depósito
como una única fuerza puntual equivalente a 1/4 del peso total (por
simetría), en vez de modelar las 4 patas con su posible reparto desigual.
Válida mientras el depósito sea razonablemente simétrico y esté centrado
sobre sus apoyos; deja de serlo si hay excentricidad relevante (llenado
no uniforme, geometría asimétrica) que reparta la carga de forma
desigual entre patas.

**Diseño frágil (a evitar):**

```text
Viga B-101
- cargaDeposito = 2500 kg
```

Mezcla en un único campo: el valor de la acción, sin indicar a qué caso
pertenece (`LC-VACIO` o `LC-LLENO`), sin convenio de signos explícito,
sin origen registrado (¿por qué 2500 kg?), y sin distinguir si es un dato
de entrada o ya una combinación. Es el mismo problema de fondo que el
ejemplo de la zapata (`FIRST_ITERATION.md`, 6.5): convierte una Acción
—con su propia identidad, agrupación y procedencia— en un número suelto
pegado al objeto físico que la recibe.
