# Tipo vs. Estado de diseño — notas de preparación (Miguel)

> Notas personales de preparación para la sesión de `iteration-02`. Hipótesis
> `DRAFT`, no son contenido aprobado. Todavía en borrador, sin subir al
> historial de `develop`. Basadas en
> [`domain-objects/DESIGN_OCCURRENCE.md`](../domain-objects/DESIGN_OCCURRENCE.md),
> [`RELATIONSHIPS.md`](../RELATIONSHIPS.md),
> [`VOCABULARY.md`](../VOCABULARY.md) y la síntesis de la primera iteración.
> [`ENUNCIADO.md`](ENUNCIADO.md) no exige ficha; este documento es solo apoyo
> personal para la discusión conjunta. Complementa
> [`NOTAS_CORRESPONDENCIA_FISICO_ANALITICA.md`](NOTAS_CORRESPONDENCIA_FISICO_ANALITICA.md).

## 1. El problema en una frase

¿Cuándo decimos que un depósito o una columna es "de tipo X", esa etiqueta se
pega para siempre al objeto, o puede cambiar cada vez que se revisa el diseño?

## 2. Los tres conceptos que hay que separar

```text
OcurrenciaDeDiseño O-017          ← la identidad, para siempre
├── EstadoDeDiseño R03            ← una "foto" aceptada, en un momento dado
│   ├── clase funcional: columna
│   ├── geometría, materiales, placement
│   └── (aquí vive el tipo declarado en esa revisión)
└── EstadoDeDiseño R04
    ├── clase funcional: columna
    └── geometría, materiales, placement modificados
```

**Analogía sencilla:** piensa en el carnet de identidad de una persona. El
número de DNI nunca cambia — eso es la `OcurrenciaDeDiseño`. Pero si preguntas
"¿qué trabajo tiene esta persona *ahora*?", la respuesta puede cambiar con los
años: becario en 2023, empleado fijo en 2024. Esa foto de "cómo es la persona
en este momento" es el `EstadoDeDiseño`. Y la etiqueta de categoría laboral
(becario / fijo / autónomo) es el **tipo** — y vive pegada a la foto de un
momento concreto, no al DNI. La persona no deja de ser la misma persona
(mismo DNI) cuando cambia de categoría laboral.

## 3. Dónde vive el tipo — no es un tercer nivel de la jerarquía

Si se dibuja el tipo como un hijo más de la ocurrencia, aparece un problema: el
mismo tipo normalmente lo comparten **otras** ocurrencias (`EQ-102`, `EQ-103`...).
Colgarlo de una única ocurrencia obligaría a duplicar su definición en cada una,
violando la regla ya escrita en `AGENTS.md`: *"cada concepto debe tener una
única fuente propietaria"*.

```text
DefinicionDeTipo TANQUE-VERTICAL-A        DefinicionDeTipo TANQUE-VERTICAL-B
        ▲                                          ▲
        │ está tipado por                          │ está tipado por
        │                                          │
OcurrenciaDeDiseño EQ-101
├── EstadoDeDiseño R03 ─────────────────────┘
└── EstadoDeDiseño R04 ──────────────────────────────────────────────┘
```

El tipo no cuelga hacia abajo del árbol: es un objeto que existe por su cuenta,
y cada `EstadoDeDiseño` apunta hacia él mediante la relación `está tipado por`
(ya nombrada en `RELATIONSHIPS.md`). Es la misma separación que hace IFC con
`IfcTypeObject` + `IfcRelDefinesByType`.

**Ejemplo:** `EQ-101` en `R03` es un depósito cilíndrico vertical, tipo
`TANQUE-VERTICAL-A`. Tras un rediseño, `R04` cambia a patas más cortas y otro
material, tipo `TANQUE-VERTICAL-B`. Sigue siendo el mismo `EQ-101` — mismo
proyecto, mismo TAG — pero su tipo cambió entre revisiones. Si el tipo
estuviera pegado a la ocurrencia completa, `R04` tendría que ser "otro
depósito", rompiendo la trazabilidad de revisiones.

## 4. Cómo se tipa una ocurrencia en la práctica — la mecánica

Separar "dónde vive el tipo" de "cómo se conecta" es importante. El proceso
tiene cuatro pasos:

**1. El tipo se declara primero, de forma independiente.**
Alguien crea `DefinicionDeTipo TANQUE-VERTICAL-A` con valores por defecto
(p. ej. altura 6m, diámetro 3m, material acero al carbono). Esto ocurre sin
referencia a `EQ-101` — el tipo existe en su propio catálogo, listo para que
cualquier ocurrencia lo use.

