# Cuándo cambia un Estado de Diseño: revisión vs. recálculo

> **Status:** DRAFT
> **Editable:** sí; nota personal de preparación de Miguel
> **Document owner:** Miguel
> **Canonical for:** —
> **Sources:** [`RULES.md`](../RULES.md), [`domain-objects/DESIGN_OCCURRENCE.md`](../domain-objects/DESIGN_OCCURRENCE.md),
> [`RELATIONSHIPS.md`](../RELATIONSHIPS.md), [`VOCABULARY.md`](../VOCABULARY.md) y
> conversación de trabajo sobre casos reales de coordinación STAAD/SAP2000 ↔ maqueta 3D.
> **Supersedes:** —
> **Last reviewed:** 2026-09-22

## Nota de alcance y de apertura de carpeta

Esta es la primera nota de `iteration-03/`. Se abre esta carpeta antes de que
`iteration-02` haya tenido su sesión de contraste porque el tema —cuándo un
`EstadoDeDiseño` cambia realmente— surgió como un caso concreto de duda
operativa (coordinación STAAD/SAP2000 ↔ maqueta 3D) que Miguel quiso separar
de las notas de `iteration-02` para no mezclar dos bloques de investigación
distintos. `iteration-02` sigue abierta y activa; esta carpeta no la
sustituye ni la cierra.

## 1. El problema en una frase

¿Cuándo una edición de la maqueta 3D o del modelo analítico (STAAD, SAP2000)
constituye una revisión nueva del `EstadoDeDiseño` de una ocurrencia, y
cuándo es solo una edición sin esa consecuencia?

## 2. Casos concretos que disparan la duda

- Un ingeniero entrega el modelo analítico de STAAD a un diseñador para que
  lo incorpore en la maqueta 3D (revisión `R0`). Al día siguiente, el
  diseñador añade elementos auxiliares y misceláneos (barandillas,
  escaleras...): está editando la maqueta, pero no parece que esté
  cambiando la revisión real de la estructura.
- El departamento de piping envía nuevas bandejas para los pipe racks. Se
  decide que no deben recalcularse en STAAD, pero sí incorporarse en la
  maqueta 3D para tenerlas presentes. La revisión estructural debería seguir
  siendo la misma, pero la propia edición del modelo 3D puede confundirse
  con una revisión nueva.
- Los diseñadores suben o bajan arriostramientos por necesidades de ruteo.
  Aquí sí cambia un dato propio del arriostramiento (su posición), a
  diferencia de los dos casos anteriores.

## 3. La raíz de la confusión: dos preguntas distintas

Se suele asumir que "si edito, es porque afecta al cálculo, luego es nueva
revisión". Pero son dos preguntas distintas:

- **¿Ha cambiado el estado de diseño?**
- **¿Este cambio exige recalcular?**

`RULES.md` ya separa estas dos ideas, aunque nadie lo había aplicado todavía
a este caso:

> **Regla 5:** *"Un estado aceptado registra decisión, responsable, fecha,
> contexto y evidencia; no equivale al snapshot más reciente."*

Cada vez que alguien toca STAAD o la maqueta 3D se genera un **snapshot**
— evidencia de "qué hizo tal herramienta en tal momento" — no
automáticamente un **estado de diseño**. Que un snapshot se convierta en
`EstadoDeDiseño` formal depende de una decisión explícita de aceptación
(`DecisionDeAceptacion`, entidad vecina ya nombrada en
`DESIGN_OCCURRENCE.md`), tomada por quien tiene autoridad — normalmente el
ingeniero de cálculo, no quien edita la maqueta.

**Analogía sencilla:** piensa en un documento colaborativo compartido, donde
cualquiera puede escribir libremente. Eso es la maqueta 3D — cambia todo el
rato, cualquiera edita. Pero "publicar una nueva edición oficial" del
documento es un acto aparte, que solo hace el editor cuando decide que la
versión actual merece convertirse en la referencia — no cada vez que alguien
teclea una letra.

## 4. El criterio práctico para decidir "¿es una nueva revisión de ESTA ocurrencia?"

Antes de preguntar si algo "afecta al cálculo", conviene preguntar algo más
objetivo:

> ¿El cambio toca datos que pertenecen a la ocurrencia concreta que nos
> preocupa (su geometría estructural, material, placement/posición o una
> relación de apoyo/conexión vigente), o toca otra cosa (otra ocurrencia
> distinta, una relación nueva, o solo una representación de coordinación)?

## 5. Los tres casos, aplicando el criterio

### 5.1 Elementos auxiliares/miscelánea añadidos a la maqueta

El diseñador no toca ningún dato de la columna o viga estructural (su
geometría, material o placement no cambian). Añade **otras ocurrencias
distintas** (barandillas, escaleras, elementos varios) al mismo archivo 3D
compartido.

> **Regla 6:** *"Una representación física no es la ocurrencia que
> representa."*

