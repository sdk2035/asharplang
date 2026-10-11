# A# (A Sharp)

A# es un proyecto de adaptación de Ada a la plataforma .NET (CLI), asociado
históricamente con MGNAT. El archivo MGNAT histórico ha sido recuperado localmente y analizado para generar
un UML de alto nivel. Este repositorio publica la documentación de ingeniería
inversa; la importación completa de fuentes y el build reproducible siguen pendientes.

## Estado verificado

Inventario realizado el **2026-10-10**, sobre el commit
`111e1c8e85f1a3b44303d665eb961432e0df4c74`:

- `README.md`: presentación del proyecto.
- `mgnat/COMPLIANCE.txt`: informe histórico de compatibilidad Ada.
- No hay fuentes Ada/C/C#, solución `.sln`, proyectos `.csproj`, Makefiles,
  scripts de construcción ni pruebas.

El informe histórico declara limitaciones en representación de datos, conversiones
no comprobadas, almacenamiento y pruebas de concurrencia. Sus afirmaciones no
constituyen resultados reproducidos en este repositorio. No se ha validado
compatibilidad con .NET moderno, Mono, NuGet, AOT ni sistemas operativos actuales.

## Evaluación y construcción

- [Inventario de los materiales importados](docs/mgnat-inventory.md)
- [Plan de compilación reproducible y criterios de aceptación](docs/reproducible-build-plan.md)

No existe todavía un comando de compilación válido. Instalar el SDK de .NET no
reemplaza las fuentes y las herramientas históricas que faltan.

Para inspeccionar la documentación:

```sh
git clone https://github.com/sdk2035/asharplang.git
cd asharplang
git ls-tree -r HEAD
```

## Referencias de implementación

Consulta las [seis referencias y su papel en el compilador](docs/compiler-references.md):
GNAT LLVM, el archivo de fuentes SPARK GPL 2014, SPARK 2014, el sitio histórico de A#, GNU Ada en SourceForge y ada-lang.io.

## Avance de ingeniería inversa

[UML de paquetes principales y evidencia](docs/uml/informe-arquitectura.md), obtenido
por análisis estático de `mgnat20060606.zip`. Incluye PlantUML editable, SVG,
inventario y dependencias. La ruta de emisión observada usa `JVM.MSIL_Emit`.
No se ejecutaron el compilador ni las pruebas históricas.

## Próxima tarea asistida por IA

[ASHARP-RE-002 — Ingeniería inversa del parser y del AST](docs/next-ai-assisted-task.md):
detallar Par, Scn, Scans, Sinfo y Atree y trazar reglas → rutinas → nodos AST.

La [tarea de recuperación](docs/recovery-task.md) continúa parcialmente:
el archivo está disponible localmente; procedencia, licencias por componente,
importación y entorno de bootstrap todavía requieren validación.
