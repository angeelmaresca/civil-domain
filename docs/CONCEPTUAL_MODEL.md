# Modelo conceptual inicial

> **Status:** DRAFT  
> **Editable:** no mientras no figure como documento activo en `WORKING_SET.md`  
> **Document owner:** equipo de dominio civil  
> **Canonical for:** —  
> **Sources:** conversaciones iniciales del equipo y referencias comparativas  
> **Supersedes:** —  
> **Last reviewed:** 2026-09-08

## Propósito de esta fase

Conceptualizar de manera genérica y robusta los elementos civiles y estructurales
que intervienen en la construcción de una planta industrial: vigas, columnas,
zapatas, pedestales, cargas, pernos, equipos y otros conceptos relacionados.

Este documento recoge hipótesis de partida. No define todavía un modelo canónico ni
una estructura de base de datos.

El descubrimiento continúa en [`ELEMENT_INVENTORY.md`](ELEMENT_INVENTORY.md). Este
documento se conserva como referencia para no convertir sus hipótesis iniciales en
conclusiones durante el inventario.

## Problema inicial

Una primera cuestión es cómo representar elementos que conservan un significado
estructural reconocible, pero pueden adoptar geometrías muy diferentes.

El ejemplo inicial es la zapata:

- una entidad específica podría expresar correctamente su función e invariantes,
  pero sería frágil si intentase enumerar todas sus geometrías mediante campos;
- un elemento geométrico completamente genérico permitiría cualquier forma, pero no
  expresaría por sí mismo si actúa como zapata, viga, pedestal u otro elemento.

## Hipótesis de trabajo

La alternativa inicial que se estudiará combina significado y representación:

```text
elemento con significado civil o estructural
        ├── representación geométrica
        ├── asignación o composición de materiales
        ├── posición y sistema de coordenadas
        ├── relaciones con otros elementos
        └── representación analítica, cuando exista
```

Según esta hipótesis, una zapata puede conservar su identidad y función aunque su
geometría sea rectangular, escalonada, combinada, irregular o libre. La geometría
no determina por sí sola el significado del elemento.

Esto no decide todavía si los tipos se implementarán mediante entidades separadas,
clasificaciones, composición, capacidades o herencia.

## Distinciones que deben conservarse

### Elemento físico y representación geométrica

El elemento representa una realidad del dominio. La geometría describe una forma de
representarlo. Puede ser necesario admitir distintas representaciones o niveles de
detalle para un mismo elemento.

### Modelo físico y modelo analítico

Una idealización de cálculo no tiene por qué corresponder uno a uno con el elemento
construido. Una columna puede convertirse en una barra analítica y una zapata puede
representarse mediante una superficie, varios elementos finitos o unas condiciones
equivalentes.

### Elemento y acción

Una carga no se considera inicialmente un elemento físico. Es una acción, con origen
y condiciones propias, aplicada sobre un objetivo físico o analítico.

### Elemento simple y elemento compuesto

No debe asumirse que todo elemento posee una sola geometría o un solo material.
Pernos, armaduras, insertos, placas, recrecidos y elementos mixtos exigirán estudiar
partes, conjuntos y relaciones de composición.

### Equipo y dominio civil

Un equipo es físico, pero no se presupone que toda su definición pertenezca al
dominio civil. El modelo civil puede necesitar conocer su identidad de referencia,
interfaces de apoyo, geometría relevante y acciones transmitidas.

## Relación inicial con Footings

La hipótesis actual es compartir identidad y significado para los conceptos comunes,
sin obligar a Footings a utilizar directamente las futuras tablas o clases del
modelo civil.

```text
elemento civil + revisión + geometría + materiales + acciones
                            │
                            ▼
                 adaptación explícita a Footings
                            │
                            ▼
             hipótesis + cálculo + comprobaciones + resultados
```

Footings podría trabajar con una proyección o snapshot adaptado al cálculo y devolver
resultados referidos a la identidad y revisión del elemento civil. Así se evita crear
dos conceptos independientes de zapata y, al mismo tiempo, se evita acoplar el motor
de cálculo a la persistencia general.

Permanece abierta la responsabilidad sobre las modificaciones: Footings podría
consumir un diseño civil existente o producir una propuesta de nueva revisión.

## Referencias comparativas iniciales

Estas referencias no son autoridad sobre el modelo propio:

- IFC separa el significado de `IfcFooting` de la colocación y las representaciones
  disponibles mediante su jerarquía de productos.
- IFC mantiene también un dominio de análisis estructural diferenciado del modelo
  físico.
- CADMATIC combina objetos especializados, como vigas y placas, con componentes
  estructurales paramétricos construidos mediante primitivas y formas 3D.
- Tekla combina partes estructurales reconocibles con elementos genéricos para formas
  que no encajan en sus operaciones habituales.

Enlaces de partida:

- <https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcFooting.htm>
- <https://standards.buildingsmart.org/IFC/DEV/IFC4_3/HTML/lexical/IfcProduct.html>
- <https://standards.buildingsmart.org/IFC/DEV/IFC4_3/HTML/ifcstructuralanalysisdomain/content.html>
- <https://docs.cadmatic.com/plant/Content/Component%20Modeller/componentmodeller.htm>
- <https://support.tekla.com/doc/tekla-structures/2025/mod_create_parts>

## Preguntas para el caso inicial

Al recorrer el ejemplo de zapata, pedestal, placa base, pernos, equipo y cargas habrá
que responder, sin precipitar una solución técnica:

1. ¿Qué objetos poseen identidad y ciclo de vida propios?
2. ¿Qué objetos son partes de otros y cuáles solo están relacionados?
3. ¿Dónde termina el significado de un elemento y comienza su geometría?
4. ¿A qué nivel se asigna un material cuando existen varias partes?
5. ¿Cómo se relacionan el elemento físico y sus posibles modelos analíticos?
6. ¿Qué datos son compartidos con Footings y cuáles pertenecen exclusivamente al
   contexto de cálculo?
7. ¿Quién puede crear una nueva revisión del diseño físico?