**2. Al aceptar un estado de diseño, se establece la relación `está tipado por`.**
Cuando se acepta `EQ-101 @ R03` como estado de diseño, alguien decide
explícitamente que ese estado usa `TANQUE-VERTICAL-A`:

```text
EstadoDeDiseño EQ-101@R03  --está tipado por-->  DefinicionDeTipo TANQUE-VERTICAL-A
```

**3. El estado hereda los valores por defecto del tipo, salvo que los sobrescriba.**
Mecánica tomada de IFC (`IfcTypeObject` + `IfcRelDefinesByType`): si
`EQ-101@R03` no declara una altura propia, hereda los 6m del tipo. Si este
proyecto necesita 6.2m, el estado declara su propio valor, que **prevalece**
sobre el del tipo — sin romper la relación de tipado. El tipo da valores por
defecto, no un contrato blindado.

**4. Retipar implica un nuevo estado, no editar el existente.**
`EstadoDeDiseño` es "una definición aceptada para una revisión"; no se muta
después de aceptado. Si en la revisión siguiente `EQ-101` pasa a usar
`TANQUE-VERTICAL-B`, no se cambia la relación de `R03` — se crea
`EstadoDeDiseño EQ-101@R04` con su propia relación hacia `TANQUE-VERTICAL-B`.
`R03` sigue apuntando para siempre a `TANQUE-VERTICAL-A`, intacto en la
historia.

**Matiz aparte — "clase funcional" no pasa por este mecanismo.** En el
diagrama del punto 2, `clase funcional: columna` vive *dentro* del estado
como un dato propio, no como relación de tipado hacia fuera. "Esto es una
columna" (categoría básica) y "esta columna usa el perfil `HEB 300`" (tipo
reutilizable concreto) son preguntas distintas: la primera es una propiedad
simple del estado; la segunda pasa por `está tipado por` hacia un objeto
compartido.

### Ejemplo completo con override

```text
DefinicionDeTipo TANQUE-VERTICAL-A          DefinicionDeTipo TANQUE-VERTICAL-B
  altura: 6m (default)                        altura: 5m (default)
  diámetro: 3m (default)                       diámetro: 3.2m (default)
        ▲                                            ▲
        │ está tipado por                            │ está tipado por
        │                                            │
EstadoDeDiseño EQ-101@R03                    EstadoDeDiseño EQ-101@R04
  altura: 6.2m  ← sobrescribe el default       (usa los defaults tal cual)
```

`R03` usó `TANQUE-VERTICAL-A` pero pisó la altura por defecto con un valor
propio (6.2m). `R04` cambió de tipo por completo y esta vez no sobrescribió
nada — usa los valores del tipo `B` tal cual.

## 5. Evidencia que ya tenemos de dos frentes distintos

- **Miguel, ficha de acciones y cargas (A.4):** *"dimensiones, material o tipo
  de soportes entre revisiones de diseño... pertenecen al tipo/especificación
  de cada revisión, no a la identidad de la ocurrencia."*
- **`DESIGN_OCCURRENCE.md`, pregunta 4:** *"¿El tipo se aplica a la
  continuidad completa o puede cambiar entre estados? La segunda opción
  parece necesaria para la zapata de Luis."*

Dos frentes independientes (acciones/cargas y zapata) apuntan a la misma
conclusión: **el tipo vive en el estado, no en la ocurrencia completa.**

**Matiz sin cerrar:** en `RELATIONSHIPS.md`, la relación `está tipado por` se
define con origen "estado **u** ocurrencia contextualizada" — el equipo no ha
cerrado formalmente esta pregunta, aunque la evidencia ya apunta en una
dirección.

## 6. Qué concepto debe recoger `DefinicionDeTipo`

Según la síntesis de la primera iteración: *"el tipo se declara para reutilizar
una intención dentro de un alcance conocido; la agrupación [derivada] se
obtiene comparando propiedades."*

Tres palabras hacen el trabajo: **declarado** (alguien decide explícitamente
que hay una intención compartida, no es casualidad), **intención** (una
decisión de ingeniería, no una observación), **alcance conocido** (no es
universal para siempre, vale dentro de un contexto).

### Debería recoger

1. La definición común reutilizable (parámetros por defecto: geometría, perfil,
   material típico) — una plantilla, no los valores reales de una ocurrencia.
2. El alcance de validez (este proyecto, un catálogo corporativo, una
   disciplina).
