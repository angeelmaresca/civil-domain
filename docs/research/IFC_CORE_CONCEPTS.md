# Fundamentos conceptuales de IFC

> **Status:** DRAFT  
> **Editable:** sí mientras figure como documento activo en `WORKING_SET.md`  
> **Document owner:** frente de investigación IFC  
> **Canonical for:** —  
> **Sources:** documentación oficial de IFC 4.3.2.0 enlazada en cada apartado  
> **Supersedes:** —  
> **Last reviewed:** 2026-09-09

## 1. Para qué leemos IFC

IFC —Industry Foundation Classes— es un estándar abierto para describir e
intercambiar información del entorno construido. La versión oficial utilizada en
este estudio es IFC 4.3.2.0. Su esquema abarca edificios e infraestructuras y contiene
también recursos compartidos de geometría, materiales, propiedades y relaciones.

No debe interpretarse como:

- el diseño de nuestra futura base de datos;
- el modelo interno ideal de una aplicación;
- una lista de clases que debamos copiar;
- una solución completa para la información de una planta industrial;
- una garantía de que todos los programas exportan el mismo contenido con igual
  calidad.

Lo estudiamos porque ha tenido que resolver durante años preguntas muy parecidas a
las nuestras: qué es un objeto, cómo se identifica, cómo se diferencia de su tipo,
dónde está, qué forma tiene, de qué material está hecho y cómo se relaciona con otros
objetos.

Fuente principal: [documentación oficial de IFC
4.3.2.0](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/).

## 2. El mapa mental mínimo

La parte central de IFC puede resumirse así:

```text
IfcRoot
├── IfcObjectDefinition       cosas tratadas semánticamente
│   ├── IfcObject             ocurrencias: objetos concretos
│   │   └── IfcProduct        objetos ubicables o representables
│   │       ├── IfcElement    componentes físicos de una instalación
│   │       ├── IfcSpatialElement
│   │       ├── IfcPort       puntos de conexión
│   │       └── otros productos físicos o no físicos
│   ├── IfcTypeObject         definiciones comunes reutilizables
│   └── IfcContext            contexto de proyecto o biblioteca
├── IfcRelationship           relaciones con identidad propia en el intercambio
└── IfcPropertyDefinition     conjuntos y plantillas de propiedades
```

El diagrama es deliberadamente incompleto. Su valor está en mostrar tres decisiones
de fondo:

1. las cosas del dominio no se confunden con las relaciones entre ellas;
2. una ocurrencia concreta no se confunde con la definición de su tipo;
3. la geometría y las propiedades no agotan el significado del objeto.

`IfcRoot` aporta a sus subtipos un identificador global, nombre y descripción
opcionales e información de ownership/historia opcional. Las entidades de recursos
geométricos, unidades o valores no descienden necesariamente de `IfcRoot` y no se
consideran objetos independientes del mismo modo. Véanse
[`IfcRoot`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcRoot.htm)
y [`IfcObjectDefinition`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcObjectDefinition.htm).

## 3. Ejemplo conductor: una viga dentro de un pipe rack

Podemos imaginar una viga concreta `B-101`:

```text
Proyecto industrial
└── emplazamiento o instalación
    └── contenedor espacial
        └── B-101                         ocurrencia física

Pipe rack PR-01 ──agrupa funcionalmente──► B-101
Tipo HEB 300 ─────define───────────────► B-101
B-101 ────────────tiene───────────────► placement local
B-101 ────────────tiene───────────────► representaciones geométricas
B-101 ────────────usa─────────────────► perfil/material
B-101 ────────────conecta con─────────► columna C-101
```

Esta lectura evita expresar toda la realidad mediante un único árbol. La viga puede
estar contenida en un lugar, pertenecer a un sistema, tener un tipo, conectarse con
otros elementos y participar en un modelo analítico. Cada afirmación responde a una
pregunta diferente.

## 4. Ocurrencia, tipo, clasificación y propiedad

Estas cuatro ideas suelen mezclarse al comenzar un modelo.

