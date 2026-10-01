# Sistema de ingeniería

> **Status:** DRAFT
> **Editable:** sí; definición conceptual candidata para contraste del equipo
> **Document owner:** equipo de dominio civil
> **Canonical for:** —
> **Sources:** [informe de consolidación y preparación de la quinta iteración](../iteration-05/ENUNCIADO.md), [notas de Ángel sobre varios modelos](../iteration-04/ANGEL_ITERATION_04.md#8-varios-modelos-simultáneamente-válidos-y-conciliación-por-alcance) y [ocurrencia de diseño](DESIGN_OCCURRENCE.md)
> **Supersedes:** —
> **Last reviewed:** 2026-10-01

## Por qué aparece ahora

Las iteraciones anteriores permiten identificar una ocurrencia a través de varias
fuentes y reconocer varios modelos simultáneamente válidos, pero no responden por
sí solas qué modelos y ocurrencias forman un ámbito coherente de trabajo ni qué
políticas deben aplicarse al conciliarlos. La hipótesis `SistemaDeIngeniería`
aparece para cubrir esa responsabilidad.

No reemplaza a `OcurrenciaDeDiseño`. Desplaza la pregunta desde «¿qué guarda la
ocurrencia?» hacia «¿en qué contexto de ingeniería aparecen esa ocurrencia, sus
representaciones y los modelos que la tratan?».

## Definición candidata

Un **sistema de ingeniería** es un contexto de negocio identificable en el proyecto,
con propósito y frontera explícitos, que permite relacionar un conjunto coherente
de ocurrencias de diseño, modelos de ingeniería y políticas de conciliación.

Ejemplos propuestos por el informe son un pipe rack concreto, un sistema de
cimentación, un pipe bridge, un edificio, la cimentación de un equipo o un sistema
de soportes de tubería. Son candidatos que deben probarse individualmente: la lista
mezcla expresiones que también podrían designar un conjunto físico, un sistema
funcional, un contenedor espacial o un tipo.

## Responsabilidades candidatas

| Responsabilidad | Sí corresponde al candidato | No se deduce todavía |
|---|---|---|
| Identidad y propósito | Permitir hablar de este ámbito de ingeniería a través de cambios. | Que su nombre o TAG baste para identificarlo. |
| Frontera | Declarar qué se considera dentro, fuera o compartido para un propósito. | Que exista una frontera única para todas las disciplinas y fases. |
| Relación con modelos | Asociar modelos con rol, propósito, cobertura y vigencia. | Que el sistema posea en exclusiva el lifecycle del modelo. |
| Relación con ocurrencias | Contextualizar qué ocurrencias participan y con qué papel. | Que la membresía equivalga a composición física o contención espacial. |
| Conciliación | Proporcionar un ámbito candidato para seleccionar modelos, revisiones y políticas. | Que toda conciliación deba quedar encerrada en un único sistema. |
| Navegación | Permitir consultar por sistema, modelo u ocurrencia sin duplicar identidades. | Que sea una jerarquía rígida `Project → System → Object`. |

El sistema no almacena copias de geometría, material, sección, cargas o resultados.
Esos datos siguen perteneciendo a estados, modelos, representaciones, relaciones o
evidencias concretas. Una vista resuelta puede reunirlos para una consulta, pero no
crea por sí sola otra fuente de verdad.

## Fronteras con conceptos existentes

- **Conjunto físico:** responde qué partes constituyen un todo físico. Un pipe rack
  concreto puede ser a la vez conjunto físico y contexto de ingeniería, pero ambas
  identidades no se unifican por defecto.
- **Sistema funcional:** responde qué objetos colaboran para una función y admite
  membresía muchos-a-muchos. `SistemaDeIngeniería` añade el contexto de modelos,
  cobertura y conciliación; falta demostrar si esta diferencia justifica una entidad
  distinta o solo un rol especializado.
- **Contexto espacial:** responde dónde se considera contenido un objeto. No decide
  por sí solo qué modelos o políticas participan.
- **Modelo de ingeniería:** es un artefacto con identidad, propósito y revisiones
  propios. Se asocia al sistema; no es el sistema.
- **Ocurrencia de diseño:** mantiene la continuidad de un individuo físico. Puede
  participar en uno o varios sistemas sin copiarse.
- **Proyecto:** constituye un contexto más amplio. No se ha demostrado que todo
  objeto del proyecto deba descender de un sistema de ingeniería.

## Relaciones mínimas que deben probarse

```text
SistemaDeIngeniería
├── contextualiza → OcurrenciasDeDiseño
├── tiene asociado → ModelosDeIngeniería
└── delimita → CasosDeConciliación

Representación
├── representa → OcurrenciaDeDiseño
└── aparece en → ModeloDeIngeniería / revisión concreta
```

«Contextualiza» y «tiene asociado» son deliberadamente más débiles que «contiene».
Hasta contrastar casos compartidos, las cardinalidades no se fijan como uno-a-muchos.

## Criterios candidatos de identidad y límite

Para reconocer un sistema no basta una agrupación arbitraria. Debe poder responderse:

1. qué propósito de ingeniería permite tratarlo como unidad;
2. qué continuidad conserva cuando cambian ocurrencias o modelos;
3. qué criterio decide inclusión, exclusión o pertenencia compartida;
4. qué modelos lo representan o analizan, con qué cobertura y revisión;
5. qué decisiones o conciliaciones necesitan referirse al sistema completo.

Si solo existe una selección temporal de objetos para una consulta, probablemente
no hace falta identidad de sistema. Si el candidato solo enumera partes físicas,
puede bastar la composición de una ocurrencia compuesta.

## Casos que pueden refutar la hipótesis

- un modelo global que cubre varios sistemas de ingeniería;
- una cimentación compartida por dos módulos o sistemas;
- una ocurrencia que participa en el sistema resistente y en otro sistema funcional;
- un modelo previo a la definición formal de su sistema;
- una ocurrencia creada antes de asignarle un contexto;
- una conciliación transversal entre dos sistemas;
- dos candidatos con el mismo nombre de negocio pero fronteras distintas por fase.

Si estos casos solo pueden resolverse duplicando modelos u ocurrencias, la frontera
es incorrecta. Si `SistemaDeIngeniería` no aporta decisiones, consultas o lifecycle
propios frente al conjunto físico y al sistema funcional, el concepto sobra.

## Decisiones abiertas

1. Si es una entidad de dominio autónoma, un rol de `SistemaFuncional` o un contexto
   de coordinación.
2. Si toda ocurrencia y todo modelo deben asociarse a uno, o si la asociación puede
   ser posterior, opcional o múltiple.
3. Cómo se expresa la cobertura parcial de un modelo y los límites compartidos.
4. Qué hace persistir la identidad del sistema al cambiar nombre, composición,
   propósito, fase o disciplina responsable.
5. Si el sistema es el ámbito habitual de conciliación y qué excepciones legítimas
   existen.
6. Si «agregado raíz» aporta algo antes de tomar decisiones de consistencia y
   transacción. Por ahora no se adopta ese término como definición conceptual.
