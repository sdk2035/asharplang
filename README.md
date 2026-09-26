# A# (A Sharp) 🚀

**A# (A Sharp)** es una adaptación e implementación de alto rendimiento del lenguaje de programación **Ada** para la plataforma **.NET (CLI)**, orientada al desarrollo de sistemas de alta integridad, tiempo real suave y aplicaciones críticas dentro de la infraestructura del Common Language Runtime.

Evolucionado a partir de las bases del compilador **JGNAT** (desarrollado por AdaCore) y optimizado mediante el framework **MGNAT**, A# traslada las rigurosas garantías de seguridad, el tipado estricto, la verificación de contratos y el modelo de concurrencia nativo de Ada (`tasking`) hacia el ecosistema ejecutable de .NET y Mono, permitiendo una interoperabilidad bidireccional de baja latencia con C# y la Base Class Library (BCL).

---

## 🌟 Características Principales

* **Semántica Ada Nativa sobre el CLR:** Soporte para la sintaxis y semántica del estándar Ada (incluyendo verificación de rangos, subtipos, bloques de manejo de excepciones y cláusulas de representación) compiladas directamente a CIL (Common Intermediate Language).
* **Sistemas de Alta Integridad en .NET:** Integración del modelo de concurrencia de Ada (`Tasking` y `Protected Objects`) mapeado eficientemente sobre los hilos del sistema operativo y las primitivas de sincronización administradas del CLR.
* **Interoperabilidad Transparente con C# y .NET:** Capacidad para instanciar clases de .NET (`System.*`), consumir paquetes NuGet y exportar paquetes Ada como ensamblados `.dll`/`.exe` totalmente consumibles desde C#, F# o VB.NET.
* **Compilación Nativa y Multiplataforma:** Compatibilidad completa con entornos Linux, macOS y Windows a través de Mono/.NET SDK, con soporte para compilación AOT (*Ahead-Of-Time*) para minimizar el tiempo de arranque.

---

## 🏗️ Arquitectura de la Plataforma

* **A# Front-End Compiler (asharp / gnat1):** Basado en la infraestructura de GCC/GNAT y JGNAT, analiza el código fuente Ada (`.ads` / `.adb`) y genera la representación de árbol semántico y la tabla de símbolos.
* **MGNAT Bytecode / CIL Generator:** Motor backend (basado en el trabajo del Dr. Martin C. Carlisle) encargado de traducir el árbol semántico de Ada e instrucciones abstractas a Common Intermediate Language (CIL) compatible con el estándar ECMA-335.
* **Ada-to-BCL Runtime Bridge (`asharp.dll`):** Librería de soporte en tiempo de ejecución que mapea las entradas/salidas nativas de Ada (`Ada.Text_IO`), los tipos numéricos de precisión fija/flotante y la gestión de memoria sobre la BCL de .NET.

---

## 🚦 Inicio Rápido

### Prerrequisitos

* **.NET SDK** (versión 6.0/8.0 o superior) o **Mono Runtime** (`mono-complete`).
* Entorno de compilación **A# / MGNAT** configurado en el sistema.

### Instalación

```bash
# Clonar el repositorio
git clone [https://github.com/tu-usuario/asharp.git](https://github.com/tu-usuario/asharp.git)
cd asharp

# Construir el compilador A# y las librerías del runtime
dotnet build ASharp.sln