| Concepto | Pregunta | Ejemplo provisional |
|---|---|---|
| Ocurrencia | ¿Qué objeto concreto existe en este proyecto? | viga `B-101` |
| Tipo | ¿Qué definición común reutilizan varias ocurrencias? | tipo de viga con perfil y propiedades comunes |
| Clasificación | ¿Cómo lo sitúa un vocabulario externo? | código de una clasificación de productos o elementos |
| Propiedad | ¿Qué característica declaramos sobre el objeto o tipo? | resistencia, acabado, estado o fabricante |

En IFC, `IfcTypeObject` contiene información común a las ocurrencias que comparten
el tipo. La relación `IfcRelDefinesByType` une un tipo con una o muchas ocurrencias.
Una propiedad declarada directamente en la ocurrencia puede sobrescribir la
propiedad homónima procedente del tipo.

Esto sugiere un patrón útil, pero no obliga a permitir cualquier override en nuestro
dominio. Las reglas funcionales deben decidir qué características pueden variar por
ocurrencia.

Fuentes: [`IfcTypeObject`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcTypeObject.htm)
y [`IfcRelDefinesByType`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcRelDefinesByType.htm).

### Aplicación a nuestros grupos

`Pipe rack` podría ser simultáneamente:

- un término de clasificación;
- un tipo de sistema estructural;
- una estructura concreta `PR-01`;
- una agrupación funcional de elementos;
- un conjunto descompuesto en módulos.

El inventario debe preguntar cuál de estos significados se está utilizando, en vez
de dar por supuesto que existe una única entidad llamada `PipeRack`.

## 5. Producto, elemento y representación

`IfcProduct` representa una ocurrencia relacionada con un contexto geométrico o
espacial. Puede tener dos referencias principales:

- `ObjectPlacement`: establece su sistema de coordenadas;
- `Representation`: contiene una o varias representaciones geométricas o
  topológicas.

`IfcElement` especializa el concepto para los componentes que forman una instalación.
Incluye elementos permanentes y temporales e incluso elementos de vacío, como huecos.

La separación importante es:

```text
objeto B-101
    ├── identidad y significado
    ├── placement
    ├── representación de eje
    ├── representación de cuerpo
    ├── representación simplificada
    └── propiedades y materiales
```

La forma no tiene por qué ser la identidad del objeto. Además, un producto puede no
tener todavía geometría o puede disponer de varias representaciones para propósitos o
niveles de detalle distintos.

Fuentes: [`IfcProduct`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcProduct.htm),
[`IfcElement`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcElement.htm)
y [Product Geometric Representation](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/concepts/Product_Shape/Product_Geometric_Representation/content.html).

### Aplicación a una zapata

Una misma zapata podría conservar identidad mientras cambia entre:

- una representación paramétrica preliminar;
- un sólido detallado;
- una envolvente para coordinación;
- una representación para mediciones;
- una idealización analítica.

IFC confirma que separar objeto y representación es un problema real. Todavía no
confirma qué representaciones necesita nuestro dominio ni quién es propietario de
cada una.

## 6. Placement y sistemas de coordenadas

Un placement establece el sistema local en el que se expresan las representaciones
del producto. `IfcLocalPlacement` permite posicionarlo respecto al placement de otro
producto o directamente en el sistema global del proyecto.

```text
sistema del proyecto
└── sistema del emplazamiento
    └── sistema de la estructura
        └── sistema local de la viga
            └── puntos de su geometría
```

La ventaja es que mover una estructura puede expresarse cambiando una transformación
superior sin reescribir necesariamente todos los puntos de sus elementos. El riesgo
es crear cadenas difíciles de interpretar, ciclos o dependencias implícitas; IFC deja
algunas validaciones, como impedir ciclos de placements relativos, a las
aplicaciones.

Para nuestro dominio habrá que distinguir al menos:

- sistema global del proyecto;
- sistemas de referencia de planta o área;
- placement del objeto;
- coordenadas propias de una geometría;
- georreferenciación terrestre;
- sistemas propios del modelo analítico o de una aplicación externa.

Fuentes: [Product Placement](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/concepts/Product_Shape/Product_Placement/content.html),
[Product Local Placement](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/concepts/Product_Shape/Product_Placement/Product_Local_Placement/content.html)
y [`IfcLocalPlacement`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcLocalPlacement.htm).

## 7. No existe una única relación jerárquica