3. La posibilidad de que el estado la sobrescriba (una propiedad declarada en
   el estado puede prevalecer sobre la del tipo, como en IFC).

### No debería recoger

| Concepto vecino | Por qué no es lo mismo |
|---|---|
| Clasificación (`está clasificado como`) | Referencia a un vocabulario externo (bSDD, Uniclass, catálogo de fabricante); no declara una intención propia de reutilización. |
| Agrupación derivada | Se calcula comparando propiedades; puede coincidir por casualidad sin que nadie haya declarado un tipo compartido. |
| Estado de diseño | Contiene los valores reales de esta ocurrencia en esta revisión, use o no los valores por defecto del tipo. |
| Ocurrencia de diseño | Identidad de un individuo concreto; el tipo quiere ser compartido por varios individuos. |
| Objeto analítico | Cómo se idealiza para calcular; no tiene que ver con qué plantilla de diseño física se reutilizó. |

## 7. Pregunta abierta para plantear en la sesión — con ejemplo para debatir

En la propia tabla de `DESIGN_OCCURRENCE.md` aparece esta entrada, sin resolver:

> *"Perfil HEB 300 → No [es ocurrencia]. Es una definición reutilizable **o**
> clasificación, no el individuo `C-101`."*

El "o" delata que el equipo no ha decidido si un perfil normalizado es un
**tipo intencional** o una **clasificación externa**.

### Ejemplo para debatir: el perfil HEB 300 de Ángel

Ángel usa el perfil `HEB 300` en `C-101` y en `C-105`.

**Pregunta para el equipo:** ¿`HEB 300` es...

- **(a) `DefinicionDeTipo`** — una intención declarada por el equipo de
  reutilizar esa sección en varias columnas del proyecto, con datos por
  defecto (área, inercia, dimensiones) que cada columna hereda y puede
  sobrescribir puntualmente; o
- **(b) Clasificación** — una simple referencia al catálogo de la norma de
  perfiles (p. ej. EN 10025-2), sin intención propia de reutilización del
  proyecto: cada columna declara sus propios datos geométricos, que
  *coinciden* con ese catálogo por elegir el mismo perfil comercial.

**Consecuencia de cada opción, para que se debata en la sesión:**

- Si es (a): corregir un dato del `HEB 300` en un solo sitio actualiza (o
  propone actualizar) todas las columnas tipadas por él — pero exige decidir
  si el propio tipo necesita su propia revisión cuando cambie (ver punto 8).
- Si es (b): no hay un lugar central que reutilizar; cada columna es
  independiente y solo "se parece" a otras por casualidad de catálogo — más
  simple, pero se pierde la ventaja de corrección centralizada.
- **Posible tercer camino, para plantear también:** que no sean excluyentes —
  `HEB 300` podría ser una `DefinicionDeTipo` propia del proyecto que, a su
  vez, esté `clasificada como` una referencia al catálogo externo de la
  norma. Tipo y clasificación no compiten por el mismo rol si se mantienen
  como conceptos separados y compatibles.

## 8. Segunda pregunta abierta, más de fondo

Si `TANQUE-VERTICAL-A` cambia su propia definición con el tiempo (p. ej., se
corrige una errata en su altura por defecto), ¿todas las ocurrencias tipadas
por él heredan silenciosamente el cambio, o el tipo también necesita su propia
revisión — el mismo problema que ya se resolvió para la ocurrencia con
`EstadoDeDiseño`, ahora aplicado al tipo?

No hace falta resolverlo en esta sesión, pero merece quedar anotado: la
herencia silenciosa podría alterar retroactivamente diseños ya aceptados sin
que nadie lo decidiera explícitamente.

## 9. Resumen para llevar a la sesión

1. El tipo vive en el estado (`EstadoDeDiseño`), no en la ocurrencia completa
   — con evidencia cruzada de dos frentes distintos (Miguel y Luis).
2. El tipo no es un hijo de la ocurrencia: es un objeto compartido, conectado
   por la relación `está tipado por`.
3. El tipado ocurre al aceptar un estado (no antes, no después): el tipo se
   declara aparte, el estado se enlaza a él, y puede sobrescribir sus
   valores por defecto sin romper la relación.
4. Pregunta para debatir: ¿`HEB 300` es tipo intencional, clasificación, o
   ambos a la vez con roles separados?
5. Pregunta para anotar sin cerrar: ¿el propio tipo necesita revisión cuando
   cambia su definición compartida?
