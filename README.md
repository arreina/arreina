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
| [#352](https://github.com/boykopovar/AnyPS5/pull/352) fix(savedata): reject invalid directory names in sceSaveDataDelete | In review | `../` in a save name deleted directories outside the save folder |

My fork, [arreina/AnyPS5](https://github.com/arreina/AnyPS5), adds CI for this work: AddressSanitizer and UBSan jobs, static analysis (cppcheck, clang-tidy), SPIR-V validation, and fuzzers for the ELF reader, x86 and GPU instruction decoders, the shader recompiler, the shader cache, JSON and GPU command packets. They found 11 bugs; the rest are queued for upstream.

## Own projects

| Project | Description |
|---|---|
| [lince](https://github.com/arreina/lince) · C | A general-purpose programming language in Spanish |
| [bot-reels-videojuegos](https://github.com/arreina/bot-reels-videojuegos) · Python | Turns video game news into vertical short videos: script, synthetic voice, royalty-free footage, controlled from a phone |

## How the work is done

- Small, single-topic changes that follow each project's conventions
- A regression test for every fix, checked to fail without it
- Only synthetic test data; no proprietary content
- Nothing is published to another project without my review
