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
| [#412](https://github.com/boykopovar/AnyPS5/pull/412) fix(shader): reject position exports without vertex input info | Aceptado | Un shader de píxeles que exportaba una posición tumbaba el recompilador (puntero nulo) |
| [#455](https://github.com/boykopovar/AnyPS5/pull/455) fix(audio): bound ATRAC9 decoding to the superframe | Aceptado | Un audio ATRAC9 corrupto hacía que el decodificador leyera más allá del buffer del juego |
| [#488](https://github.com/boykopovar/AnyPS5/pull/488) fix(json2): throw on numbers that overflow a double | Aceptado | Un número JSON como `1e309` se convertía en infinito y cerraba el proceso al serializarlo |
| [#352](https://github.com/boykopovar/AnyPS5/pull/352) fix(savedata): reject invalid directory names in sceSaveDataDelete | Aceptado | Un `../` en el nombre de una partida borraba carpetas fuera de la de partidas |
| [#3631](https://github.com/boykopovar/AnyPS5/pull/3631) test(json2): destroy the value before constructing over it | Fusionada | Un test perdía un nodo de memoria, detectado por LeakSanitizer |
| [#3971](https://github.com/boykopovar/AnyPS5/pull/3971) fix(libkernel): limit param.json nesting depth | Fusionada | Un `param.json` con decenas de miles de arrays anidados cerraba el proceso (desbordamiento de pila) |

Mi fork, [arreina/AnyPS5](https://github.com/arreina/AnyPS5), añade la integración continua de este trabajo: jobs con AddressSanitizer y UBSan, análisis estático (cppcheck, clang-tidy), validación de SPIR-V y fuzzers para el lector ELF, los decodificadores de instrucciones x86 y de GPU, el recompilador de shaders, la caché de shaders, JSON y los paquetes de comandos de GPU. Han encontrado más de una docena de bugs; los que aún no se han reportado están en cola.

Issues que he reportado:

| Issue | Estado | Qué es |
|---|---|---|
| [#1276](https://github.com/boykopovar/AnyPS5/issues/1276) ANYPS5_ENABLE_SPIRV_TOOLS: CCP turns a constant byte store into an 8-bit OpConstant that the module cannot declare | Arreglada en [#1343](https://github.com/boykopovar/AnyPS5/pull/1343) 14 horas después | La encontró el fuzzer del recompilador; el arreglo se probó con el shader de la issue |
| [#3634](https://github.com/boykopovar/AnyPS5/issues/3634) AddressSanitizer on Linux: the PS5 window is the shadow gap, so the guest arena has no free range | Arreglada en [#3705](https://github.com/boykopovar/AnyPS5/pull/3705) (por otra persona) | Las compilaciones con sanitizers no podían reservar memoria del guest. La solución usa el mismo enfoque que la solución descrita en la incidencia: sacar la ventana del guest del hueco de sombra |

También ejecuté los tests de AMD de la [#487](https://github.com/boykopovar/AnyPS5/issues/487) en una Radeon RX 580 (Polaris), y un mantenedor citó el resultado al cerrarla.

En la [#2709](https://github.com/boykopovar/AnyPS5/issues/2709), un fallo intermitente del test `guest_avplayer`, ejecuté 1.000 pruebas de estrés con AddressSanitizer y UBSan sin ningún fallo en Linux y publiqué el resultado. El fallo que quedaba en Windows lo arregló otra persona en la [#5733](https://github.com/boykopovar/AnyPS5/pull/5733).

### [Coucou](https://github.com/Louis-CFM/coucou) · Tauri (Rust, TypeScript)

Aplicación de escritorio que muestra en la parte superior de la pantalla el estado de las sesiones de agentes de programación (Claude Code, Codex, Gemini CLI y otros). Mis contribuciones son a su versión para Linux.

| Pull request | Estado | Qué hace |
|---|---|---|
| [#104](https://github.com/Louis-CFM/coucou/pull/104) Linux (X11): keep the island unfocusable and on every workspace | Aceptado | La ventana ya no roba el foco del teclado y aparece en todos los escritorios |
| [#110](https://github.com/Louis-CFM/coucou/pull/110) Pause idle animations, and stop polling for a cursor Linux doesn't have | Aceptado | Menos consumo de CPU en reposo |
| [#111](https://github.com/Louis-CFM/coucou/pull/111) Linux: shrink the hidden island to its wake strip, and only take clicks there | Aceptado | La ventana oculta ya no bloquea los clics en las ventanas de debajo |
| [#105](https://github.com/Louis-CFM/coucou/pull/105) Add npm run fake-session to try the island without Claude Code | En revisión | Una sesión simulada para desarrollar y probar sin un agente |
| [#106](https://github.com/Louis-CFM/coucou/pull/106) Ignore clicks on a fresh approval card, and wire up Y / N | Cerrado | Evitaba aprobar un permiso por accidente; se cerró porque el proyecto integró por separado el mismo bloqueo de clics |

### [LibAtrac9](https://github.com/shadps4-emu/ext-LibAtrac9) · C

Decodificador de audio ATRAC9 que usan emuladores de PS4/PS5.

| Pull request | Estado | Qué corrige |
|---|---|---|
| [#5](https://github.com/shadps4-emu/ext-LibAtrac9/pull/5) Range-check band extension, gradient and channel config parameters | En revisión (aprobado por un revisor) | Frames de audio corruptos hacían que el decodificador leyera y escribiera fuera de sus propios arrays |

## Proyectos propios

### [Lince](https://github.com/arreina/lince) · C

Lenguaje de programación de propósito general con palabras clave en español, para que programar no exija saber inglés. Escrito en C puro, sin dependencias externas; se compila con `gcc` y `make` en Linux, macOS y Windows. La versión 0.6 tiene clases, interfaces, enumeraciones, generadores y closures, librerías que se pueden repartir en varios ficheros y con espacio de nombres propio, y un compilador que genera ejecutables nativos. Los ejemplos del manual son ficheros `.lince` reales que se ejecutan al generar la página, así que la salida que muestra es la que producen. Web: [arreina.github.io/lince](https://arreina.github.io/lince) · [Manual](https://arreina.github.io/lince/manual.html).

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
