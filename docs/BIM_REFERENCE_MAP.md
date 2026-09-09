# Mapa de referencias BIM y de planta industrial

> **Status:** DRAFT  
> **Editable:** sí mientras figure como documento activo en `WORKING_SET.md`  
> **Document owner:** equipo de dominio civil  
> **Canonical for:** —  
> **Sources:** estándares abiertos y documentación oficial enlazados por referencia  
> **Supersedes:** —  
> **Last reviewed:** 2026-09-09

## 1. Objetivo

Estudiar cómo otros estándares y aplicaciones han conceptualizado el entorno
construido, el análisis estructural y las instalaciones industriales antes de
continuar definiendo el dominio propio.

La investigación debe servir para:

- descubrir conceptos que falten en el inventario;
- reconocer separaciones conceptuales ya contrastadas por la industria;
- comprender mecanismos de crecimiento y extensión;
- anticipar necesidades de interoperabilidad;
- evitar copiar complejidad que responda a problemas distintos de los nuestros.

No se pretende reproducir IFC, CFIHOS, DEXPI, SAF ni el modelo interno de un software.

## 2. Preguntas comunes para cada referencia

1. ¿Para qué propósito y fase del ciclo de vida fue creada?
2. ¿Qué parte de la realidad incluye y qué deja expresamente fuera?
3. ¿Qué diferencia entre objeto individual, tipo, clasificación y propiedad?
4. ¿Cómo representa sistemas, conjuntos, partes y contenedores espaciales?
5. ¿Qué relaciones reconoce y cuáles pueden tener información propia?
6. ¿Cómo separa identidad, posición, geometría y material?
7. ¿Cómo diferencia el elemento físico de su representación analítica?
8. ¿Cómo gestiona fuentes externas, revisiones, estados o procedencia?
9. ¿Cómo permite extender vocabulario y propiedades sin modificar su núcleo?
10. ¿Qué intercambia y cómo expresa los requisitos o límites de ese intercambio?
11. ¿Qué conceptos propone para nuestro inventario?
12. ¿Qué decisiones o complejidad no debemos trasladar automáticamente?

## 3. Mapa inicial del ecosistema

| Referencia | Propósito principal | Interés para este trabajo |
|---|---|---|
| IFC 4.3 | Modelo semántico abierto e intercambio del entorno construido | objetos, tipos, relaciones, sistemas, geometría, materiales y estructura espacial |
| IFC Structural Analysis | Modelo analítico dentro del ecosistema IFC | miembros, conexiones, acciones y vínculo con elementos físicos |
| SAF 2.2 | Intercambio práctico entre aplicaciones de análisis estructural | nodos, barras, superficies, cargas, combinaciones y metadatos de modelo |
| CFIHOS 2.0 | Entrega estructurada de información de instalaciones industriales | clases, equipos, TAG, propiedades, documentos y lifecycle de handover |
| DEXPI 2.0 | Intercambio de información de proceso y planta | estructura de planta, equipos, piping, instrumentación y topología funcional |
| bSDD | Diccionarios compartidos de clases y propiedades | términos, definiciones, propiedades y equivalencias entre vocabularios |
| Uniclass 2015 | Clasificación de construcción a distintas escalas | complejos, entidades, espacios, elementos, sistemas y productos |
| IDS 1.0 | Especificación verificable de requisitos de información IFC | qué objetos, propiedades, clasificaciones y materiales deben entregarse |
| ISO 19650 | Gestión de información mediante BIM | requisitos, responsabilidades, estados y entregas; no es un modelo de entidades |
| CADMATIC, Tekla y Revit | Implementaciones de producto | decisiones pragmáticas, extensiones y límites encontrados en uso real |

Versiones y estados deben comprobarse al realizar cada análisis; la tabla refleja la
documentación oficial consultada el 2026-09-08.

## 4. Frente 1 — IFC físico, espacial y semántico

**Estado:** EN CURSO  
**Informe activo:** [Fundamentos conceptuales de IFC](research/IFC_CORE_CONCEPTS.md)

### Objetivo

Comprender las separaciones estructurales del núcleo IFC antes de revisar su amplio
catálogo de clases.

### Temas prioritarios

