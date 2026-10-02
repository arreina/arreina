# Alberto Ruiz

[English](README.md)

Desarrollo software dirigiendo agentes de IA de programación ([Claude Code](https://claude.com/claude-code)). Yo decido en qué trabajar, fijo las restricciones, elijo qué se propone a otros proyectos y llevo la conversación con sus mantenedores. El agente escribe y prueba el código. Todos los pull requests de abajo lo indican en su descripción.

## Contribuciones open source

### [AnyPS5](https://github.com/boykopovar/AnyPS5) · C++20, CMake

Herramienta que porta ejecutables de PS5 a Linux y Windows. Mis contribuciones son correcciones de robustez encontradas con fuzzing y sanitizers. Cada una incluye un test de regresión.

| Pull request | Estado | Qué corrige |
|---|---|---|
| [#183](https://github.com/boykopovar/AnyPS5/pull/183) fix(relinker): require a full ELF64 header before reading it | Aceptado | Los ficheros truncados se leían más allá de su final |
| [#193](https://github.com/boykopovar/AnyPS5/pull/193) fix(relinker): keep ELF bounds checks from overflowing | Aceptado | Offsets manipulados desbordaban la comprobación de límites (heap overflow) |
| [#213](https://github.com/boykopovar/AnyPS5/pull/213) fix(shader): skip the push constant copy when there is nothing to copy | Aceptado | Comportamiento indefinido detectado por UBSan en la caché de shaders |
| [#280](https://github.com/boykopovar/AnyPS5/pull/280) fix(shader): reject SDWA and DPP instructions without their modifier word | Aceptado | Instrucciones de GPU truncadas se leían fuera de límites |
| [#328](https://github.com/boykopovar/AnyPS5/pull/328) fix(json2): reject documents nested deeper than 512 levels | En revisión | Un JSON muy anidado tumbaba el proceso (desbordamiento de pila) |
| [#352](https://github.com/boykopovar/AnyPS5/pull/352) fix(savedata): reject invalid directory names in sceSaveDataDelete | En revisión | Un `../` en el nombre de una partida borraba carpetas fuera de la de partidas |

Mi fork, [arreina/AnyPS5](https://github.com/arreina/AnyPS5), añade la integración continua de este trabajo: jobs con AddressSanitizer y UBSan, análisis estático (cppcheck, clang-tidy), validación de SPIR-V y fuzzers para el lector ELF, los decodificadores de instrucciones x86 y de GPU, el recompilador de shaders, la caché de shaders, JSON y los paquetes de comandos de GPU. Han encontrado 11 bugs; los que faltan están en cola para proponerse.

## Proyectos propios

| Proyecto | Descripción |
|---|---|
| [lince](https://github.com/arreina/lince) · C | Lenguaje de programación de propósito general en español |
| [bot-reels-videojuegos](https://github.com/arreina/bot-reels-videojuegos) · Python | Convierte noticias de videojuegos en vídeos verticales: guion, voz sintética, imágenes libres de derechos y control desde el móvil |

## Cómo se trabaja

- Cambios pequeños, de un solo tema, siguiendo las convenciones de cada proyecto
- Un test de regresión por cada corrección, comprobando que falla sin ella
- Solo datos de prueba sintéticos; nada de contenido propietario
- Nada se publica en otro proyecto sin mi revisión
