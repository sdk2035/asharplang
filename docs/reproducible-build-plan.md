# Plan de compilación reproducible

Estado: plan propuesto, no ejecutado. Fecha: 2026-10-10.

## Objetivo y frontera

Construir desde fuentes una distribución identificada de A#/MGNAT y ejecutar
un programa Ada mínimo como ensamblado CLI. No se presume soporte de .NET 6/8,
Mono actual, NuGet, AOT o todas las características Ada.

La base inventariada carece de fuentes y receta de construcción. No se inventan
versiones de GCC/GNAT, comandos de bootstrap ni imágenes de contenedor.
La primera ejecución queda condicionada a recuperar esos materiales.

## 1. Recuperación y procedencia

1. Localizar una distribución original y sus instrucciones de instalación.
2. Registrar URL de origen, fecha de descarga, versión o revisión, tamaño y
   SHA-256 del archivo; conservar un manifiesto de cada componente importado.
3. Revisar licencia y avisos de copyright de compilador, runtime, parches y
   herramientas. Si no se puede establecer permiso de redistribución, detener
   la importación de ese componente y registrar la brecha.
4. Comparar el informe de compatibilidad incluido con el archivo original;
   registrar diferencias sin atribuirle una versión por conjetura.

Entregable: fuentes trazables y manifiesto de procedencia/licencias. No ejecutar
scripts descargados hasta revisar su contenido y dependencias.

## 2. Reconstrucción del entorno

Extraer de la receta original el sistema operativo y arquitectura, compiladores
de bootstrap, versiones GCC/GNAT, ensamblador CIL, bibliotecas de soporte y runtime
CLI. Distinguir dependencias de construcción de las de ejecución.

Fijar cada versión y checksum en un manifiesto. Registrar locale, zona horaria,
variables necesarias y orden de construcción. Usar una VM aislada si el entorno
histórico no funciona en un contenedor moderno. Separar un perfil histórico
reproducible de cualquier experimento de actualización.

Entregables previstos (a crear al conocer la receta): manifiesto de herramientas,
definición de VM/contenedor, script de bootstrap y script de construcción.
Cada descarga debe estar fijada y verificarse; la construcción posterior debe
poder realizarse sin red con las dependencias previamente preparadas.

## 3. Primera construcción

1. Partir de un checkout limpio fijado por commit y del entorno identificado.
2. Construir compilador, backend y runtime en el orden establecido por la receta.
3. Guardar comandos exactos, códigos de salida, versiones y log completo.
4. Registrar rutas y SHA-256 de binarios y ensamblados producidos.
5. Repetir desde cero en un segundo entorno limpio.

Aceptar reproducibilidad funcional si ambas ejecuciones construyen y producen
los mismos resultados de pruebas. Evaluar por separado identidad binaria de los
artefactos; si difieren por timestamps u otros metadatos, documentar la causa.
No declarar reproducibilidad bit a bit sin comparación de hashes satisfactoria.

## 4. Fixture mínimo y validación

Fixture propuesto, pendiente de compilación con la distribución recuperada:

```ada
with Ada.Text_IO;
procedure Hello is
begin
   Ada.Text_IO.Put_Line ("Hello, A#");
end Hello;
```

| Caso | Resultado exigido |
| --- | --- |
| Compilar Hello | Código de salida 0 y ensamblado CLI identificable |
| Ejecutar Hello | Salida estándar: una línea `Hello, A#`; salida 0 |
| Fuente con identificador no declarado | Diagnóstico y salida distinta de 0; sin artefacto ejecutable nuevo |
| Asignación fuera de un subtipo de rango | Fixture diseñado para evaluación en ejecución; `Constraint_Error` capturada y marcador esperado |
| Dos construcciones limpias | Mismos resultados funcionales; hashes comparados y diferencias explicadas |

Capturar stdout y stderr por separado; normalizar solo CRLF/LF para comparar
la línea del fixture. Registrar el runner CLI exacto y su versión.
Las comprobaciones de rango, excepciones y concurrencia requieren fixtures
propios; Hello no demuestra compatibilidad Ada completa.

## 5. Evidencia de aceptación y siguiente hito

Publicar un informe con commit fuente, manifiesto, entorno, comandos, logs,
checksums y resultados de cada caso. Añadir CI únicamente cuando la receta
funcione de manera local y pueda obtener sus dependencias de forma verificable.

La tarea actual entrega inventario y plan. La siguiente tarea es recuperar e
importar las fuentes originales con procedencia, licencias y dependencias fijadas.
El proyecto seguirá con **build sin verificar** hasta completar las fases 1–4.
