# Notas de Ángel — iteración 04

> **Status:** DRAFT
> **Editable:** sí; notas personales de Ángel abiertas durante la sesión de estudio
> **Document owner:** Ángel
> **Canonical for:** —; conserva conclusiones provisionales y dudas de esta sesión, sin sustituir las fuentes propietarias
> **Sources:** conversación de estudio con Ángel del 28 de septiembre de 2026; [`ENUNCIADO.md`](ENUNCIADO.md); [`ANALISIS_AGENTE.md`](ANALISIS_AGENTE.md)
> **Supersedes:** —
> **Last reviewed:** 2026-09-29

## Propósito

Recoger las conclusiones provisionales y las preguntas que surjan durante el
estudio de la cuarta iteración. Estas notas no convierten las propuestas en
acuerdos del equipo ni modifican por sí solas las definiciones propietarias.

## 1. Cobertura física y analítica de una ocurrencia

### Conclusiones provisionales

- Una ocurrencia puede estar representada tanto en maqueta como en un modelo
  analítico. Una columna puede aparecer como elemento físico en SP3D y como
  idealización analítica en STAAD.
- Una ocurrencia puede estar representada en maqueta y no tener una
  idealización analítica directa. Una barandilla puede existir en SP3D sin
  necesitar una barra, placa u otro objeto equivalente en STAAD.
- La ausencia de una idealización analítica directa no implica por sí sola un
  error. Debe distinguirse si esa representación es `no aplicable`, está
  `pendiente`, falta de forma injustificada o ha sido sustituida por una
  consecuencia analítica trazable.
- También puede existir el caso inverso: una idealización analítica de
  prediseño sin representación física todavía en maqueta.
- La alineación entre representación física y analítica no exige igualdad
  geométrica. Debe evaluarse según el propósito, la versión y los criterios
  de correspondencia aplicables.

### Duda terminológica

La expresión «estado válido» resulta ambigua porque puede confundirse con
«cálculo aprobado» o «diseño técnicamente validado». Conviene precisar si se
quiere expresar:

- cobertura suficiente para un propósito o hito;
- coherencia conocida entre representaciones;
- aceptación humana de una versión;
- o validación técnica del cálculo.

## 2. Elementos sin idealización analítica directa que producen efectos

### Ejemplo de trabajo: barandilla

Una barandilla puede no estar modelada como objeto analítico en STAAD y, sin
embargo, producir efectos que deben entrar en el cálculo. La carga no se
considera la representación analítica de la barandilla: representa una
consecuencia suya sobre el sistema resistente.

```text
Barandilla BR-01 @ estado R05
├── está representada en → SP3D P17 / objeto BR-438
├── puede originar → Acción A-BR01-PESO
├── transmite acciones a → Viga B-101
└── A-BR01-PESO se aplica en → STAAD S12 / AppliedLoad AL-204
```

Esta separación permite registrar que la barandilla:

- existe en la maqueta;
- no tiene una idealización analítica directa;
- sí tiene consecuencias consideradas en el análisis;
- y debe provocar una revisión de esas consecuencias cuando cambie un dato
  relevante de su estado.

### Distinciones necesarias

«La barandilla induce cargas» puede ocultar fenómenos diferentes:

- su peso propio puede **originar** una acción permanente;
- una acción de uso puede originarse en una situación de diseño y ser
  **recibida y transmitida** por la barandilla;
- el viento puede originarse externamente, depender de la geometría expuesta
  y transmitirse a través de sus apoyos.

No conviene reducir todos estos casos a una única relación genérica
`induce carga`. Como vocabulario de trabajo se distinguen:

- `origina acción`, para identificar la fuente física o de diseño;
- `transmite acciones a`, para describir el recorrido físico previsto;
- `se aplica en modelo como`, para vincular una acción con una aplicación
  concreta en una revisión analítica;
- `se basa en estado`, para conservar qué versión de la ocurrencia sustentó
  la determinación de la acción.

