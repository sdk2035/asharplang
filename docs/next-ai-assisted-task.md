# ASHARP-RE-002 — Ingeniería inversa del parser y del AST

Estado: propuesta pendiente. Predecesor: [UML de alto nivel](uml/informe-arquitectura.md).
Entrada: archivo recuperado `mgnat20060606.zip`, SHA-256
`23572280e6d5e89bcf94f4512279d83bad5c5c3ea32306da76ca94948c77c01d`.

## Objetivo

Describir el subsistema formado por Par, Scn, Scans, Sinfo y Atree, vinculando
la sintaxis concreta Ada con rutinas de parsing y nodos de sintaxis abstracta.
El primer alcance será una unidad mínima con declaración de variable, expresión
aritmética y asignación. La cobertura completa del lenguaje será incremental.

## Trabajo asistido por IA

1. Inventariar especificaciones, cuerpos y subunidades `par-*.adb`, y registrar
   archivo y línea para cada unidad y operación pública.
2. Identificar tokens y operaciones léxicas de Scans/Scn y dependencias de Par.
3. Extraer clases de nodos, campos y accesores de Sinfo; describir almacenamiento
   e identificadores de Atree y constructores Nmake/Tbuild cuando intervengan.
4. Producir UML de paquetes y operaciones principales del subsistema.
5. Crear una matriz regla sintáctica → rutina del parser → constructor/nodo AST
   → referencia de código, empezando por el alcance mínimo.
6. Documentar restricciones estructurales del AST por separado de reglas de
   resolución de nombres y tipos, que se analizarán posteriormente en Sem.
7. Diseñar fixtures positivos y negativos con resultados esperados. Marcar como
   propuestos todos los resultados que no se hayan obtenido ejecutando el compilador.

## Entregables

- `docs/reverse-engineering/parser-ast.md`: explicación y límites de cobertura.
- Diagrama UML editable y vista SVG del subsistema.
- CSV de unidades, operaciones y dependencias con trazabilidad.
- Matriz de sintaxis y AST y fixtures mínimos.

## Aceptación

Cada relación del UML y cada fila de la matriz debe enlazar con evidencia
inspeccionada. Distinguir unidad Ada real de agrupación conceptual y asociación
de dependencia. Validar que los archivos y líneas citados corresponden al archivo
identificado. No inventar una gramática completa ni atribuir a Sinfo reglas
semánticas que residen en Sem. La aprobación del documento no demuestra un build.

## Orden posterior

Después: Sem/Expander, seguido de Jx/JVM/MSIL_Emit y runtime.
La importación completa de fuentes, revisión de licencias por componente y
bootstrap reproducible siguen pendientes como trabajo de recuperación.