Que el archivo 3D cambie no significa que la ocurrencia estructural cambie.
**No es nueva revisión** de la columna ni de la viga. Es, como mucho, la
aparición de nuevas ocurrencias — que quizá ni necesiten identidad propia,
según la prueba de individualidad/continuidad/razón de negocio de
`DESIGN_OCCURRENCE.md`.

### 5.2 Bandejas de tuberías añadidas al pipe rack, sin recalcular

Aquí pasan dos cosas a la vez, y hay que separarlas:

1. La bandeja es una **ocurrencia nueva** (o quizá ni eso, si no necesita
   identidad propia).
2. Se crea una **relación nueva** (`da apoyo a` o `se conecta con`) entre la
   bandeja y la viga del pipe rack.

Ninguna de las dos cosas es, por sí misma, una propiedad de la viga.

> **Regla 13:** *"Las relaciones que pueden cambiar deben identificar su
> contexto o vigencia."*

La relación nueva lleva su propia fecha/vigencia, sin obligar a la viga a
generar un nuevo estado. Que el departamento de piping diga "no hay que
recalcular" es, en la práctica, una decisión de aceptación implícita —
*"esta carga ya estaba contemplada en el margen de diseño original"* —, y
esa justificación debería quedar escrita como evidencia de la relación, no
perderse.

### 5.3 Arriostramientos que suben o bajan de posición

Este caso sí toca un dato propio de la ocurrencia: su placement. Aquí no
conviene forzar la conclusión de "no es nueva revisión" solo para evitar
papeleo. La salida está en el punto 6.

## 6. Separar "nuevo estado" (barato) de "requiere recálculo" (caro)

Mover el arriostramiento sí puede registrarse como un nuevo `EstadoDeDiseño`
de esa barra concreta — es simplemente verdad: su posición cambió. Pero eso
no obliga a recalcular nada. El ingeniero de cálculo puede aceptar ese
estado marcando explícitamente *"dentro de tolerancia, no requiere nueva
pasada de STAAD"*, con su propia evidencia y responsable (regla 5 otra vez).

Lo que no puede pasar es que el estado "no cuente" solo porque no se
recalculó — eso es justo lo que la regla 5 prohíbe en cualquier dirección:
ni el último snapshot es automáticamente el estado aceptado, ni un estado
real deja de serlo porque no fue recalculado.

> **Regla 15:** *"La validación técnica se refiere a estados, entradas,
> análisis y evidencias identificados; no es una propiedad eterna de la
> ocurrencia."*

Es decir: "validado" o "requiere recálculo" son etiquetas de un estado
concreto, no un interruptor único que se aplica a toda la ocurrencia para
siempre.

## 7. Resumen — 3 propuestas para el equipo

1. **Ninguna herramienta genera revisiones por sí sola.** STAAD, SAP2000 y
   la maqueta 3D producen *snapshots*; una revisión (`EstadoDeDiseño`) solo
   existe cuando alguien con autoridad la acepta explícitamente, con
   responsable y evidencia.
2. **Antes de preguntar "¿afecta al cálculo?", preguntar "¿de quién es este
   dato?".** Si el cambio no toca la geometría/material/placement/relaciones
   vigentes de la ocurrencia en cuestión —porque es otra ocurrencia, una
   relación nueva, o solo la representación de coordinación—, no es una
   revisión suya.
3. **Separar "nuevo estado" de "requiere recálculo".** Son dos decisiones
   distintas, con responsables potencialmente distintos: el diseñador puede
   generar estados; solo el ingeniero de cálculo decide si uno de ellos
   exige recalcular.

## 8. Pregunta abierta para plantear en la sesión — con ejemplo para debatir

Queda sin resolver **quién tiene autoridad** para aceptar un estado como
"no requiere recálculo" sin pasar por el ingeniero de cálculo en cada caso
individual.

### Ejemplo para debatir: bandejas de piping dentro de un margen ya previsto

Supongamos que el proyecto definió desde el inicio un margen de carga futura
en los pipe racks (una práctica habitual: sobredimensionar a propósito para
absorber bandejas que se añadirán más adelante). El departamento de piping
añade una bandeja nueva dentro de ese margen.

**Pregunta para el equipo:**

- ¿Puede el propio departamento de piping aceptar el nuevo estado de la
  relación bandeja-viga como "dentro de margen, no requiere recálculo", o
  esa aceptación debe pasar siempre por el ingeniero de cálculo, aunque sea
  un trámite rápido?
- Si se delega esa autoridad, ¿qué evidencia mínima debe registrarse para
  que, más adelante, alguien pueda auditar por qué no se recalculó (p. ej.
  referencia al cálculo original que ya contemplaba ese margen)?
- ¿Qué pasa si dos bandejas sucesivas, cada una "dentro de margen" por
  separado, agotan juntas un margen que nadie sumó explícitamente? ¿Quién
  es responsable de vigilar el acumulado, si la aceptación se delegó caso a
  caso?

No hace falta resolverlo en esta nota — es la pregunta que puede evitar que
la solución de "recálculo vs. no recálculo" se convierta en una vía rápida
para acumular deuda técnica sin que nadie se dé cuenta.
