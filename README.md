# Alberto Ruiz

[Español](README.es.md)

I build software by directing AI coding agents ([Claude Code](https://claude.com/claude-code)). I choose what to work on, set the constraints, decide what gets proposed to other projects and handle the conversation with their maintainers. The agent writes and tests the code. Every pull request below says so in its description.

## Open source contributions

### [AnyPS5](https://github.com/boykopovar/AnyPS5) · C++20, CMake

A tool that ports PS5 executables to Linux and Windows. My contributions are robustness fixes found with fuzzing and sanitizers. Each one has a regression test.

| Pull request | Status | What it fixes |
|---|---|---|
| [#183](https://github.com/boykopovar/AnyPS5/pull/183) fix(relinker): require a full ELF64 header before reading it | Merged | Truncated input files were read past their end |
| [#193](https://github.com/boykopovar/AnyPS5/pull/193) fix(relinker): keep ELF bounds checks from overflowing | Merged | Crafted offsets wrapped the bounds check (heap overflow) |
| [#213](https://github.com/boykopovar/AnyPS5/pull/213) fix(shader): skip the push constant copy when there is nothing to copy | Merged | Undefined behaviour reported by UBSan in the shader cache |
| [#280](https://github.com/boykopovar/AnyPS5/pull/280) fix(shader): reject SDWA and DPP instructions without their modifier word | Merged | Truncated GPU instructions were read out of bounds |
| [#328](https://github.com/boykopovar/AnyPS5/pull/328) fix(json2): reject documents nested deeper than 512 levels | In review | Deeply nested JSON crashed the process (stack overflow) |
| [#412](https://github.com/boykopovar/AnyPS5/pull/412) fix(shader): reject position exports without vertex input info | In review | A pixel shader exporting a position crashed the recompiler (null pointer) |
| [#352](https://github.com/boykopovar/AnyPS5/pull/352) fix(savedata): reject invalid directory names in sceSaveDataDelete | In review | `../` in a save name deleted directories outside the save folder |

My fork, [arreina/AnyPS5](https://github.com/arreina/AnyPS5), adds CI for this work: AddressSanitizer and UBSan jobs, static analysis (cppcheck, clang-tidy), SPIR-V validation, and fuzzers for the ELF reader, x86 and GPU instruction decoders, the shader recompiler, the shader cache, JSON and GPU command packets. They found 11 bugs; the rest are queued for upstream.

### [Coucou](https://github.com/Louis-CFM/coucou) · Tauri (Rust, TypeScript)

A desktop companion that shows the state of coding agent sessions (Claude Code, Codex, Gemini CLI and others) at the top of the screen. My contributions are to its Linux version.

| Pull request | Status | What it does |
|---|---|---|
| [#104](https://github.com/Louis-CFM/coucou/pull/104) Linux (X11): keep the island unfocusable and on every workspace | Merged | The overlay no longer steals keyboard focus and follows you across workspaces |
| [#110](https://github.com/Louis-CFM/coucou/pull/110) Pause idle animations, and stop polling for a cursor Linux doesn't have | Merged | Lower idle CPU use |
| [#111](https://github.com/Louis-CFM/coucou/pull/111) Linux: shrink the hidden island to its wake strip, and only take clicks there | Merged | The hidden overlay no longer blocks clicks on the windows below it |
| [#105](https://github.com/Louis-CFM/coucou/pull/105) Add npm run fake-session to try the island without Claude Code | In review | A simulated session for developing and testing without an agent |
| [#106](https://github.com/Louis-CFM/coucou/pull/106) Ignore clicks on a fresh approval card, and wire up Y / N | In review | Prevents approving a permission request by accident; adds keyboard shortcuts |

## Own projects

### [Lince](https://github.com/arreina/lince) · C

A general-purpose programming language with Spanish keywords, so that programming does not require knowing English. Written in plain C with no external dependencies; builds with `gcc` and `make` on Linux, macOS and Windows. Version 0.5 has classes and types, and a compiler that produces native executables. Website: [arreina.github.io/lince](https://arreina.github.io/lince).

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

## How the work is done

- Small, single-topic changes that follow each project's conventions
- Bug fixes come with a regression test where the project has a test suite, checked to fail without the fix
- Only synthetic test data; no proprietary content
- Nothing is published to another project without my review
