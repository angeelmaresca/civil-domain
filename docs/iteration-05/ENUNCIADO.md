# Quinta iteración — frontera de los sistemas de ingeniería

> **Status:** DRAFT
> **Editable:** sí; memoria de conclusiones aportadas y guía de la siguiente iteración
> **Document owner:** equipo de dominio civil
> **Canonical for:** —; conserva la hipótesis y el plan de contraste, no decisiones aprobadas
> **Sources:** informe «Evolución del modelo: desde Design Occurrence hacia Engineering System» aportado por Miguel el 2026-10-01; documentos enlazados en el análisis
> **Supersedes:** —
> **Last reviewed:** 2026-10-01

## 1. Punto de partida

La cuarta iteración separó ocurrencia, representación, snapshot, modelo y caso de
conciliación. También mostró que pueden coexistir varios modelos con propósito y
ciclos de revisión independientes y que una conciliación puede abarcar un conjunto,
no solo una ocurrencia.

El informe de consolidación aporta la siguiente hipótesis: falta un contexto de
negocio superior a la ocurrencia para declarar qué modelos y ocurrencias forman un
universo coherente de ingeniería. Propone llamarlo `Engineering System` o
`SistemaDeIngeniería`.

## 2. Conclusiones que se conservan

El informe refuerza, sin elevarlas a `CANONICAL`, estas convergencias `DRAFT`:

- `OcurrenciaDeDiseño` mantiene identidad y trazabilidad de un individuo físico;
- sección, material, geometría, armadura o ubicación pueden cambiar y no definen por
  sí solas esa identidad;
- la ocurrencia no debe duplicar valores técnicos mantenidos por estados, modelos o
  fuentes;
- los modelos tienen identidad, propósito, revisiones y lifecycle propios;
- una representación enlaza la ocurrencia con lo que un modelo afirma sobre ella;
- la conciliación es una capacidad de negocio contextualizada por propósito,
  alcance, modelos, revisiones y políticas.

Sigue abierto cómo nace una ocurrencia, quién decide continuidad, cuándo se fusionan
o separan identidades y cómo se conserva la historia de conciliación.

## 3. Hipótesis nueva

```text
Proyecto
└── SistemaDeIngeniería (candidato)
    ├── ocurrencias contextualizadas
    ├── modelos asociados
    └── casos y políticas de conciliación aplicables

Representación
├── representa una ocurrencia
└── aparece en un modelo/revisión
```

La fuente propietaria `DRAFT` de este candidato es
[`ENGINEERING_SYSTEM.md`](../domain-objects/ENGINEERING_SYSTEM.md). La ocurrencia no
se convierte en contenedor de modelos: aparece en ellos mediante representaciones.

## 4. Matices necesarios antes de aceptar la propuesta

### 4.1 Contexto no equivale todavía a propiedad exclusiva

El informe usa «contiene» y «pertenece». La iteración probará primero relaciones de
asociación contextual. Un modelo global puede cubrir varios sistemas; una ocurrencia
puede participar en varios; una cimentación puede ser compartida. Una jerarquía
rígida falsearía esos casos o forzaría duplicados.

### 4.2 Los ejemplos no forman aún un catálogo

`Pipe rack`, `foundation system`, `building`, `equipment foundation` y `pipe support
system` mezclan posiblemente conjunto físico, sistema funcional, contexto espacial,
tipo y sistema de ingeniería. La etiqueta de negocio no decide la categoría. Cada
instancia debe superar pruebas de identidad, frontera y utilidad.

### 4.3 «Agregado raíz» queda aplazado

Un agregado raíz delimita consistencia y transacciones en un diseño de software. El
repositorio sigue en conceptualización de dominio y ha pospuesto tablas, clases y
API. Esta iteración puede descubrir una frontera de negocio sin afirmar todavía una
frontera técnica de agregado.

### 4.4 Propiedad canónica no significa copia maestra

El informe propone resolver propiedades desde fuentes de verdad. Se conserva como
hipótesis una `VistaResueltaDePropiedades`: para un aspecto, propósito y momento
concretos selecciona o deriva un valor desde afirmaciones con procedencia y autoridad.
No se crea una segunda bolsa mutable en la ocurrencia ni se asume una autoridad
universal por aplicación.

## 5. Pregunta de la iteración

> ¿`SistemaDeIngeniería` tiene identidad, frontera y responsabilidades propias que
> no cubren ya el conjunto físico, el sistema funcional o el contexto espacial, y
> sirve como ámbito habitual —no necesariamente exclusivo— de modelos y conciliación?

