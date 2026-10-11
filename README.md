# A# (A Sharp)

A# es un proyecto de adaptación de Ada a la plataforma .NET (CLI), asociado
históricamente con MGNAT. Este repositorio conserva actualmente documentación;
**no contiene un compilador ni un runtime construibles**.

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

## Próxima tarea asistida por IA

[ASHARP-RECOVERY-001: recuperar MGNAT y fijar el bootstrap histórico](docs/next-ai-assisted-task.md).

Recuperar una distribución original, verificar fuentes y licencias, calcular
checksums y preparar un manifiesto y una receta de entorno con herramientas
fijadas. La propuesta incluye entregables y criterios de aceptación.
La construcción y ejecución Ada → CIL siguen pendientes.
