# Guía de estudio — fundamentos del dominio civil

> **Status:** DRAFT
> **Editable:** sí; material didáctico derivado incluido en `WORKING_SET.md`
> **Document owner:** coordinación del dominio civil
> **Canonical for:** —
> **Sources:** [fundamentos IFC](../research/IFC_CORE_CONCEPTS.md), [enunciado de la primera iteración](../iteration-01/ENUNCIADO.md), [síntesis](../iteration-01/SINTESIS.md) y fichas de [Ángel](../iteration-01/FICHA_ANGEL_COLUMNA.md), [Luis](../iteration-01/FICHA_LUIS_ZAPATA.md) y [Miguel](../iteration-01/FICHA_MIGUEL_ACCIONES_CARGAS.md)
> **Supersedes:** —
> **Last reviewed:** 2026-09-17

## Cómo utilizar esta guía

Esta guía reorganiza el material actual para poder estudiarlo sin conexión. No
define todavía el dominio civil. Las fichas y la síntesis siguen en `DRAFT`, la
ficha de Alberto aún no está incorporada y la de Luis sigue pendiente de revisión.

Ruta sugerida:

1. estudiar las separaciones conceptuales;
2. recorrer el caso común EQ-101 → terreno;
3. comparar objeto físico, modelos analíticos y acciones;
4. resolver el [cuaderno](STUDY_WORKBOOK.md);
5. revisar las [respuestas](STUDY_ANSWERS.md) y volver a las fuentes.

## 1. Por qué estudiamos IFC

IFC es una referencia que ha tenido que resolver identidad, objetos, tipos,
geometría, materiales, propiedades y relaciones durante décadas. Lo usamos como
mapa de preguntas, no como diseño de nuestra base de datos.

El mapa mínimo es:

```text
IfcRoot
├── IfcObjectDefinition
│   ├── IfcObject       ocurrencias concretas
│   ├── IfcTypeObject   definiciones reutilizables
│   └── IfcContext      contexto del intercambio
├── IfcRelationship     relaciones explícitas
└── IfcPropertyDefinition
```

Las lecciones importantes no son los nombres `Ifc*`, sino estas separaciones:

- las cosas no son sus relaciones;
- una ocurrencia no es su tipo;
- geometría y propiedades no agotan el significado de un objeto;
- una jerarquía única no puede representar todos los vínculos;
- intercambio y modelo interno tienen objetivos distintos.

## 2. Ocurrencia, tipo, clasificación y propiedad

Supongamos una columna concreta `C-101`:

| Concepto | Pregunta | Ejemplo |
|---|---|---|
| Ocurrencia | ¿Qué objeto concreto es? | La columna C-101 instalada en ST-01 |
| Tipo | ¿Qué definición reutilizable comparte? | Perfil/material/configuración común |
| Clasificación | ¿Cómo la categoriza un sistema externo? | Código IFC, bSDD o corporativo |
| Propiedad | ¿Qué dato describe al objeto o tipo? | Longitud, resistencia, fase, acabado |

Errores típicos:

- usar el TAG o el perfil como identidad interna;
- crear un subtipo de dominio por cada código de clasificación;
- tratar cualquier conjunto de propiedades como definición de tipo;
- asumir que dos objetos del mismo tipo tienen el mismo estado o placement.

La identidad debe sobrevivir a cambios razonables. Una columna puede cambiar de
perfil o longitud durante el diseño y seguir representando la misma ocurrencia.

## 3. Función y geometría no son lo mismo

Una zapata no es «un sólido de hormigón»; es un elemento con función de cimentación,
relaciones con la estructura y el terreno, materiales y comportamiento esperado.

Un mismo objeto puede tener varias representaciones:

```text
Footing F-101
├── geometría paramétrica editable
├── sólido detallado calculado
├── envolvente de coordinación
├── símbolo en planta
└── representación analítica
```

Cambiar la representación no crea automáticamente otro objeto físico. También debe
distinguirse placement de geometría:

- placement responde «dónde y con qué orientación»;
- geometría responde «qué forma se representa»;
- sistema de coordenadas explica respecto a qué marco se expresan ambos.

## 4. Un objeto físico puede tener varios modelos analíticos

La columna C-101 puede idealizarse de distintas formas:

```text
PhysicalColumn C-101
├── mapping → una barra entre ejes
├── mapping → dos barras + nodo rígido
└── mapping → superficies o sólidos para análisis local
```

Los nodos, offsets, releases, ejes locales y mallas pertenecen al modelo analítico,
no necesariamente al objeto físico. La correspondencia puede ser:

- uno a uno;
- uno a varios;
- varios objetos físicos a un objeto analítico;
- diferente para cada propósito o aplicación.

Por eso `staadNodeID` o `sapMemberID` no deberían convertirse sin más en identidad
del objeto civil. Son referencias externas dentro de una correspondencia con
procedencia y revisión.

## 5. Relaciones: el dominio es un grafo

En el caso común aparecen muchas líneas:

```text
Equipo EQ-101
└── estructura ST-01
    └── columna C-101
        └── placa BP-101 + pernos
            └── grout G-101
                └── pedestal PD-101
                    └── zapata F-101
                        └── terreno
```

El dibujo vertical no significa que todas sean parent-child. Debemos preguntar qué
expresa cada vínculo:

| Relación | Pregunta |
|---|---|
| Ownership | ¿Quién controla creación y borrado? |
| Contención espacial | ¿Dónde está ubicado? |
| Pertenencia a sistema | ¿En qué sistema funcional participa? |
| Composición | ¿Qué partes forman un conjunto? |
| Conexión | ¿Qué objetos une y con qué comportamiento? |
| Apoyo/contacto | ¿Dónde y cómo transmite interacción? |
| Asignación analítica | ¿Qué objeto representa a cuál en un modelo? |

Un objeto puede estar contenido en un área, pertenecer a dos sistemas y conectar
con otros sin que esas relaciones definan su lifecycle.

## 6. Cuándo una conexión necesita identidad o datos propios

Una conexión deja de ser una simple referencia cuando necesitamos describirla:

- posición o geometría de interfaz;
- rigidez, releases o capacidad;
- holgura, fricción o contacto;
- patrón de pernos o componentes;
- estado, revisión o procedencia;
- correspondencia con conexiones analíticas.

La ficha de Alberto todavía debe contrastar este frente. Por eso no se aprueba aquí
una entidad universal `Connection`; solo se aprende a reconocer cuándo una relación
porta información que no pertenece limpiamente a ninguno de sus extremos.

## 7. Acción, carga, caso, combinación y resultado

Una carga no es simplemente un número guardado en la zapata. El recorrido conceptual
es:

```text
fuente física
  ↓ origina
Action
  ↓ se agrupa bajo una hipótesis
LoadCase
  ↓ se aplica a una representación concreta
AppliedLoad
  ↓ participa en
Combination
  ↓ análisis
Result / Envelope / Check
```

Aspectos que deben acompañar a una acción o aplicación:

- origen y disciplina propietaria;
- magnitud, unidad y naturaleza física;
- punto, línea, superficie o volumen de aplicación;
- sistema de coordenadas y convenio de signos;
- revisión del objeto y modelo utilizados;
- transformación o aproximación realizada.

La misma acción del equipo puede aplicarse a un nodo en un modelo y repartirse sobre
una barra o superficie en otro. La acción física puede ser la misma; la aplicación
analítica no.

## 8. Zapata, terreno y métodos de análisis

La zapata F-101 ilustra varias distinciones:

- objeto físico frente a su geometría;
- cuerpo de hormigón frente a armadura, insertos o recrecidos;
- pertenencia al conjunto de cimentación frente a contacto con terreno;
- condiciones geotécnicas asignadas frente a estratos reales;
- modelo manual, algorítmico, de placas o de sólidos;
- cálculo frente a aprobación técnica.