## 6. Trabajo propuesto

### 6.1 Traducción a preguntas normales

No se pide al equipo que maneje de entrada el vocabulario conceptual. Para estudiar
un caso basta responder estas preguntas:

| Término de trabajo | Pregunta sencilla |
|---|---|
| Propósito | ¿Para qué reconocemos este conjunto como una unidad en el proyecto? |
| Continuidad | ¿Qué puede cambiar y aun así seguiríamos llamándolo el mismo sistema? |
| Frontera | ¿Qué consideramos dentro y qué dejamos fuera? ¿Qué queda compartido? |
| Ocurrencias | ¿Qué elementos físicos necesitamos seguir individualmente dentro de este caso? |
| Modelos | ¿Qué modelos o archivos usamos para diseñarlo, coordinarlo o calcularlo? |
| Revisiones | ¿Qué entrega concreta de cada modelo estamos mirando? No basta decir «la última». |
| Responsables | ¿Quién mantiene cada modelo y quién puede aceptar una diferencia? Se buscan roles, no nombres de personas. |
| Decisiones del conjunto | ¿Qué preguntas solo pueden responderse mirando el conjunto y no una columna o zapata aislada? |

### 6.2 Ejemplo rellenado — pipe rack `PR-05`

El ejemplo siguiente es ilustrativo. Sirve para mostrar el nivel de respuesta
esperado; no declara que sus límites o responsables estén aprobados.

| Pregunta | Respuesta de ejemplo |
|---|---|
| ¿Para qué lo tratamos como una unidad? | Para soportar y coordinar líneas y bandejas a lo largo de un recorrido, diseñando conjuntamente estructura, acciones e interfaces. |
| ¿Qué puede cambiar sin dejar de ser `PR-05`? | Secciones, número de vanos, arriostramientos, división en módulos o revisiones de sus modelos. Habría que decidir si dividirlo en dos racks operativamente independientes conserva una identidad o crea dos. |
| ¿Qué está dentro? | Como hipótesis: módulos estructurales, columnas, vigas y arriostramientos. Está abierto si incluye las cimentaciones. |
| ¿Qué está fuera o solo relacionado? | Las tuberías y bandejas soportadas pueden usar el rack sin ser partes físicas del rack. El terreno y el área espacial tampoco se incluyen automáticamente. |
| ¿Qué elementos seguimos individualmente? | Por ejemplo `ST-01`, `C-101`, `B-101`, `BR-01` y, si se acuerda, `F-101`. No hace falta enumerar cada detalle menor. |
| ¿Qué modelos usamos? | Por ejemplo, coordinación física en SP3D, cálculo global en STAAD, detalle/fabricación en Tekla y un modelo de cimentaciones. |
| ¿Qué revisiones concretas comparamos? | Ejemplo: SP3D `P13`, STAAD estático `S06`, Tekla `T08` y cimentaciones `F04`. Estos códigos solo ilustran que deben identificarse entregas concretas. |
| ¿Quién responde de qué? | Coordinación civil/estructural mantiene el límite del caso; cada autor mantiene su modelo; la autoridad técnica correspondiente acepta diferencias de estructura, cargas o cimentación. Los roles exactos siguen abiertos. |
| ¿Qué se decide para todo `PR-05`? | Si las cimentaciones forman parte del sistema, si una nueva modularización conserva identidad, qué revisiones son compatibles y si una discrepancia global bloquea la entrega. |

Este ejemplo ayuda a detectar la diferencia entre niveles:

```text
PR-05                         candidato a SistemaDeIngeniería
├── ST-01                     posible conjunto físico
│   ├── C-101                 OcurrenciaDeDiseño
│   └── B-101                 OcurrenciaDeDiseño
├── modelo SP3D P13           modelo/revisión asociados
├── modelo STAAD S06          modelo/revisión asociados
└── ¿F-101 está dentro?       pregunta de frontera, no hecho resuelto
```

### 6.3 Lista inicial que debemos construir

La primera parte del trabajo consiste precisamente en sacar la lista de lo que el
equipo considera sistemas de ingeniería. No se busca todavía una taxonomía completa.
Se buscan **instancias reales con nombre**, como `PR-05`, no solo clases como
«pipe rack».

Esta es una semilla para corregir, ampliar o descartar:

| Candidato inicial | Por qué podría ser sistema de ingeniería | Duda principal |
|---|---|---|
| Pipe rack `PR-05` | Tiene significado de negocio y puede reunir varios modelos y muchas ocurrencias. | Si incluye módulos, estructura y cimentaciones bajo la misma frontera. |
| Pipe bridge concreto | Puede diseñarse y coordinarse como unidad entre disciplinas. | Si es distinto de un pipe rack o solo otra clase del mismo patrón. |
| Edificio o nave concretos | Suele reunir estructura, cimentación y varios modelos con entregas coordinadas. | Si el nombre identifica sistema, conjunto físico o contenedor espacial. |
| Sistema de cimentaciones de un área | Puede necesitar decisiones globales de terreno, cargas y coordinación. | Si es un sistema real o una agrupación conveniente de cimentaciones independientes. |
| Cimentación de un equipo concreto | Puede tener modelos y decisiones de cálculo propios. | Puede bastar una ocurrencia compuesta; quizá no sea un sistema. |
| Sistema de soportes de tubería de un área | Reúne soportes, interfaces y modelos de varias disciplinas. | Si existe una frontera y un ciclo reconocibles o solo una selección por disciplina. |

También conviene traer ejemplos que probablemente **no** sean sistemas de
ingeniería:

- una columna `C-101`: parece una ocurrencia individual;
- el archivo o modelo STAAD global: es un modelo, aunque cubra varios sistemas;
- «todos los HEB 300»: es una agrupación por propiedad;
- «todo lo visible en SP3D hoy»: es una selección dependiente de una herramienta;
- el proyecto completo: es un contexto superior y no demuestra por sí solo la
  necesidad del concepto intermedio.

### 6.4 Deberes antes de la sesión

Cada participante prepara únicamente lo siguiente:

1. **Lista corta:** entre tres y cinco cosas reales del proyecto que considere
   posibles sistemas de ingeniería. Deben tener nombre o alcance reconocible; no
   hace falta definirlas formalmente.
2. **Una ficha:** elegir el candidato más claro y responder las ocho preguntas de la
   tabla de la sección 6.1. Se admiten «no lo sé» y límites dudosos.
3. **Un contraejemplo:** aportar una cosa que al principio parezca sistema pero que
   probablemente sea solo una ocurrencia, un modelo, un espacio o una agrupación.
4. **Una evidencia concreta:** nombrar al menos dos modelos reales relacionados y,
   si es posible, una revisión o entrega de cada uno.
5. **Una decisión global:** describir una decisión real que afecte al candidato
   completo y que no pueda resolverse mirando una pieza aislada.

No se pide dibujar una arquitectura, decidir cardinalidades, enumerar todas las
ocurrencias ni usar las palabras `aggregate root`, `ownership` o «vista canónica».

#### Plantilla copiable

```text
Nombre del candidato:
¿Para qué lo tratamos como una unidad?:
¿Qué podría cambiar y seguir siendo el mismo?:
Dentro:
Fuera o compartido:
Elementos físicos importantes:
Modelos y entregas/revisiones conocidas:
Roles que mantienen o deciden:
Decisiones que afectan al conjunto:
Dudas:
```

### 6.5 Trabajo conjunto durante la sesión

Con las fichas delante, el equipo hará tres cosas:

1. **Unificar la lista:** detectar nombres repetidos, candidatos que son tipos en vez
   de instancias y elementos que pertenecen a otra categoría.
2. **Completar un único ejemplo:** elegir el candidato mejor conocido y dibujar una
   matriz sencilla de elementos físicos frente a modelos. En cada cruce bastará
   indicar «aparece», «no aparece», «efecto indirecto» o «no sabemos».
3. **Probar una conciliación:** escoger dos revisiones reales y explicar qué se
   compara, qué diferencias serían aceptables, quién decide y qué quedaría fuera.

Solo después de esta conversación se traducirán los resultados a identidad,
frontera, cardinalidades y reglas del modelo conceptual.

## 7. Criterios de salida

La iteración puede cerrarse cuando exista:

- una definición que resuelva al menos dos ejemplos y un contraejemplo;
- una distinción operativa frente a conjunto físico, sistema funcional y espacio;
- cardinalidades justificadas para sistemas, modelos y ocurrencias;
- un caso de conciliación reproducible con revisiones concretas;
- una decisión explícita: mantener, renombrar, fusionar o descartar el candidato.

El resultado seguirá `DRAFT` hasta aprobación humana. Solo después tendría sentido
evaluar si la frontera conceptual justifica un agregado, tablas, clases o API.