IFC utiliza relaciones objetivadas: la relación es un objeto del intercambio y puede
tener identidad, nombre, descripción y semántica propia. Las relaciones principales
no son intercambiables.

| Relación conceptual | Qué expresa | Ejemplo civil |
|---|---|---|
| Contención espacial | dónde se considera contenido principalmente un objeto | viga contenida en un nivel o una parte de instalación |
| Referencia espacial | otros espacios o niveles relevantes sin cambiar su contenedor principal | columna que atraviesa varios niveles |
| Agregación | composición todo–parte no ordenada y con dependencia | pórtico compuesto por elementos o assembly compuesto por piezas |
| Nesting | composición ordenada o de elementos subordinados | puertos pertenecientes a un equipo |
| Asignación a grupo/sistema | pertenencia funcional sin implicar ownership | vigas asignadas a un sistema estructural |
| Conectividad | unión o interacción entre objetos | viga conectada con columna |
| Tipado | aplicación de una definición común a ocurrencias | varias vigas definidas por un tipo |
| Asociación | referencia a material, clasificación, biblioteca o documento | viga asociada a acero y a un código externo |

La contención espacial de IFC es jerárquica: un elemento tiene como máximo un
contenedor espacial principal, aunque puede referenciar otros. La agregación también
implica dependencia y cada objeto solo puede ocupar una posición en esa descomposición.
La asignación a grupos no implica por sí sola esa dependencia.

Esto refuerza una lección ya encontrada en Footings: ownership, parent físico,
asignación estructural y propagación de cargas no deben reducirse a un enlace
genérico.

Fuentes: [`IfcObjectDefinition`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcObjectDefinition.htm),
[Spatial Structure](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/concepts/Object_Connectivity/Spatial_Structure/content.html),
[`IfcRelContainedInSpatialStructure`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcRelContainedInSpatialStructure.htm)
y [`IfcBuiltSystem`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcBuiltSystem.htm).

### Consecuencia para nuestro modelo

No deberíamos dibujar al principio un único árbol como:

```text
Planta > estructura > viga > placa > perno
```

Esa expresión oculta preguntas diferentes:

- ¿dónde está cada objeto?;
- ¿qué lo posee durante su lifecycle?;
- ¿de qué partes se compone?;
- ¿a qué sistema funcional pertenece?;
- ¿con qué se conecta?;
- ¿por dónde se transmiten acciones?;

## 8. Sistemas, assemblies, partes y características

`IfcBuiltSystem` agrupa elementos que comparten una función dentro de la instalación.
Puede además descomponerse jerárquicamente en subsistemas.

`IfcElementAssembly` representa un conjunto complejo agregado a partir de varios
elementos. Su geometría puede surgir de la geometría de las partes o disponer además
de una representación propia.

Una característica geométrica no tiene por qué convertirse en un elemento
independiente. IFC dispone, por ejemplo, de conceptos para huecos, proyecciones y
aspectos identificables de la forma.

Aplicado al dominio civil:

| Concepto | Posible lectura inicial |
|---|---|
| Pipe rack | sistema funcional, estructura concreta o ambas cosas |
| Pórtico | assembly de vigas y columnas o sistema estructural |
| Conjunto de anclaje | assembly de pernos, tuercas y arandelas |
| Hueco en zapata | característica que modifica un elemento, no necesariamente elemento autónomo |
| Recrecido | parte agregada, característica o elemento con lifecycle propio según el caso |

Fuentes: [`IfcBuiltSystem`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcBuiltSystem.htm),
[`IfcElementAssembly`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcElementAssembly.htm)
y [`IfcShapeAspect`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcShapeAspect.htm).

## 9. Material simple y composición material

IFC no limita un elemento a un único campo `material`. Distingue varias formas de
asociación:

- material único;
- conjunto de capas con orden y espesores;
- conjunto de perfiles, útil para elementos extruidos;
- conjunto de constituyentes, útil cuando hay partes o materiales diferenciados sin
  una disposición por capas o perfiles.

Los aspectos de forma pueden utilizarse para relacionar un constituyente material
con una parte identificable de la representación geométrica.

```text
elemento
├── material único
├── capas: material + orden + espesor
├── perfiles: sección + material + disposición
└── constituyentes: papel o parte + material
```

