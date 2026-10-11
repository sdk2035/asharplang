# Referencias de implementación del compilador

Referencias incorporadas el 2026-10-10. Son puntos de partida para recuperar
A#/MGNAT y estudiar su evolución; no son dependencias incorporadas ni builds
validados de este repositorio.

| Referencia | Papel en ASharpLang | Límite de la evidencia |
| --- | --- | --- |
| [GNAT LLVM](https://github.com/sdk2035/gnat-llvm) | Estudiar la conexión del frontend GNAT con un generador LLVM y su organización de construcción | Produce objetos nativos y bitcode LLVM; adaptar ese diseño a CIL requiere trabajo específico |
| [Índice de fuentes SPARK GPL 2014 para Windows x86](https://github.com/sdk2035/gnat-community-archives/blob/master/sources/spark-gpl-2014-x86-windows-bin.exe-sources.md) | Localizar materiales históricos de GNAT/GCC y herramientas asociadas | El índice no identifica una distribución MGNAT; disponibilidad, hashes y compatibilidad deben verificarse |
| [SPARK 2014](https://github.com/robotics-intelligent-systems/spark2014) | Referencia para análisis, verificación y selección de versiones compatibles del frontend | Su integración con A# y con el runtime CLI queda por diseñar y validar |
| [Sitio histórico de A#](https://asharp.martincarlisle.com/) | Fuente primaria para localizar MGNAT, MSIL2Ada y reconstruir el entorno original | Instrucciones históricas, todavía no reproducidas aquí |

| [GNU Ada en SourceForge](https://sourceforge.net/projects/gnuada/) | Investigar distribuciones y materiales históricos de herramientas GNAT | Su oferta actual se centra en GNAT Studio para macOS; no acredita una distribución A#/MGNAT |
| [Ada community: ada-lang.io](https://ada-lang.io/) | Orientar la selección de herramientas Ada actuales, Alire y recursos del lenguaje | La disponibilidad de herramientas actuales no demuestra compatibilidad con el bootstrap histórico de MGNAT |

## A#/MGNAT: recuperación prioritaria

El [sitio de A#](https://asharp.martincarlisle.com/) señala SourceForge como
distribuidor de `mgnat.zip`, que incluye compilador fuente y ejecutable,
y de `msil2ada.zip`. Describe una reconstrucción mediante Makefiles en
`src` y `src/lib`, GNAT para Windows y un shell Unix como Cygwin.
El runtime incluye `mgnat.dll` y `mgnatcs.dll`; este último requiere
Visual Studio .NET según las instrucciones históricas. También advierte que
hay rutas locales que ajustar en Makefile y jMakefile.

La página menciona .NET Framework 2.0.50727 e ILASM en el entorno histórico,
y distribución bajo GPL. Recuperar el archivo exacto, inspeccionar sus avisos
y verificar dependencias sigue siendo necesario antes de fijar una receta.
Estas pistas actualizan el plan; no demuestran una construcción actual.

## GNAT LLVM: arquitectura de backend

El [README de GNAT LLVM](https://github.com/sdk2035/gnat-llvm/blob/master/README.md)
explica la conexión entre frontend GNAT y generación LLVM. La receta consultada
utiliza fuentes GNAT, bindings Ada para LLVM, GNAT de bootstrap, LLVM/Clang y
Make; declara GPL versión 3 o posterior.

Uso propuesto: comparar la interfaz del frontend, la traducción de tipos y la
organización del backend con MGNAT una vez recuperado. LLVM bitcode y CIL son
destinos diferentes: no se presupone un conversor LLVM → CIL ni compatibilidad
directa con .NET. Para experimentar, fijar commit y versiones de herramientas
de la receta correspondiente, evitando mezclar un frontend histórico con
dependencias modernas sin pruebas.

## Archivo SPARK GPL 2014: materiales históricos

El [índice suministrado](https://github.com/sdk2035/gnat-community-archives/blob/master/sources/spark-gpl-2014-x86-windows-bin.exe-sources.md)
enlaza fuentes de GNAT/GCC 4.7, SPARK, gnat_util, GPRbuild, AUnit, XML/Ada,
ASIS, Why3, Alt-Ergo y otras herramientas.

Uso propuesto: investigar versiones históricas y preparar un inventario de
archivos candidatos. El nombre del instalador no implica que todas sus entradas
sean fuentes, ni que GNAT 4.7 pueda construir MGNAT. No se descargaron ni
ejecutaron esos archivos; sus identificadores URL no se aceptan como SHA-256
verificados.

## SPARK 2014: análisis y verificación

El [README de SPARK](https://github.com/robotics-intelligent-systems/spark2014/blob/master/README.md)
vincula las fuentes SPARK a una versión compatible del frontend GNAT y describe
ramas y submódulos para construir con las herramientas correspondientes.

Uso propuesto: diseñar fixtures de análisis y contratos para un subconjunto Ada
compatible. Registrar por separado resultados de prueba formal, compilación a
CIL y ejecución: demostrar una propiedad del código Ada no demuestra por sí solo
que el backend o runtime .NET preserve esa propiedad.

## Secuencia de evaluación

1. Recuperar MGNAT desde la referencia primaria y registrar procedencia,
   licencia, checksum y receta.
2. Contrastar sus requisitos con los materiales del archivo GNAT/SPARK.
3. Estudiar GNAT LLVM como referencia de arquitectura para una posible evolución.
4. Evaluar SPARK sobre un subconjunto definido con frontend compatible.
5. Publicar evidencia de cada experimento antes de declarar integración o soporte.

## GNU Ada y comunidad Ada

[GNU Ada en SourceForge](https://sourceforge.net/projects/gnuada/) conserva
publicaciones históricas y actualmente describe paquetes GNAT Studio para macOS.
Su propia descripción remite a ada-lang.io y Alire para compiladores y paquetes.
Uso propuesto: buscar candidatos de bootstrap con versión y plataforma
identificadas; comprobar cada archivo antes de incorporarlo al manifiesto.

[Ada-lang.io](https://ada-lang.io/) presenta recursos del lenguaje y acceso al
ecosistema mediante Alire. Uso propuesto: preparar un entorno Ada actual de
referencia para fixtures, separado del entorno histórico de A#.
La comparación semántica debe limitarse al subconjunto Ada admitido por ambos.
