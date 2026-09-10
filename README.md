# Civil Domain

Este repositorio inicia la definición de un dominio civil y estructural capaz de
describir los elementos que intervienen en una planta industrial y las relaciones
entre ellos.

Queremos poder razonar sobre estructuras, equipos, vigas, columnas, cimentaciones,
pedestales, pernos, terreno, cargas, coordenadas y modelos analíticos sin diseñar cada
familia como un caso aislado. El modelo deberá crecer durante años, por lo que ahora
nos importa más separar bien los conceptos que cerrar rápidamente tablas o clases.

## En qué fase estamos

Estamos en una fase de **investigación y descubrimiento de conceptos**.

Antes de definir entidades propias estudiaremos cómo BIM, los estándares
estructurales y los modelos de información de plantas industriales resuelven
problemas similares. IFC es la primera referencia, pero no será nuestro modelo ni
una autoridad automática.

Buscamos principalmente:

- conceptos que todavía no hemos identificado;
- separaciones útiles entre objeto, tipo, clasificación, propiedad, geometría,
  material y representación analítica;
- relaciones distintas de una jerarquía padre–hijo;
- mecanismos que permitan ampliar el dominio sin rehacerlo;
- complejidad de otros modelos que no necesitamos copiar.

## Qué no estamos haciendo todavía

En esta fase no vamos a:

- diseñar la base de datos;
- cerrar una jerarquía definitiva de entidades;
- reproducir IFC, CADMATIC, Tekla, Revit u otro software;
- crear una clase por cada término encontrado;
- decidir prematuramente qué código o persistencia compartirán Civil Domain y
  Footings.

Las conclusiones actuales son hipótesis `DRAFT` hasta que el equipo las revise.

## Antes de la primera sesión

Para llegar un poco más informados es suficiente con leer
[Fundamentos conceptuales de IFC](docs/research/IFC_CORE_CONCEPTS.md). No se espera
que nadie domine IFC, cierre conclusiones ni prepare una entrega antes de la sesión.

Como propuesta opcional, quien quiera puede:

1. Elegir uno de estos ejemplos: pipe rack, viga, equipo sobre cimentación, zapata o
   viga de atado.
2. Anotar, sin intentar modelarlo todavía:
   - qué objetos aparecen;
   - qué relaciones existen;
   - qué parte es física, analítica o una interfaz;
   - una duda o desacuerdo provocado por la lectura.

Estos posibles «deberes» solo pretenden facilitar la conversación: no son una tarea
asignada ni una condición para participar. Tampoco es necesario leer el esquema
completo de IFC o investigar individualmente las demás fuentes.

## Objetivo de la primera sesión

Utilizaremos los ejemplos para comprobar si compartimos el significado de los
conceptos básicos. La sesión debe terminar con:

- un vocabulario provisional, no definitivo;
- preguntas que requieran investigación;
- un primer reparto de frentes;
- acuerdo sobre qué no intentaremos resolver todavía.

El reparto inicial propuesto para cuatro personas es una base para discutir y
ajustar durante la sesión; todavía no representa tareas asignadas:

| Frente | Referencias y pregunta principal |
|---|---|
| Modelo físico y semántico | IFC: objetos, tipos, sistemas, geometría, materiales y relaciones |
| Modelo estructural analítico | IFC Structural Analysis y SAF: nodos, miembros, conexiones, cargas y correspondencia físico–analítica |
| Información de planta industrial | CFIHOS y DEXPI: planta, equipo, TAG, interfaces y lifecycle de información |
| Clasificación y requisitos | bSDD, Uniclass e IDS: clases, propiedades y requisitos de entrega |

Este reparto sirve para investigar en paralelo; no asigna ownership permanente sobre
partes del futuro dominio.

## Cómo entregar una primera investigación

Una vez que el reparto se acuerde durante la sesión, y no como preparación previa,
cada frente debería traer una aportación breve y comparable:

- hasta 5 conceptos relevantes;
- 3 separaciones conceptuales útiles;
- 2 riesgos de copiar la referencia;
- 1 ejemplo industrial explicado;
- 3 preguntas para el equipo.

La plantilla común y las fuentes iniciales están en el
[mapa de referencias BIM](docs/BIM_REFERENCE_MAP.md).

## Relación con Footings

Footings aporta casos reales sobre cimentaciones, elementos físicos, asignación y
transmisión de cargas. Es una fuente importante y un banco de pruebas, pero su modelo
especializado no define por sí solo todo el dominio civil.

Inicialmente compartiremos vocabulario y correspondencias conceptuales. Solo se
planteará compartir código, entidades o persistencia cuando existan conceptos
estables y casos reales compatibles en ambos proyectos.

## Cómo orientarse en el repositorio

- [WORKING_SET.md](docs/WORKING_SET.md): estado actual, único frente editable y
  siguiente acción. Es la puerta de entrada para trabajar.
- [FIRST_ITERATION.md](docs/FIRST_ITERATION.md): batería de preguntas, reparto
  inicial y ejemplo resuelto para preparar la próxima discusión.
- [IFC_CORE_CONCEPTS.md](docs/research/IFC_CORE_CONCEPTS.md): primera explicación
  didáctica y preguntas para el equipo.
- [BIM_REFERENCE_MAP.md](docs/BIM_REFERENCE_MAP.md): mapa de investigaciones,
  plantilla y posibles frentes.
- [ELEMENT_INVENTORY.md](docs/ELEMENT_INVENTORY.md): inventario preliminar de
  elementos y categorías; permanece en consulta durante la investigación.
- [CONCEPTUAL_MODEL.md](docs/CONCEPTUAL_MODEL.md): planteamiento conceptual inicial,
  también pendiente de contrastar.
- [AGENTS.md](AGENTS.md): reglas para agentes y colaboradores que modifiquen el
  repositorio.

La estructura del repositorio crecerá únicamente cuando exista contenido real que
lo justifique. Antes de editar, empezar siempre por
[WORKING_SET.md](docs/WORKING_SET.md).

## Versiones PDF

Para lectura o distribución sin herramientas adicionales:

- [Introducción al repositorio](README.pdf).
- [Fundamentos conceptuales de IFC](docs/research/IFC_CORE_CONCEPTS.pdf).

Los archivos Markdown son las fuentes editables. Los PDF son copias generadas y
deben regenerarse cuando cambie su documento de origen.