La lección no es adoptar esas cuatro clases literalmente. Es evitar que una temprana
relación `Elemento.materialID` cierre la puerta a vigas mixtas, recubrimientos,
elementos por fases o geometrías con regiones materiales distintas.

Fuentes: [Material Association](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/concepts/Object_Association/Material_Association/content.html),
[Material Set](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/concepts/Object_Association/Material_Association/Material_Set/content.html)
y [`IfcMaterialConstituent`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcMaterialConstituent.htm).

## 10. Puertos e interfaces

`IfcPort` representa el medio por el que un elemento se conecta con otro. Un puerto
fijo se subordina al elemento mediante nesting, se posiciona en el sistema local de
ese elemento y se conecta con otro puerto mediante una relación explícita.

Este patrón puede ser útil para estudiar:

- puntos de apoyo de equipos;
- interfaces de entrega de cargas;
- extremos de miembros;
- conexiones entre módulos;
- puntos o superficies de anclaje.

Sin embargo, no todas las interfaces civiles son puntos ni todas conectan exactamente
dos elementos. Una placa base, una superficie de contacto suelo–zapata o un grupo de
pernos pueden requerir otra semántica. Debemos estudiar el patrón, no generalizarlo
sin evidencia.

Fuente: [`IfcPort`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcPort.htm).

## 11. Propiedades y extensión del modelo

IFC mantiene un núcleo tipado y permite añadir información mediante property sets,
clasificaciones y referencias externas. También admite valores `USERDEFINED` en
determinadas enumeraciones y dispone de objetos proxy para casos no cubiertos.

Esto permite crecer sin añadir una nueva clase del esquema por cada propiedad local,
pero introduce riesgos:

- propiedades duplicadas con nombres distintos;
- semántica oculta en texto libre;
- pérdida de interoperabilidad;
- uso del objeto genérico como cajón de sastre;
- dependencia de acuerdos externos que no están versionados conjuntamente.

Para nuestro trabajo conviene separar:

```text
concepto estructural estable
clasificación o vocabulario externo
propiedad definida y tipada
valor de una ocurrencia
requisito de que ese valor sea entregado
```

bSDD e IDS se estudiarán posteriormente porque abordan las dos últimas fronteras de
forma más específica.

## 12. Modelo físico y modelo analítico

`IfcProduct` incluye tanto elementos físicos como objetos analíticos, pero IFC no los
confunde. `IfcStructuralItem` y `IfcStructuralActivity` forman parte de un dominio
específico que relaciona miembros, conexiones y acciones dentro de un modelo de
análisis.

Este informe solo fija la separación general. El siguiente frente deberá estudiar
en detalle:

- relación entre elemento físico y miembro analítico;
- nodos, curvas, superficies y sólidos;
- apoyos y conexiones;
- acciones, casos, combinaciones y resultados;
- varios modelos analíticos para un mismo conjunto físico.

Fuente: [IFC Structural Analysis Domain](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/ifcstructuralanalysisdomain/content.html).

## 13. Qué aporta IFC a nuestros grupos de exploración

| Grupo del inventario | Aportación de IFC que conviene estudiar |
|---|---|
| Tipos de estructuras | sistema, grupo, assembly, espacialidad y descomposición |
| Equipos e interfaces | producto, tipo, occurrence, port y conectividad |
| Superestructura | elementos especializados, partes, perfiles y materiales |
| Cimentación | footing, pile, deep foundation, assembly, features y materiales |
| Terreno y geotecnia | elementos geográficos, estratos y propiedades; cobertura por validar |
| Acciones y cargas | structural activities y agrupaciones; pendiente del frente analítico |
| Modelo analítico | structural items, connections y models; pendiente del frente analítico |
| Coordenadas y geometría | placement, representación múltiple, forma y georreferenciación |

## 14. Candidatos que propone esta primera lectura

Estos términos deben contrastarse antes de trasladarlos al inventario:

- ocurrencia de objeto;
- tipo de objeto;
- clasificación externa;
- definición y conjunto de propiedades;
- producto o elemento físico;
- elemento espacial y contenedor espacial;
- sistema funcional;
- assembly, parte y característica;
- placement y sistema de coordenadas;
- representación geométrica y propósito de representación;
- asignación y composición material;
- puerto o interfaz;
- relación de contención, agregación, grouping, conectividad y referencia;
- correspondencia entre elemento físico y objeto analítico.