`transmite acciones a` ya figura como relación candidata en
[`RELATIONSHIPS.md`](../RELATIONSHIPS.md#familias-iniciales). Las demás
expresiones son hipótesis de esta sesión y todavía requieren contraste.

### Trazabilidad mínima propuesta

Para afirmar que el efecto de un elemento sin idealización directa está
cubierto analíticamente habría que poder navegar, al menos, por:

```text
estado de la ocurrencia
→ acción con procedencia y contexto
→ aplicación analítica
→ modelo y revisión receptores
```

La aplicación concreta debería conservar, cuando proceda, el objeto o zona
analíticos receptores, la forma de aplicación, magnitud, dirección, unidades,
convenio de signos y caso de carga.

## 3. Cambio y discrepancia

Un cambio en la barandilla no debe generar automáticamente una discrepancia
analítica. Primero debe evaluarse si afecta a alguna acción: por ejemplo, un
cambio de masa, longitud, superficie expuesta, posición o apoyos.

- Si el cambio no afecta a las acciones, debería poder registrarse una
  aceptación sin modificación del modelo receptor.
- Si afecta, la acción y sus aplicaciones analíticas deben quedar pendientes
  de revisión.
- La mera ausencia de un objeto equivalente en STAAD no es una discrepancia
  cuando la idealización directa se declaró no aplicable.
- Sí existe un problema si era obligatorio considerar un efecto y no hay
  acción asociada, si la acción se basa en un estado obsoleto o si su
  aplicación analítica ya no representa adecuadamente el efecto.

## 4. Preguntas abiertas

1. ¿`origina acción` debe relacionar la acción con la ocurrencia completa, con
   un estado concreto o con una interfaz física identificada?
2. ¿Cómo se registra una acción agregada que procede de varias barandillas u
   otros elementos secundarios sin inventar una correspondencia uno a uno?
3. ¿Quién decide que una idealización analítica directa es `no aplicable` y
   para qué modelo, propósito y revisión vale esa decisión?
4. ¿Qué cambio del elemento invalida automáticamente una acción y cuál solo
   solicita revisión humana?
5. ¿Cómo se representa que una misma acción se aplica de formas distintas en
   varios modelos analíticos?
6. ¿Qué término sustituye a «estado válido» para diferenciar cobertura,
   coherencia, aceptación y validación técnica?

## 5. Representación y versiones concretas

### Conclusiones provisionales

- `Representación` designa la línea que mantiene continuidad dentro de un
  contexto y para un propósito determinados. Por ejemplo: «representación
  física de `C-101` en SP3D» o «idealización de `C-101` en el modelo global
  de STAAD».
- `SnapshotDeRepresentación` designa lo que esa representación afirma en una
  revisión concreta de su fuente. Conserva el contenido recibido sin
  sobrescribir retrospectivamente las revisiones anteriores.
- `ReferenciaExterna` conserva el identificador contextual de cada objeto en
  la aplicación y revisión de origen, como `C-44` en SP3D o `barra 120` en
  STAAD. Un cambio de referencia externa no implica necesariamente una nueva
  representación persistente ni una nueva ocurrencia de diseño.
- Una representación puede cambiar su geometría, propiedades, nivel de
  detalle o topología entre snapshots y conservar su continuidad. Por
  ejemplo, una columna puede estar idealizada mediante una barra en `STAAD
  S05` y mediante dos barras en `STAAD S06`.

```text
OcurrenciaDeDiseño C-101
└── Representación analítica en el modelo global de STAAD
    ├── Snapshot S05 / barra 120
    ├── Snapshot S06 / barras 120 y 121
    └── Snapshot S07 / barra 305
```

La ocurrencia sigue siendo el individuo físico; la representación expresa una
vista parcial con propósito; el snapshot fija el contenido de una revisión; y
la referencia externa identifica objetos dentro de esa fuente.

### Convención terminológica para esta sesión

Ángel considera adecuado utilizar nombres en español durante el estudio para
favorecer la comprensión compartida. En una fase posterior deberá estudiarse
un vocabulario equivalente en inglés, especialmente antes de adoptar nombres
de intercambio o implementación. Esta preferencia no fija todavía las
traducciones ni sustituye una futura decisión del equipo.

Como vocabulario provisional se emplean:

- `OcurrenciaDeDiseño`;
- `Representación`;
- `SnapshotDeRepresentación`;
- `ReferenciaExterna`;
- `EstadoDeDiseño`;
- `Discrepancia`.

Queda pendiente decidir si «snapshot» debe mantenerse como préstamo técnico o
sustituirse también por un término español, por ejemplo «captura» o «estado
registrado de la representación».

## 6. Frontera entre acción, hecho y decisión

### Corrección de la sesión

Se descarta la conclusión anterior de que dar de alta una
`OcurrenciaDeDiseño` sea siempre una decisión de dominio. Esa formulación
convertiría indebidamente cada acción del sistema en una decisión.

Como criterio provisional se distinguen:

- **acción u operación:** alguien solicita o ejecuta un cambio, por ejemplo
  registrar una columna o importar un snapshot;
- **hecho:** algo ya ocurrió y puede quedar trazado, por ejemplo
  `OcurrenciaRegistrada` o `RepresentaciónActualizada`;
- **decisión:** un responsable resuelve una cuestión con alternativas
  relevantes utilizando autoridad, criterio y evidencia.

Que una persona haya elegido ejecutar una acción no basta para convertirla en
una `Decisión` del modelo de dominio.

### Alta ordinaria y decisión de identidad

El alta ordinaria de una ocurrencia puede modelarse como una acción seguida de
un hecho:

```text
registrar una columna nueva
→ OcurrenciaDeDiseño registrada
```

No necesita una entidad de decisión adicional si no existe una incertidumbre
del dominio que resolver. Deben conservarse autor, fecha y procedencia, pero
eso puede formar parte de la trazabilidad de la operación o del evento.

Sí puede aparecer una decisión cuando existe una ambigüedad real de identidad:

```text
objeto C-44 importado de SP3D
→ ¿continúa una ocurrencia existente o es una ocurrencia nueva?
→ decisión de identidad con responsable, criterio y evidencia
→ enlace a la ocurrencia existente o alta de una nueva
```

En este caso la decisión no es «crear una ocurrencia», sino resolver qué
identidad corresponde al candidato. El alta puede ser una consecuencia de esa
decisión.

### Caso acordado

La resolución de una `Discrepancia` sí es una decisión porque exige determinar
qué significa la diferencia detectada y qué consecuencia procede: aceptar una
divergencia, exigir una corrección, descartarla justificadamente o posponerla.
La detección de la discrepancia es un hecho; su resolución es una decisión.

```text
diferencia detectada
→ Discrepancia abierta
→ evaluación
→ decisión sobre la discrepancia
→ consecuencia y cierre, o aplazamiento
```

### Prueba provisional

Una actuación merece tratarse como decisión del dominio cuando concurren varias
de estas condiciones:

1. existen alternativas defendibles;
2. hace falta una autoridad reconocida para elegir;
3. deben conservarse la justificación y las evidencias;
4. el resultado cambia qué se considera aceptado, aplicable o exigible;
5. la resolución puede discutirse, sustituirse o revocarse;
6. otros procesos necesitan referirse a ella explícitamente.

Si solo interesa saber qué ocurrió, quién lo ejecutó y cuándo, normalmente
basta una operación, un evento o un registro de auditoría.

### Ejemplos para contrastar

| Situación | Clasificación provisional |
|---|---|
| Registrar una columna nueva creada explícitamente | Acción y hecho; no decisión separada por defecto |
| Importar un snapshot de SP3D | Acción y hecho |
| Detectar una diferencia SP3D–STAAD | Hecho que puede abrir una discrepancia |
| Resolver si esa diferencia es admisible | Decisión sobre discrepancia |
| Resolver si dos objetos de fuentes distintas son el mismo individuo | Decisión de identidad |
| Aplicar una regla determinista ya acordada | Ejecución de una regla, no nueva decisión discrecional |
| Determinar que un cambio no requiere recálculo | Decisión cuando exige autoridad técnica y evidencia |
| Aceptar un `EstadoDeDiseño` para un propósito concreto | Decisión de aceptación |

Queda pendiente comprobar con casos reales si la decisión sobre discrepancia,
la decisión de identidad y la aceptación de un estado comparten suficiente
semántica para justificar un concepto común de `Decisión`, sin convertir todas
las acciones en decisiones.

## 7. Estado de diseño y conciliación entre representaciones

### Conclusiones provisionales de Ángel

1. Un `EstadoDeDiseño` aceptado no puede cambiar silenciosamente cuando se
   actualiza una representación o llega un nuevo snapshot.
2. Los estados aceptados son históricos e inmutables. Puede cambiar cuál se
   considera vigente, pero no se reescribe el contenido de un estado anterior.
3. Hace falta un concepto que reúna la comparación entre el estado vigente y
   las distintas fuentes, las diferencias detectadas, las políticas aplicadas
   y las decisiones resultantes. Se usa provisionalmente
   `CasoDeConciliación`; el nombre definitivo queda abierto.

La analogía de trabajo con Git se precisa así:

```text
Repositorio                     OcurrenciaDeDiseño
Ramas                           Representaciones que evolucionan
Commit de una rama              SnapshotDeRepresentación
Commit aceptado en develop      EstadoDeDiseño histórico
HEAD de develop                 EstadoDeDiseño vigente
Pull request                    CasoDeConciliación
Conflicto o check fallido       Discrepancia
Revisión y aprobación           Decisión
Merge                           Nuevo EstadoDeDiseño aceptado
```

La analogía orienta el razonamiento, pero no obliga a copiar la mecánica de
Git. En particular, las representaciones pueden ser abstracciones diferentes
y no siempre es correcto elegir una y sobrescribir las demás.

### `VistaDeCoherencia` no se introduce por ahora

Ángel no ve todavía una responsabilidad distinta que justifique
`VistaDeCoherencia` como concepto del dominio. La comparación calculada puede
mostrarse dentro del `CasoDeConciliación` sin darle identidad ni ciclo de vida
propios.

Solo debería recuperarse el término si aparece una necesidad concreta que el
caso no cubra, por ejemplo una consulta transversal sobre muchos casos o una
captura congelada para auditoría. Hasta entonces, no se añade un concepto por
anticipación.

### Autoridad y políticas

El sistema debe admitir políticas generales y decisiones particulares:

```text
diferencia detectada
→ existe una política aplicable
  ├── sí: la política permite clasificarla o resolverla
  └── no: requiere decisión de un responsable autorizado
```

La autoridad debe expresarse por aspecto, propósito, fase y alcance. No se
debe afirmar simplemente que «SP3D manda sobre STAAD», porque la autoridad
pertenece a un rol o proceso del dominio y la aplicación es la fuente donde
ese responsable mantiene el dato.

Una política candidata debería poder indicar:

- aspecto gobernado —identidad, geometría física, material, comportamiento
  analítico, cargas, conexiones, fabricación—;
- familia de objetos y alcance;
- fase y propósito;
- rol con autoridad;
- representación donde se mantiene el dato;
- representaciones dependientes o receptoras;
- criterio de equivalencia o tolerancia;
- excepciones admitidas;
- y responsable al que se escala un caso no cubierto.

No toda diferencia se resuelve decidiendo qué fuente prevalece:

- una fuente puede ser autoridad sobre un dato que otra replica;
- cada fuente puede gobernar aspectos diferentes;
- dos representaciones pueden diferir deliberadamente por su propósito;
- o puede no existir política suficiente y ser necesaria una decisión para el
  caso concreto.

Queda por concretar quién acepta cada resultado, qué discrepancias bloquean un
nuevo estado y cuáles pueden permanecer abiertas sin impedirlo.

### Flujo conceptual completo

```text
OcurrenciaDeDiseño
└── EstadoDeDiseño vigente e inmutable
         │
         ├── llega un SnapshotDeRepresentación nuevo
         │
         ▼
CasoDeConciliación
├── identifica estado base, snapshots y alcance
├── normaliza unidades, coordenadas y referencias cuando proceda
├── determina qué afirmaciones son comparables
├── detecta diferencias
├── aplica políticas de autoridad, equivalencia y cobertura
├── abre Discrepancias para lo que no puede resolver
└── reúne las decisiones de responsables autorizados
         │
         ├── aceptar con cambios
         │      └── crea un nuevo EstadoDeDiseño
         ├── aceptar sin cambios
         │      └── conserva el estado vigente y registra la evaluación
         ├── exigir corrección
         │      └── espera otro snapshot y vuelve a comparar
         ├── aceptar una divergencia
         │      └── conserva la diferencia y su justificación
         ├── posponer
         │      └── mantiene el caso y las discrepancias pendientes
         └── descartar el caso
                └── conserva el motivo sin alterar el estado
```

El caso debe recordar exactamente qué versiones se compararon. Un snapshot
posterior no reescribe el caso anterior: puede reabrirlo, actualizar su alcance
o iniciar otro caso según el criterio que se acuerde.

### Casuística para explicar al equipo

#### Caso A — fuentes alineadas y sin cambio respecto al estado vigente

`C-101@R03`, SP3D `P13` y STAAD `S06` describen la misma sección y posición
según los criterios aplicables.

- No se abre una discrepancia.
- No se crea otro `EstadoDeDiseño` solo para reflejar que se comparó.
- El caso se cierra como aceptación sin cambios y conserva las versiones
  evaluadas para no repetir la misma revisión.

#### Caso B — cambia la representación, no la definición de diseño

Este caso solo aplica si `C-44` y `COL-87` son identificadores internos de
SP3D, contextualizados por aplicación, modelo y revisión. No aplica si
`COL-87` es la nueva designación de proyecto que el equipo quiere reconocer
en planos, mediciones u otros procesos.

SP3D cambia su identificador técnico externo `C-44` por `COL-87`, o modifica
el nivel de detalle geométrico sin cambiar sección, material, placement,
designación de proyecto ni relaciones relevantes.

- Se conserva la continuidad de la representación y su nueva referencia.
- No cambia el `EstadoDeDiseño`.
- No hay discrepancia si la política reconoce la equivalencia.
- Se registra aceptación sin cambios si el caso requería revisión humana.

Esto no deja desactualizada la información actual. La referencia vigente
`COL-87` se consulta en la representación o en su último snapshot, mientras
que el estado aceptado conserva la definición de diseño. El histórico sigue
mostrando que el snapshot anterior utilizaba `C-44`.

```text
Ocurrencia interna O-017
├── EstadoDeDiseño vigente R03        definición aceptada, sin cambio
└── Representación SP3D
    ├── Snapshot P12 / referencia C-44
    └── Snapshot P13 / referencia COL-87
```

La clasificación cambia si el nombre tiene significado para el dominio:

| Cambio | Tratamiento provisional |
|---|---|
| ID técnico generado o gestionado únicamente por SP3D | Nueva `ReferenciaExterna`; no cambia el estado |
| TAG o código contextual de una aplicación | Referencia externa versionada; evaluar si otra fuente depende de él |
| Designación de proyecto aceptada y utilizada en planos, fabricación o mediciones | Cambio de diseño o de relación versionada; puede exigir nuevo estado |
| ID interno estable de la `OcurrenciaDeDiseño` | No debe cambiar ni reutilizarse |

Queda pendiente decidir si la designación de proyecto pertenece directamente
al `EstadoDeDiseño` o a una relación versionada separada. En ambos casos, si
`COL-87` sustituye de verdad a `C-44` como nombre reconocido por el proyecto,
no debe ocultarse como un simple cambio técnico de SP3D.

#### Caso C — cambio físico aceptable y representaciones alineadas

SP3D propone que `C-101` pase de HEB 300 a HEB 320 y el modelo analítico ya
incorpora una idealización compatible.

- El caso compara ambos snapshots con `R03`.
- La autoridad correspondiente acepta la nueva definición.
- Se crea `C-101@R04`; `R03` permanece intacto.
- La existencia de `R04` no prueba por sí sola que el cálculo esté validado:
  esa validación conserva sus entradas y evidencias propias.

#### Caso D — cambio físico con modelo analítico desactualizado

SP3D propone HEB 320 y STAAD conserva HEB 300.

- Se detecta una diferencia relevante.
- Si la política exige correspondencia, se abre una `Discrepancia`.
- El calculista puede exigir actualizar STAAD, justificar una idealización
  distinta, aceptar que no requiere recálculo o posponer.
- El caso permanece abierto hasta cumplir el criterio de cierre. Debe
  decidirse si esa discrepancia bloquea aceptar `R04` o solo bloquea un
  propósito concreto, como cálculo o fabricación.

#### Caso E — divergencia deliberada entre representaciones

SP3D sitúa la cara o el eje físico real de una columna y STAAD emplea un eje
analítico desplazado con una excentricidad modelada expresamente.

- La diferencia geométrica no obliga a que una fuente sobrescriba a la otra.
- Una política puede declararla compatible si se cumple la correspondencia
  prevista.
- Si no existe política, una decisión puede aceptar la divergencia con su
  justificación y alcance.
- Una decisión particular no se convierte automáticamente en política para
  todos los casos futuros.

#### Caso F — representación ausente por diseño

Una barandilla aparece en SP3D pero no tiene objeto analítico directo en
STAAD. Su peso se relaciona con una acción aplicada al modelo.

- La ausencia no es discrepancia si la cobertura analítica directa está
  declarada como no aplicable y la política exige únicamente sus efectos.
- Sí puede abrirse discrepancia si falta una acción requerida, se basa en un
  estado obsoleto o no existe evidencia de la cobertura acordada.

#### Caso G — no existe política suficiente

Dos fuentes aportan valores distintos y ninguna tiene autoridad previamente
establecida para ese aspecto.

- El sistema no elige automáticamente la más reciente ni la herramienta
  considerada más importante.
- Abre una discrepancia y la asigna al responsable que deba decidir.
- La decisión resuelve ese caso. Si revela un patrón repetible, el equipo
  puede decidir después crear o ajustar una política general.

#### Caso H — cambio aceptado sin modificar al receptor

Estructura publica una nueva versión de cargas, pero cimentación conserva su
versión porque el responsable comprueba que sigue siendo compatible.

- Se registra qué versión proveedora se usó originalmente.
- Se conserva la aceptación posterior frente a la nueva versión.
- No se crea artificialmente una nueva versión de cimentación solo para
  igualar numeraciones.
- Esta aceptación evita nuevas alertas mientras no aparezca otro cambio
  relevante.

### Por qué hace falta cada concepto

| Concepto | Responsabilidad que no debe perderse |
|---|---|
| `OcurrenciaDeDiseño` | Mantener la identidad del individuo físico |
| `EstadoDeDiseño` | Conservar una definición aceptada, histórica e inmutable |
| `Representación` | Mantener una perspectiva parcial con propósito propio |
| `SnapshotDeRepresentación` | Fijar qué afirmó una fuente en una revisión concreta |
| Política de autoridad/coherencia | Resolver casos repetibles sin decisión manual constante |
| `CasoDeConciliación` | Reunir comparación, alcance, políticas, discrepancias y resultado |
| `Discrepancia` | Seguir una diferencia que necesita evaluación o decisión |
| Decisión | Conservar autoridad, alternativa elegida, motivo y evidencia |
| Aceptación sin cambios | Demostrar que una versión nueva fue evaluada aunque el receptor no cambiase |

### Decisiones todavía abiertas

1. Nombre definitivo y alcance exacto de `CasoDeConciliación`.
2. Si un caso se limita a una ocurrencia o puede abarcar conjuntos y muchas
   ocurrencias.
3. Qué diferencias abren discrepancia y cuáles se resuelven por tolerancia o
   equivalencia.
4. Qué roles tienen autoridad por aspecto, fase y propósito.
5. Qué discrepancias bloquean la aceptación de un nuevo estado y para qué
   propósitos.
6. Cuándo un nuevo snapshot reabre un caso anterior y cuándo crea otro.
7. Qué evidencia mínima exige una aceptación sin cambios.

## 8. Varios modelos simultáneamente válidos y conciliación por alcance

### Ampliación aportada por Ángel

El análisis anterior ponía demasiado el foco en una ocurrencia individual y
podía sugerir que existe una única secuencia de modelo por aplicación. Para
una estructura o cimentación pueden coexistir varios modelos con identidad,
propósito y ciclos de revisión independientes:

- un modelo de coordinación física en SP3D;
- un modelo de detalle o fabricación en Tekla;
- un modelo analítico estático en STAAD;
- otro modelo analítico dinámico también en STAAD;
- y otros modelos globales, locales, temporales o especializados.

Dos modelos STAAD pueden ser simultáneamente válidos. El modelo estático y el
dinámico no son necesariamente revisiones sucesivas: son modelos distintos
cuando responden a propósitos, idealizaciones o ciclos de revisión independientes.
Cada uno puede tener después sus propias revisiones. Una hipótesis o un caso de
carga diferente, por sí solo, no obliga a crear otra identidad de modelo.

```text
Modelo analítico estático AM-EST
├── revisión S05
└── revisión S06

Modelo analítico dinámico AM-DIN
├── revisión D02
└── revisión D03
```

`S06` no sustituye a `D03`; ambos pueden ser vigentes para sus respectivos
propósitos. Esta conclusión ya es coherente con la ficha de Ángel de la
primera iteración: una misma aplicación puede mantener varios modelos con
propósito o ciclo de vida independientes.

### Árbol de navegación desde la estructura

```text
Estructura ST-01
│
├── versiones/estados del conjunto
│   ├── ST-01 v04
│   └── ST-01 v05 vigente
│
├── ocurrencias físicas
│   ├── C-101
│   ├── C-102
│   ├── B-101
│   └── BR-01
│
└── modelos asociados
    │
    ├── Modelo físico SP3D COORD
    │   ├── propósito: coordinación 3D
    │   ├── revisión P12
    │   └── revisión P13 vigente
    │       ├── C-101 → sólido SP3D COL-87
    │       ├── B-101 → sólido SP3D BM-22
    │       └── BR-01 → sólido SP3D RAIL-08
    │
    ├── Modelo físico Tekla FAB
    │   ├── propósito: detalle/fabricación
    │   └── revisión T08 vigente
    │       ├── C-101 → assembly TK-301
    │       ├── B-101 → assembly TK-412
    │       └── BR-01 → assembly TK-880
    │
    ├── Modelo analítico STAAD ESTÁTICO
    │   ├── propósito: cálculo estático global
    │   └── revisión S06 vigente
    │       ├── C-101 → barra M-120
    │       ├── B-101 → barras M-210 y M-211
    │       └── BR-01 → sin objeto directo; efecto mediante carga
    │
    └── Modelo analítico STAAD DINÁMICO
        ├── propósito: cálculo dinámico
        └── revisión D03 vigente
            ├── C-101 → barras DM-20 y DM-21
            ├── B-101 → barra DM-30
            └── BR-01 → no incluida; no aplicable según política
```

El árbol sirve para navegar, pero no afirma que los modelos sean partes
físicas de `ST-01`. Están asociados al conjunto porque lo representan o
analizan para un propósito. Tampoco los objetos de STAAD o Tekla son hijos de
la ocurrencia física: se relacionan mediante representaciones,
correspondencias y referencias contextualizadas.

### Dos niveles de consulta complementarios

Desde la estructura o cimentación se necesita poder consultar:

1. **Por modelo:** qué modelos existen, cuál es su propósito, cuáles son sus
   revisiones y qué ocurrencias cubre cada uno.
2. **Por ocurrencia:** en qué modelos aparece una ocurrencia y cómo la trata
   cada uno —objeto físico, una o varias barras, zona equivalente, efecto
   indirecto mediante carga o ausencia declarada—.

Una matriz de navegación podría mostrar:

| Ocurrencia | SP3D coordinación | Tekla fabricación | STAAD estático | STAAD dinámico |
|---|---|---|---|---|
| `C-101` | Sólido `COL-87` | Assembly `TK-301` | Una barra `M-120` | Dos barras `DM-20/21` |
| `B-101` | Sólido `BM-22` | Assembly `TK-412` | Dos barras `M-210/211` | Una barra `DM-30` |
| `BR-01` | Sólido `RAIL-08` | Assembly `TK-880` | Efecto mediante carga | No aplicable |

La matriz no exige que todos los modelos contengan las mismas ocurrencias ni
que las representen con la misma topología.

### Qué debe conciliarse

Un `CasoDeConciliación` no debe comparar indiscriminadamente todos los campos
de todos los modelos. Necesita una política o contrato que declare qué
aspectos son comparables entre determinados roles y propósitos de modelo.

Como vocabulario provisional, una `PolíticaDeConciliación` debería indicar:

- modelos o roles participantes;
- propósito y fase;
- alcance —conjunto, familia de ocurrencias u ocurrencia concreta—;
- aspectos que deben compararse;
- relación esperada —igualdad, equivalencia, tolerancia, derivación,
  cobertura o ausencia permitida—;
- autoridad por aspecto;
- gravedad y efecto de un incumplimiento;
- y responsable de resolver las excepciones.

Ejemplos iniciales, todavía pendientes de contraste:

| Aspecto | Tratamiento candidato |
|---|---|
| Identidad y cobertura de ocurrencias | Comprobar solo donde la política exija presencia |
| Sección o material físico | Comparar significado normalizado con modelos que dependan de ellos |
| Placement físico | Comparar con tolerancias y transformaciones identificadas |
| Correspondencia físico–analítica | Evaluar cardinalidad, cobertura y vigencia; no exigir igualdad geométrica |
| Topología, mallado e IDs de nodos/barras | Propios de cada modelo; no exigir igualdad |
| Offsets, releases y rigideces | Comparar intención o compatibilidad solo si el propósito lo requiere |
| Masa y densidad | Conciliar cuando sean entradas compartidas del análisis correspondiente |
| Cargas | Conciliar procedencia, cobertura, escenario y aplicación; no asumir igualdad de números fuera del mismo contexto |
| Resultados estáticos frente a dinámicos | No comparar por defecto; requieren una comprobación definida expresamente |

Que el modelo estático represente `C-101` con una barra y el dinámico con dos
no es una discrepancia por sí sola. Puede ser una diferencia válida de
idealización. Sí podría ser discrepancia que ambos declaren basarse en el
mismo estado físico y uno conserve una sección obsoleta cuando la política
exige que esa entrada sea común.

### Caso de conciliación con alcance de conjunto

El `CasoDeConciliación` puede abrirse sobre `ST-01`, no únicamente sobre una
ocurrencia:

```text
CasoDeConciliación CC-ST01-07
├── alcance: estructura ST-01
├── estado/versión base: ST-01 v05
├── modelos y revisiones comparados
│   ├── SP3D COORD P13
│   ├── Tekla FAB T08
│   ├── STAAD ESTÁTICO S06
│   └── STAAD DINÁMICO D03
├── políticas aplicadas
│   ├── cobertura física para fabricación
│   ├── correspondencia físico–analítica estática
│   ├── correspondencia físico–analítica dinámica
│   └── entradas compartidas de masa y material
├── evaluaciones por ocurrencia
│   ├── C-101 → compatible en los cuatro modelos
│   ├── B-101 → diferencia topológica permitida
│   └── BR-01 → cobertura indirecta/ausencia permitida
├── discrepancias de conjunto
│   └── masa total dinámica fuera de tolerancia
├── discrepancias por ocurrencia
│   └── C-102 conserva HEB 300 en STAAD estático frente a HEB 320 aceptado
└── decisiones y resultado
```

Esto permite que una discrepancia pertenezca al conjunto cuando no puede
atribuirse a una única ocurrencia —por ejemplo, masa total, hipótesis global o
cobertura del modelo— y que otras se localicen en ocurrencias concretas.

### Flujo ampliado

```text
Estructura/cimentación
→ identifica modelos asociados por propósito
→ selecciona revisiones concretas de cada modelo
→ selecciona políticas de conciliación aplicables
→ compara primero alcance y cobertura del conjunto
→ navega, cuando proceda, a las ocurrencias y sus representaciones
→ clasifica diferencias esperadas, toleradas o no comparables
→ abre discrepancias solo para incumplimientos reales o dudas no resueltas
→ conserva decisiones por aspecto y autoridad
→ acepta un nuevo estado/versión, acepta sin cambios o mantiene pendientes
```

No se pretende construir un modelo analítico maestro ni fusionar las
topologías del modelo estático y el dinámico. El CDM conserva cada modelo con
su identidad y propósito, y normaliza únicamente los aspectos necesarios para
las consultas y conciliaciones definidas.

### Decisiones adicionales abiertas

1. Criterio definitivo para distinguir otro modelo de una nueva revisión del
   mismo modelo.
2. Vocabulario común para modelos físicos, analíticos y documentales sin
   ocultar sus diferencias.
3. Cómo se declara formalmente que un modelo está asociado a una estructura,
   cimentación o conjunto.
4. Cómo se expresa la cobertura de una ocurrencia en un modelo: directa,
   agregada, parcial, indirecta o no aplicable.
5. Catálogo inicial de aspectos conciliables por parejas de propósitos de
   modelo.
6. Qué discrepancias pertenecen al conjunto y cuáles a una ocurrencia.
7. Si un único `CasoDeConciliación` puede abarcar varios modelos y cientos de
   ocurrencias o necesita dividirse en casos relacionados.