- `IfcRoot`, identidad y procedencia básica;
- objeto, ocurrencia, tipo y propiedad;
- producto, elemento y elemento espacial;
- placement y representaciones geométricas;
- contención espacial, agregación, nesting, agrupación y sistemas;
- conectividad, puertos e interfaces;
- asociación de materiales simples, por capas, perfiles o constituyentes;
- clasificación y referencias externas;
- mecanismos para tipos definidos por usuario y property sets.

### Fuentes de partida

- [IFC 4.3.2 oficial](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/)
- [IFC Kernel](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/ifckernel/content.html)
- [IfcProduct](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcProduct.htm)
- [IfcBuiltSystem](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcBuiltSystem.htm)
- [Spatial Container](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/concepts/Object_Connectivity/Spatial_Structure/Spatial_Container/content.html)
- [IfcElementAssembly](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcElementAssembly.htm)
- [IfcPort](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcPort.htm)
- [Material Association](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/concepts/Object_Association/Material_Association/content.html)

### Resultado esperado

Una tabla de separaciones conceptuales de IFC, ejemplos civiles para cada una y una
lista acotada de conceptos candidatos. No se inventariarán centenares de clases IFC.

## 5. Frente 2 — Modelo estructural analítico

### Objetivo

Entender cómo se separan los elementos construidos de las idealizaciones utilizadas
para analizar su comportamiento.

### Temas prioritarios

- modelo físico frente a modelo analítico;
- correspondencias uno a uno, uno a varios y varios a uno;
- nodos, miembros de curva, superficies, sólidos y mallas;
- apoyos, conexiones, liberaciones, rigideces y excentricidades;
- acciones, grupos, casos, combinaciones y resultados;
- sistemas de coordenadas globales y locales;
- selección de una parte del modelo físico para un análisis;
- identidad y actualización entre aplicaciones.

### Fuentes de partida

