# Cuarta iteración — ocurrencia, representaciones y discrepancias

> **Status:** DRAFT
> **Editable:** sí mientras figure como documento activo en `WORKING_SET.md`
> **Document owner:** equipo de dominio civil
> **Canonical for:** —
> **Sources:** sesión de trabajo del equipo, aportada por Miguel el 24 de septiembre de 2026
> **Supersedes:** —
> **Last reviewed:** 2026-09-24

## Contexto

La fuente aportada no detalla contexto adicional. Se entiende como continuación
directa de las discusiones ya registradas en
[`iteration-02/ENUNCIADO.md`](../iteration-02/ENUNCIADO.md) (identidad de
ocurrencia, tipo/estado, sesión de conjuntos y versiones del 23 de septiembre)
y en [`iteration-03/NOTAS_REVISION_VS_RECALCULO.md`](../iteration-03/NOTAS_REVISION_VS_RECALCULO.md)
(cuándo cambia un estado frente a cuándo exige recálculo). Todo el contenido de
este documento es aportación `DRAFT` para contraste, no aprobación del equipo.

## Resultado de la última sesión

### 1. Ocurrencia de Diseño

Se mantiene como concepto central y aporta identidad a un elemento del
proyecto. Debe existir independientemente de sus representaciones en
aplicaciones concretas.

### 2. Representaciones

Una Ocurrencia de Diseño puede aparecer en varios modelos. Cada representación
puede tener diferente geometría, nivel de detalle, propósito, versión y estado
de validación.

Un modelo analítico es una abstracción. Puede haber más de uno para una misma
estructura y no tiene que contener todos los elementos presentes en maqueta o
fabricación.

### 3. Estado de Diseño

Se está reformulando. La hipótesis actual es que constituye una visión
agregada o derivada de las versiones relevantes de las representaciones
asociadas a una Ocurrencia de Diseño.

No se ha decidido si debe persistirse, calcularse dinámicamente o
materializarse como snapshot validado.

### 4. Versionado e histórico

Se necesita conservar snapshots y versiones de los modelos, así como la
trazabilidad de las decisiones. Los modelos analíticos deberán ponerse a
disposición del entorno común si se quieren comparar con las demás
representaciones.

### 5. Discrepancias

La sincronización no será completamente automática. Debe existir validación
humana. El sistema debe detectar una discrepancia, presentarla al
responsable, permitir aceptar, rechazar, ignorar justificadamente o posponer,
y conservar la decisión.

Una decisión anterior debe evitar notificaciones repetidas mientras no exista
un nuevo cambio relevante.

La Discrepancia es candidata a entidad de dominio.

### 6. Entorno común

Se propone conceptualmente una interfaz CDM independiente de STAAD y SP3D
donde se visualicen y comparen representaciones, se tomen decisiones y se
conserve trazabilidad.

No debería impedir la libertad del calculista ni obligar a que todos los
modelos tengan el mismo nivel de detalle.

### 7. Elementos secundarios

Barandillas, gratings, ladders y zancas pueden pertenecer al dominio aunque no
tengan cálculo propio o no aparezcan en el modelo analítico principal.

Aportan valor para cargas, coordinación, interferencias, mediciones,
fabricación, estándares, gálibos y zonas de paso.

### 8. Transferencia entre disciplinas

La geometría o necesidad de un soporte puede originarse en tuberías. Debe
poder llegar tanto al calculista como al diseñador civil. El calculista decide
si la incorpora al modelo analítico, pero la información necesaria para
diseño no debe perderse.

### 9. Distintos significados de "tipo"

Se deben separar:

- Clase o naturaleza: viga, columna, zapata, perno.
- Variante geométrica: rectangular, octogonal, forma libre.
- Tipo de catálogo o plantilla: conjunto reutilizable de parámetros.
- Agrupación documental: agrupación de diseños equivalentes para planos y
  memorias.
- Diseño estándar frente a diseño especial o personalizado.

### 10. Catálogos

No está decidido si viven a nivel corporativo, de proyecto, estructura o
entregable. Probablemente se necesiten varios ámbitos.

También debe diferenciarse entre:

- Tipo como referencia viva, donde cambiar el tipo afecta a las ocurrencias.
- Tipo como plantilla, donde se copian valores iniciales y la ocurrencia
  puede evolucionar independientemente.

### 11. Geometría y función

La identidad del elemento debe desacoplarse de su geometría. También debe
distinguirse entre geometría, orientación, rol estructural y comportamiento
analítico.

Por ejemplo, viga y columna no deberían quedar determinadas rígidamente por
orientación.

## Decisiones o consensos

- Ocurrencia de Diseño aporta la identidad principal.
- Los modelos son representaciones parciales.
- Las representaciones evolucionan independientemente.
- Se requiere validación humana.
- Las decisiones y discrepancias deben conservarse.
- Hay que mantener histórico.
- El calculista debe conservar libertad de modelado.
- La información debe poder llegar a diseño aunque no pase por el modelo
  analítico.
- Deben separarse los diferentes significados de "tipo".
- Debe mantenerse trazabilidad cuando un diseño parte de un catálogo y
  después se personaliza.
- La geometría debe estar desacoplada de la identidad del elemento.

## Preguntas abiertas

- Definición formal de Ocurrencia, Representación y Estado de Diseño.
- Persistencia o cálculo del Estado de Diseño.
- Ciclo de vida de Discrepancia.
- Source of truth por atributo.
- Nivel de los catálogos.
- Gestión de cambios en tipos compartidos.
- Criterios de equivalencia para agrupación documental.
- Identidad entre aplicaciones.
- Reglas de propagación.
- Tratamiento de elementos ausentes en una representación.
- Separación entre clase, forma, sección y rol estructural.
- Estrategia de geometría extensible.
- Correspondencia con IFC.

## Encargo para el agente

Se pidió analizar este resultado dentro del contexto general del proyecto y
proponer próximos pasos priorizados, deberes para la siguiente sesión,
decisiones a cerrar antes de implementar, conceptos que necesitan ejemplos o
contraejemplos, artefactos a preparar, una agenda propuesta, entidades/value
objects/agregados/eventos candidatos, bounded contexts candidatos, riesgos o
contradicciones con decisiones anteriores, simplificaciones posibles para un
primer prototipo, correspondencias preliminares con IFC y preguntas críticas
todavía no planteadas — diferenciando explícitamente acuerdos, hipótesis,
alternativas, recomendaciones y decisiones pendientes.

La respuesta completa a este encargo vive en
[`ANALISIS_AGENTE.md`](ANALISIS_AGENTE.md), como documento derivado separado de
esta evidencia de sesión.
