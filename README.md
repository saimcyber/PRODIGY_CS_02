# Keylogger (Educational)

A minimal Windows keystroke logger written in C++ as a learning exercise in the
Win32 API — low-level input hooks, virtual-key translation, and buffered file I/O.

![Language: C++](https://img.shields.io/badge/language-C%2B%2B-00599C?logo=cplusplus&logoColor=white)
![Platform: Windows](https://img.shields.io/badge/platform-Windows-0078D6?logo=windows&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)

---

> ## ⚠️ Legal & ethical notice
>
> This project is published **for education and authorized security research only.**
> Running software that records another person's keystrokes without their knowledge
> and consent is illegal in most jurisdictions.
>
> **Only run this on a device you own, or on a system where you have explicit written
> authorization to do so.** You are solely responsible for how you use it. The author
> accepts no liability for misuse.

---

## What it demonstrates

- Installing a global **`WH_KEYBOARD_LL`** low-level keyboard hook with
  `SetWindowsHookEx`
- Translating virtual-key codes into readable tokens (`[BACKSPACE]`, `[TAB]`,
  named keys) and, optionally, raw decimal/hex codes
- Buffered append-only logging to a text file
- A Windows message loop (`GetMessage` / `DispatchMessage`)

It does **not** implement persistence, privilege escalation, hiding from task
managers, or any network exfiltration — and it should not.

## Build

Requires the Windows SDK and a C++ toolchain (MSVC or MinGW-w64).

**MSVC (Developer Command Prompt):**

```bat
cl /EHsc /DUNICODE /D_UNICODE keylogger.cpp user32.lib
```

**MinGW-w64:**

```bash
g++ -municode -O2 keylogger.cpp -o keylogger.exe -luser32
```

## Configuration

Compile-time `#define`s at the top of `keylogger.cpp`:

| Define | Effect |
| --- | --- |
| `visible` / `invisible` | show or hide the console window at start |
| `bootwait` / `nowait` | delay on launch (useful when started at boot) |
| `FORMAT` | `0` = named keys, `10` = decimal codes, `16` = hex codes |
| `mouseignore` | drop mouse events from the log |

The `invisible` option exists because hiding a console is a standard Win32
exercise — but a hidden logger on someone else's machine is exactly the misuse the
notice above forbids.

## License

MIT — see [LICENSE](LICENSE).
