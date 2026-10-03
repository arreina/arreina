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
| [#328](https://github.com/boykopovar/AnyPS5/pull/328) fix(json2): reject documents nested deeper than 512 levels | Aceptado | Un JSON muy anidado tumbaba el proceso (desbordamiento de pila) |
| [#412](https://github.com/boykopovar/AnyPS5/pull/412) fix(shader): reject position exports without vertex input info | En revisión | Un shader de píxeles que exportaba una posición tumbaba el recompilador (puntero nulo) |
| [#352](https://github.com/boykopovar/AnyPS5/pull/352) fix(savedata): reject invalid directory names in sceSaveDataDelete | En revisión | Un `../` en el nombre de una partida borraba carpetas fuera de la de partidas |

Mi fork, [arreina/AnyPS5](https://github.com/arreina/AnyPS5), añade la integración continua de este trabajo: jobs con AddressSanitizer y UBSan, análisis estático (cppcheck, clang-tidy), validación de SPIR-V y fuzzers para el lector ELF, los decodificadores de instrucciones x86 y de GPU, el recompilador de shaders, la caché de shaders, JSON y los paquetes de comandos de GPU. Han encontrado 11 bugs; los que faltan están en cola para proponerse.

### [Coucou](https://github.com/Louis-CFM/coucou) · Tauri (Rust, TypeScript)

Aplicación de escritorio que muestra en la parte superior de la pantalla el estado de las sesiones de agentes de programación (Claude Code, Codex, Gemini CLI y otros). Mis contribuciones son a su versión para Linux.

| Pull request | Estado | Qué hace |
|---|---|---|
| [#104](https://github.com/Louis-CFM/coucou/pull/104) Linux (X11): keep the island unfocusable and on every workspace | Aceptado | La ventana ya no roba el foco del teclado y aparece en todos los escritorios |
| [#110](https://github.com/Louis-CFM/coucou/pull/110) Pause idle animations, and stop polling for a cursor Linux doesn't have | Aceptado | Menos consumo de CPU en reposo |
| [#111](https://github.com/Louis-CFM/coucou/pull/111) Linux: shrink the hidden island to its wake strip, and only take clicks there | Aceptado | La ventana oculta ya no bloquea los clics en las ventanas de debajo |
| [#105](https://github.com/Louis-CFM/coucou/pull/105) Add npm run fake-session to try the island without Claude Code | En revisión | Una sesión simulada para desarrollar y probar sin un agente |
| [#106](https://github.com/Louis-CFM/coucou/pull/106) Ignore clicks on a fresh approval card, and wire up Y / N | En revisión | Evita aprobar un permiso por accidente y añade atajos de teclado |

## Proyectos propios

### [Lince](https://github.com/arreina/lince) · C

Lenguaje de programación de propósito general con palabras clave en español, para que programar no exija saber inglés. Escrito en C puro, sin dependencias externas; se compila con `gcc` y `make` en Linux, macOS y Windows. La versión 0.5 tiene clases y tipos, y un compilador que genera ejecutables nativos. Web: [arreina.github.io/lince](https://arreina.github.io/lince).

```
clase Persona {
    funcion crear(val texto nombre, val numero edad): nulo {
        mi.nombre = nombre
        mi.edad   = edad
    }
    funcion saludar(): texto {
        devolver "Hola, soy " + mi.nombre + " y tengo " + mi.edad + " años"
    }
}

sea lista personas = [Persona("Ana", 22), Persona("Luis", 30)]
para cada elemento p en personas {
    escribir(p.saludar())
}
```

## Cómo se trabaja

- Cambios pequeños, de un solo tema, siguiendo las convenciones de cada proyecto
- Las correcciones incluyen un test de regresión cuando el proyecto tiene tests, comprobando que falla sin la corrección
- Solo datos de prueba sintéticos; nada de contenido propietario
- Nada se publica en otro proyecto sin mi revisión
