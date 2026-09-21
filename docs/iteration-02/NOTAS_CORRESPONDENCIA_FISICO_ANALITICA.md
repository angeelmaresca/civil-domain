# Correspondencia físico–analítica — notas de preparación (Miguel)

> Notas personales de preparación para la sesión de `iteration-02`. Hipótesis
> `DRAFT`, no son contenido aprobado. Todavía en borrador, sin subir al
> historial de `develop`. Basadas en
> [`RELATIONSHIPS.md`](../RELATIONSHIPS.md),
> [`domain-objects/DESIGN_OCCURRENCE.md`](../domain-objects/DESIGN_OCCURRENCE.md)
> (sección 3.7) y la [ficha de acciones y cargas](../iteration-01/FICHA_MIGUEL_ACCIONES_CARGAS.md)
> de la primera iteración. [`ENUNCIADO.md`](ENUNCIADO.md) no exige ficha; este
> documento es solo apoyo personal para la discusión conjunta. Complementa
> [`NOTAS_TIPO_ESTADO_DISENO.md`](NOTAS_TIPO_ESTADO_DISENO.md).

## 1. El problema en una frase

Cuando un objeto físico (una columna, una zapata) se "traduce" a un modelo de
cálculo, ¿siempre es una traducción de "una pieza física = un objeto de
cálculo", o puede ser más complicado?

## 2. Los conceptos, tal como los define el repo

- `ModeloAnalitico` / `ObjetoAnalitico`: la idealización usada para calcular
  (barras, placas, nodos...). **Nunca** es lo mismo que la ocurrencia física,
  ni siquiera cuando parecen "la misma cosa" a simple vista.
- `se corresponde con objeto analítico`: la relación que conecta un estado
  físico —o un snapshot físico todavía no aceptado— con uno o varios objetos
  o zonas de un modelo analítico. Puede ser **1:1, 1:N, N:1 o N:M** — las
  cuatro son casos normales, no excepciones.

**Analogía sencilla:** piensa en dibujar un retrato de una persona. Puedes
hacerlo con un solo trazo simple (un muñeco de palitos) o con un dibujo
anatómico detallado dividido en partes: brazo, torso, pierna... La persona
real sigue siendo una sola — lo que cambia es cuántos "trozos de dibujo"
decides usar para representarla, y eso depende de para qué necesitas el
dibujo (identificarla rápido, o hacerle un traje a medida).

## 3. Los cuatro casos, con ejemplos del caso común

| Cardinalidad | Ejemplo | Cuándo pasa |
|---|---|---|
| **1:1** | `C-101` se idealiza como **una** barra en el modelo global `AM-01`. | Caso simple, el más habitual en un modelo preliminar. |
| **1:N** | `C-101` se idealiza como **dos** barras dentro del **mismo** `AM-01`, porque el mallado la corta donde se conecta un arriostramiento intermedio. | Una sola pieza física, partida en varios trozos analíticos por necesidad del cálculo. |
| **N:1** | Varias placas de anclaje y pernos físicos (varios objetos reales) se representan como **un único** resorte o conexión equivalente. | Simplificación: muchas piezas reales, un solo objeto de cálculo. |
| **N:M** | La zapata `F-101` se idealiza con varias placas (shells), que a su vez corresponden a varias zonas distintas del terreno modelado. | El caso más complejo: varios objetos físicos y varios objetos analíticos, sin relación uno a uno en ningún sentido. |

## 4. Un matiz importante — esto no es lo mismo que vimos en la ficha de acciones

En la ficha de acciones y cargas (bloque F, pregunta F.26) se llegó a esta
conclusión, que sigue siendo válida pero sobre **otra pregunta distinta**:

> *"Dentro de un mismo modelo analítico: uno a uno. Una carga puntual... se
> aplica a un único elemento... nunca se reparte simultáneamente entre varios
> elementos dentro del mismo modelo."*

Eso era sobre **dónde se aplica una Acción** (un dato de carga). Lo que
pregunta la correspondencia físico–analítica es distinto: **cuántos objetos
analíticos idealizan a un mismo elemento físico** — y ahí sí puede haber 1:N
*dentro de un mismo modelo* (como `C-101` partido en dos barras). No es una
contradicción, es una pregunta vecina que conviene no confundir en la sesión.

## 5. La regla de oro que hay que defender

La correspondencia nunca debe "fingir" que el objeto físico y el analítico
son el mismo objeto. Según `RELATIONSHIPS.md`, la relación debe poder
conservar:

- propósito y modelo/revisión de análisis;
- cardinalidad (`1:1`, `1:N`, `N:1`, `N:M`);
- evidencia y autor de la correspondencia;
- sistemas de referencia y transformaciones relevantes;
- vigencia o evaluación de alineación con el estado físico;
- rol de cada participante, sin declarar que ambos son el mismo objeto.

Es la misma lección que ya se tenía sobre el convenio de signos en la ficha
de acciones: la trazabilidad del "cómo y por qué se hizo esta traducción" es
tan importante como el número o la geometría resultante.

## 6. Pregunta abierta para plantear en la sesión — con ejemplo para debatir

`RELATIONSHIPS.md` exige que la correspondencia guarde "vigencia o evaluación
de alineación con el estado físico" — pero no dice qué pasa exactamente
cuando el estado físico cambia.

### Ejemplo para debatir: `C-101` cambia de perfil entre revisiones

`C-101@R03` (perfil `HEB 300`) se corresponde 1:1 con la barra `B-1` del
modelo `AM-01`. En la revisión siguiente, `C-101@R04` cambia de perfil a
`HEB 340` — mismo eje, misma posición, pero distinta sección.

**Pregunta para el equipo:** ¿la correspondencia `C-101 → B-1` sigue vigente
automáticamente para `R04` (asumiendo que solo cambian las propiedades de la
barra, no su geometría de eje), o hay que **re-evaluarla explícitamente** —
por ejemplo, marcándola como "pendiente de revisión" hasta que alguien
confirme que sigue alineada?

**Consecuencia de cada opción:**

- **Herencia automática:** más simple, pero silenciosa — nadie decide
  explícitamente que `B-1` sigue siendo válida para el nuevo perfil; es el
  mismo riesgo de "herencia silenciosa" que ya se señaló para el tipo en
  `NOTAS_TIPO_ESTADO_DISENO.md` (punto 8).
- **Re-evaluación explícita:** más trazable — cada cambio de estado físico
  obliga a confirmar (o corregir) sus correspondencias analíticas — pero
  añade trabajo en cada revisión, incluso cuando el cambio es trivial para
  el modelo de cálculo.
- **Posible camino intermedio:** distinguir cambios que sí afectan al modelo
  analítico (geometría de eje, posición) de los que no lo afectan
  necesariamente (propiedades de sección, material) y solo forzar
  re-evaluación en el primer caso.

## 7. Resumen para llevar a la sesión

1. La correspondencia físico–analítica admite 1:1, 1:N, N:1 y N:M — todas
   son normales, ninguna es una excepción del esquema.
2. Esto es distinto de "dónde se aplica una carga dentro de un modelo"
   (ficha de acciones, F.26) — son preguntas vecinas, no la misma pregunta.
3. La relación nunca debe igualar objeto físico y analítico; debe conservar
   propósito, revisión, autor, sistemas de referencia y vigencia.
4. Pregunta para debatir: cuando el estado físico cambia, ¿la correspondencia
   hereda vigencia automáticamente o exige re-evaluación explícita?
