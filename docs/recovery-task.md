# Siguiente tarea propuesta asistida por IA

## ASHARP-RECOVERY-001 — Recuperar MGNAT y fijar el bootstrap histórico

Estado: propuesta pendiente. Fecha: 2026-10-10.
Prioridad: siguiente paso del [plan de compilación](reproducible-build-plan.md).
Este documento especifica trabajo futuro; no afirma que los archivos hayan
sido recuperados ni que el compilador se haya construido.

## Objetivo

Recuperar una distribución identificada de A#/MGNAT desde el sitio histórico,
inventariar sus fuentes y seleccionar un entorno de bootstrap coherente con
su receta original. Dejar una importación trazable y una receta revisable para
la primera construcción Ada → CIL.

## Entradas

Las [seis referencias](compiler-references.md) cumplen papeles distintos:
A# guía la recuperación; GNU Ada y el archivo GNAT/SPARK aportan candidatos
históricos; ada-lang.io orienta un entorno Ada actual de comparación;
GNAT LLVM y SPARK aportan referencias posteriores de backend y verificación.

## Trabajo propuesto

1. Seguir los enlaces del sitio A# y localizar una versión concreta de
   `mgnat.zip`; registrar disponibilidad de `msil2ada.zip` por separado.
2. Descargar los materiales disponibles, calcular SHA-256 y registrar URL,
   fecha, versión declarada, tamaño y licencia por componente.
3. Extraer e inventariar frontend, backend CIL, runtime, Makefiles, ejemplos y
   dependencias. Comparar `COMPLIANCE.txt` con la copia existente.
4. Revisar Makefile/jMakefile y documentar GNAT para Windows, shell, herramientas
   .NET/ILASM, rutas y orden de construcción exigidos por esa versión.
5. Seleccionar candidatos de bootstrap desde las referencias históricas.
   Fijar versiones y justificar compatibilidad; registrar dudas sin convertirlas
   en requisitos confirmados. Mantener aparte el entorno Ada moderno.
6. Importar las fuentes redistribuibles con avisos de licencia y preparar una
   receta de VM o entorno y comandos derivados de los Makefiles recuperados.
7. Informar si se puede iniciar la primera construcción y enumerar los bloqueos
   restantes. La ejecución completa y los fixtures pertenecen al siguiente hito
   si requieren herramientas aún no disponibles.

## Entregables previstos

- `docs/recovery-report.md`: procedencia, comparación, decisiones y bloqueos.
- `manifests/mgnat-sources.json`: archivos, versiones, tamaños, SHA-256 y licencias.
- `docs/bootstrap-environment.md`: herramientas fijadas y receta revisable.
- Fuentes importadas preservando su estructura y avisos, cuando se establezcan
  sus condiciones de redistribución.

## Criterios de aceptación

- Al menos una distribución MGNAT recuperada e identificada por SHA-256,
  con fuentes y avisos inspeccionados.
- Inventario que distingue fuentes, binarios, dependencias y elementos ausentes.
- Requisitos confirmados vinculados a archivos o instrucciones de esa versión.
- Manifiesto sin versiones ni checksums inventados.
- Receta que identifica plataforma y comandos reales, con bloqueos explícitos.
- Revisión humana de procedencia, licencias y cambios antes de aceptar el hito.

Si los archivos no están disponibles, entregar un informe de búsquedas y enlaces
fallidos. Ese resultado documenta el bloqueo, pero no completa la recuperación.

## Asistencia de IA

La IA puede localizar candidatos, comparar archivos, extraer dependencias y
redactar manifiestos y recetas. Las conclusiones deben sustentarse en materiales
inspeccionados. No asumir que GNAT moderno o LLVM reemplazan el bootstrap MGNAT
ni que verificación SPARK acredita la ejecución CLI.