- [IFC Structural Analysis Domain](https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/ifcstructuralanalysisdomain/content.html)
- [SAF Documentation 2.2](https://www.saf.guide/en/stable/)
- [Qué es SAF](https://www.saf.guide/en/stable/getting-started/what-is-saf.html)
- [Modelo físico y análisis en Tekla](https://support.tekla.com/dist/sxf/document/TS_ANA_2026_en_Analyze_models.pdf)
- documentación oficial de Revit y otros programas, seleccionada por problema
  concreto durante la investigación.

### Resultado esperado

Un mapa físico–analítico, una taxonomía inicial de acciones y agrupaciones de carga,
y diferencias relevantes con el modelo actual de Footings.

## 6. Frente 3 — Información de plantas industriales

### Objetivo

Evitar una visión exclusivamente edificatoria y estudiar estándares nacidos para
plantas de proceso y activos industriales.

### Temas prioritarios

- estructura o desglose de planta;
- TAG, elemento etiquetado, equipo y activo;
- clase de equipo, tipo, instancia y propiedades requeridas;
- topología e interfaces entre objetos;
- información funcional frente a representación gráfica o geométrica;
- procedencia y entrega entre contratista, suministrador y operador;
- información de diseño frente a activo instalado;
- relación entre datos, documentos y requisitos de handover.

### Fuentes de partida

- [CFIHOS 2.0](https://www.jip36-cfihos.org/cfihos-standards/)
- [DEXPI Specifications](https://dexpi.org/specifications/)
- [Introducción a DEXPI 2.0](https://dexpi.gitlab.io/-/Specification/-/jobs/11676485644/artifacts/src/.build/html/html/introduction.html)
- [Modelo de información DEXPI](https://dexpi.org/static/pid_specification_1.4/reference/index.html)
- ISO 15926, empezando por documentación pública y usos concretos en CFIHOS y DEXPI.

### Resultado esperado

Una comparación de los conceptos de planta, equipo, TAG, clase, activo e interfaz, y
una lista de aquellos que el dominio civil debe poseer o solamente referenciar.

## 7. Frente 4 — Clasificación y requisitos de información

### Objetivo

Distinguir el modelo de objetos del vocabulario utilizado para clasificarlos y de
los requisitos que determinan qué información debe entregarse.

### Temas prioritarios

- clase frente a entidad u ocurrencia;
- diccionario, definición y propiedad;
- clasificación multiaxial y equivalencias;
- escalas de complejo, entidad, espacio, elemento, sistema y producto;
- requisitos de información dependientes de fase y uso;
- validación automática de modelos;
- límite entre requisitos alfanuméricos y validación geométrica;
- utilidad posterior de ISO 19650 sin confundir gestión con dominio.

### Fuentes de partida

- [buildingSMART Data Dictionary](https://www.buildingsmart.org/users/services/buildingsmart-data-dictionary/)
- [Esquema de bSDD](https://standards.buildingsmart.org/DataDictionary/)
- [Uniclass 2015](https://uniclass.thenbs.com/)
- [Information Delivery Specification](https://www.buildingsmart.org/standards/bsi-standards/information-delivery-specification-ids/)
- [UK BIM Framework](https://ukbimframework.org/) como guía pública de ISO 19650.

### Resultado esperado

Una recomendación sobre qué debe vivir en el modelo conceptual, qué pertenece a una
clasificación o diccionario y qué debe expresarse como requisito de intercambio.

## 8. Plantilla de análisis de una referencia

```markdown
### Nombre y versión

**Organización responsable:**
**Fuente oficial:**
**Propósito declarado:**
**Fases y disciplinas cubiertas:**
**Fuera de alcance o limitaciones conocidas:**

**Conceptos principales:**

**Separaciones conceptuales relevantes:**

**Relaciones relevantes:**

**Identidad, tipos y clasificación:**

**Geometría, materiales y coordenadas:**

**Modelo físico y modelo analítico:**

**Extensión y personalización:**

**Intercambio, requisitos y validación:**

**Conceptos candidatos para nuestro inventario:**

**Lecciones aplicables:**

**Complejidad que no debemos copiar automáticamente:**

**Preguntas abiertas:**
```

No todos los apartados serán aplicables a todas las referencias. Una ausencia
relevante también debe registrarse.

## 9. Hallazgos iniciales que deben contrastarse

Los siguientes puntos son hipótesis de investigación, no decisiones del dominio:

1. IFC separa objetos, relaciones y definiciones de propiedades en su núcleo.
2. Ocurrencia y tipo son conceptos distintos; las propiedades pueden proceder del
   tipo y especializarse en la ocurrencia.
3. Contención espacial, descomposición, pertenencia a sistemas y conectividad no son
   relaciones equivalentes.
4. Un producto puede conservar identidad mientras dispone de placement y varias
   representaciones geométricas.
5. Los materiales compuestos requieren mecanismos diferentes según sean capas,
   perfiles o constituyentes.
6. Una interfaz puede tener semántica, posición y relaciones propias sin ser un
   elemento físico independiente.
7. El modelo físico y el analítico deben poder evolucionar y relacionarse sin
   correspondencia obligatoria uno a uno.
8. IFC no cubre por sí solo todas las necesidades de una planta industrial; CFIHOS,
   DEXPI e ISO 15926 aportan perspectivas complementarias.
9. Diccionario, clasificación, requisito de entrega y modelo de instancias son
   artefactos diferentes.
10. Footings puede aportar casos reales de relaciones físicas y transmisión de
    cargas, pero sus decisiones mantienen inicialmente alcance local.

## 10. Reparto inicial posible

| Frente | Encargo de investigación |
|---|---|
| 1 | IFC físico, espacial y semántico |
| 2 | IFC Structural Analysis, SAF y aplicaciones estructurales |
| 3 | CFIHOS, DEXPI e ISO 15926 |
| 4 | bSDD, Uniclass, IDS e introducción a ISO 19650 |

Cada frente utiliza la misma plantilla y debe presentar tanto lecciones útiles como
límites y dudas. El reparto facilita la primera pasada; no crea ownership permanente.

## 11. Criterio de salida de la primera investigación

La primera tarea se considera completa cuando:

1. los cuatro frentes tienen al menos una referencia principal analizada;
2. existe una comparación de los conceptos que usan con significados diferentes;
3. se han identificado separaciones conceptuales recurrentes;
4. hay una lista razonada de candidatos para el inventario;
5. se han señalado incompatibilidades o riesgos de adoptar modelos ajenos;
6. el equipo puede decidir qué partes del inventario deben revisarse primero.

No exige leer todos los esquemas ni cerrar el modelo propio.