No se propone conservar los nombres IFC ni convertir todos estos términos en
entidades propias.

## 15. Lecciones aplicables provisionalmente

1. **Una única jerarquía no basta.** Espacialidad, composición, sistema y conexión
   forman grafos con semánticas diferentes.
2. **El objeto no es su geometría.** Identidad, placement y representación deben
   poder razonarse por separado.
3. **Tipo no es clasificación.** Un tipo aporta una definición reutilizable; una
   clasificación sitúa el objeto en un vocabulario.
4. **Las relaciones pueden necesitar semántica propia.** No deben reducirse todas a
   un `parentID` genérico.
5. **La composición material debe permanecer abierta.** Un único material por
   elemento no cubre todos los casos.
6. **Físico y analítico son vistas relacionadas.** No se presupone correspondencia
   uno a uno.
7. **Extensibilidad requiere gobierno.** Permitir propiedades libres sin diccionario
   ni procedencia desplaza el problema en vez de resolverlo.

## 16. Qué no conviene copiar automáticamente

- la extensa jerarquía de herencia de IFC;
- sus nombres técnicos y decisiones condicionadas por compatibilidad histórica;
- la cardinalidad exacta de cada relación sin validar nuestros casos;
- un único contenedor espacial principal si el dominio industrial requiere otra
  navegación;
- la estrategia de GUID o `OwnerHistory` como modelo completo de revisiones;
- property sets libres como sustituto de conceptos bien definidos;
- objetos proxy como solución ordinaria;
- la serialización IFC como esquema interno de persistencia.

## 17. Preguntas para la revisión con el equipo

1. ¿`Pipe rack`, `edificio` o `estructura soporte` son sistemas, assemblies,
   contenedores espaciales o combinaciones de varios conceptos?
2. ¿Qué diferencia práctica habrá entre tipo estructural, clasificación y plantilla
   de creación?
3. ¿Qué elementos necesitan más de una representación geométrica conservada?
4. ¿Qué relaciones necesitan identidad, propiedades o revisión propias?
5. ¿Qué interfaces civiles se parecen a un puerto y cuáles son superficies o
   conjuntos más complejos?
6. ¿Puede un elemento formar parte de un único assembly físico pero pertenecer a
   varios sistemas funcionales?
7. ¿Qué jerarquías de coordenadas usamos realmente en plantas industriales?
8. ¿Cómo deben convivir geometría nominal, geometría de diseño, geometría calculada y
   geometría construida?
9. ¿Qué materiales compuestos o asignaciones por regiones aparecen en nuestros casos
   habituales?
10. ¿Qué identidad necesitamos preservar al importar y exportar repetidamente con
    herramientas BIM?

## 18. Fuentes oficiales consultadas

- [IFC 4.3.2.0](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/)
- [IFC Kernel](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/ifckernel/content.html)
- [`IfcRoot`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcRoot.htm)
- [`IfcObjectDefinition`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcObjectDefinition.htm)
- [`IfcTypeObject`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcTypeObject.htm)
- [`IfcRelDefinesByType`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcRelDefinesByType.htm)
- [`IfcProduct`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcProduct.htm)
- [`IfcElement`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcElement.htm)
- [Product Shape](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/concepts/Product_Shape/content.html)
- [Product Local Placement](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/concepts/Product_Shape/Product_Placement/Product_Local_Placement/content.html)
- [Spatial Structure](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/concepts/Object_Connectivity/Spatial_Structure/content.html)
- [`IfcRelContainedInSpatialStructure`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcRelContainedInSpatialStructure.htm)
- [`IfcBuiltSystem`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcBuiltSystem.htm)
- [`IfcElementAssembly`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcElementAssembly.htm)
- [`IfcPort`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcPort.htm)
- [Material Association](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/concepts/Object_Association/Material_Association/content.html)
- [Material Set](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/concepts/Object_Association/Material_Association/Material_Set/content.html)
- [`IfcShapeAspect`](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcShapeAspect.htm)
- [IFC Structural Analysis Domain](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/ifcstructuralanalysisdomain/content.html)
