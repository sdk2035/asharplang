# Inventario de MGNAT/A#

Fecha: 2026-10-10. Base inspeccionada: commit
`111e1c8e85f1a3b44303d665eb961432e0df4c74` de `sdk2035/asharplang`.
Método: árbol Git recursivo completo (sin truncamiento) y lectura de ambos blobs.
El inventario describe esa base, anterior a la incorporación de estos documentos.

## Material presente

| Ruta | Tamaño (bytes) | Blob Git | Clasificación |
| --- | ---: | --- | --- |
| README.md | 2992 | ab41e121a092e0d8d116df75d4c6d82954690a86 | Presentación; terminaba en un bloque de instalación incompleto |
| mgnat/COMPLIANCE.txt | 1699 | 8a9b1810a18e7b300dd72d382f17d58ac38a4675 | Informe histórico de compatibilidad; no es código fuente |

La carpeta `mgnat/` contiene un único archivo. No se encontraron fuentes
`.ads`, `.adb`, `.c`, `.h` o `.cs`; tampoco proyectos .NET, Makefiles,
scripts, binarios, ejemplos, pruebas, CI ni un archivo de licencia.
Esto es un inventario del repositorio, no de una distribución externa de MGNAT.

## Evidencia y límites

`COMPLIANCE.txt` afirma compatibilidad para numerosas secciones del manual Ada,
pero no identifica versión del compilador, edición del manual, fecha, plataforma
ni comandos de prueba. Por ello sus afirmaciones se conservan como antecedentes
y no como certificación actual.

Limitaciones que declara el propio informe:

- Atributos de enumeración para tipos importados de .NET: no soportados.
- Tareas y sincronización: implementadas, sin pruebas extensivas.
- Secciones 13.1, 13.2, 13.3, 13.5, 13.6 y 13.8: no implementadas.
- Conversiones no comprobadas: implementación parcial; un cast incompatible
  puede generar una excepción.
- Gestión de almacenamiento y restricciones: no probadas.
- Streams: implementados con pruebas limitadas.

El README anterior proponía `dotnet build ASharp.sln`, pero ese archivo no existe.
Sus afirmaciones sobre NuGet, AOT y compatibilidad multiplataforma carecen de
artefactos de validación en la base inspeccionada.

## Brechas para construir

| Componente | Evidencia actual | Acción requerida |
| --- | --- | --- |
| Frontend Ada y backend CIL | Ausentes | Recuperar distribución original y determinar qué fuentes requiere |
| Runtime y puente .NET | Ausentes | Identificar fuentes, ensamblados y contratos de integración |
| Herramientas de bootstrap | No especificadas | Derivar versiones y dependencias de las instrucciones originales |
| Licencias y procedencia | No documentadas | Verificar condiciones por componente antes de importar |
| Fixtures y resultados | Ausentes | Añadir un programa mínimo y pruebas positivas y negativas |

Resultado: **evaluación documental completada; construcción bloqueada por
ausencia de fuentes y receta original**. El [plan](reproducible-build-plan.md)
define cómo pasar de este inventario a evidencia ejecutable.