Dos análisis diferentes no crean dos zapatas. Cada ejecución debe registrar método,
inputs, configuración, revisión física y resultados. La validación técnica humana es
otra dimensión: un resultado reproducible no está automáticamente aprobado.

## 9. Procedencia, revisión y vigencia

Para un dato importado conviene poder responder:

1. ¿de qué sistema y objeto externo procede?;
2. ¿qué revisión o snapshot se utilizó?;
3. ¿la traducción fue exacta, normalizada, aproximada o no soportada?;
4. ¿sigue alineado con el objeto físico actual?;
5. ¿quién aprobó el uso del resultado y para qué propósito?

Estas preguntas separan:

- trazabilidad histórica;
- vigencia técnica;
- calidad de traducción;
- aprobación humana.

No deben comprimirse en un único booleano `isValid`.

## 10. Footings como caso especializado

Footings aporta evidencia real sobre cimentaciones y camino de cargas. Algunas
correspondencias útiles son:

| Footings | Pregunta para Civil Domain |
|---|---|
| DesignElement | ¿Qué unidad física o de diseño comparte identidad? |
| `parentElementID` | ¿Qué relaciones físicas caben realmente en un parent `0..1`? |
| Support → receptor | ¿Cómo se representa una interfaz de entrega de acciones? |
| TieBeam endpoints | ¿Qué conexiones requieren extremos explícitos? |
| ElementSelectionSet | ¿Cómo separar selección operacional de sistema o assembly? |
| Calculate/Check | ¿Qué pertenece al objeto y qué a modelos o ejecuciones analíticas? |

Civil Domain no debe copiar Footings. Footings tampoco debe implementar un modelo
BIM genérico. Primero se estabilizan vocabulario y correspondencias; compartir
código o persistencia será una decisión posterior basada en casos compatibles.

## 11. Señales de un modelo frágil

Conviene detenerse cuando aparece alguno de estos síntomas:

- un único `parentID` significa ownership, ubicación, sistema y apoyo;
- el TAG, coordenadas o perfil actúan como identidad;
- una acción variable vive como campo fijo del objeto físico;
- el objeto físico contiene IDs directos de una sola herramienta analítica;
- la única geometría posible determina el significado del objeto;
- `isValid` mezcla actualidad, convergencia, aprobación y calidad de importación;
- se crean clases internas copiando una jerarquía IFC sin caso funcional.

## 12. Vocabulario provisional para recordar

- Ocurrencia: objeto concreto con identidad.
- Tipo: definición reutilizable para varias ocurrencias.
- Clasificación: etiqueta de un sistema de conocimiento externo.
- Placement: posición y orientación respecto a un marco.
- Representación: una forma de mostrar o idealizar el objeto.
- Conexión/interfaz: relación localizada que puede tener comportamiento propio.
- Acción: fenómeno físico originado por una fuente.
- Aplicación de carga: proyección de una acción sobre un modelo analítico.
- Modelo analítico: idealización para un propósito de cálculo.
- Mapping físico–analítico: correspondencia trazable entre ambos planos.
- Provenance: origen, transformación y revisión de la información.

Estos términos son material de estudio. El equipo todavía debe acordar su
vocabulario mínimo.

## Fuentes para profundizar

- [Fundamentos conceptuales de IFC](../research/IFC_CORE_CONCEPTS.md).
- [Enunciado y batería común](../iteration-01/ENUNCIADO.md).
- [Síntesis transversal](../iteration-01/SINTESIS.md).
- [Columna física y analítica](../iteration-01/FICHA_ANGEL_COLUMNA.md).
- [Zapata y encepado](../iteration-01/FICHA_LUIS_ZAPATA.md).
- [Acciones y cargas](../iteration-01/FICHA_MIGUEL_ACCIONES_CARGAS.md).
- [Mapa de referencias BIM](../BIM_REFERENCE_MAP.md).
