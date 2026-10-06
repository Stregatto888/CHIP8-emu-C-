# ChippOtto - CHIP-8 Emulator

Un emulatore CHIP-8 in C++ con interfaccia SDL2 su Arch Linux.

## 🎯 Obiettivi

- [ ] Comprendere come funziona una CPU virtuale (fetch-decode-execute)
- [ ] Implementare l'architettura CHIP-8 completa
- [ ] Comunicare con memoria, registri e I/O
- [ ] Rendering grafico con SDL2
- [ ] Gestione input da tastiera

## 📋 Passi da fare

### 1. Setup Ambiente

- Installare dipendenze: `sudo pacman -S base-devel gdb sdl2`
- Creare struttura cartelle: `src/`, `build/`, `roms/`
- Creare `Makefile` per compilazione
- Configurare VS Code (C/C++, tasks.json, launch.json)

### 2. Struttura Hardware (chip8.h)

- Memoria: `uint8_t memory[4096]`
- Registri: `uint8_t V[16]` (V0-VF)
- Registro Indice: `uint16_t index`
- Program Counter: `uint16_t pc` (inizia a 0x200)
- Stack: `uint16_t stack[16]` + Stack Pointer
- Timer: `delayTimer`, `soundTimer` (60Hz)
- I/O: `keypad[16]`, `video[64*32]`
- Opcode corrente: `uint16_t opcode`

### 3. Implementazione CPU (chip8.cpp)

- **Constructor**: Caricamento fontset (80 byte)
- **LoadROM()**: Lettura file binario ROM in memoria da 0x200
- **Cycle()**: Fetch-Decode-Execute
  - Fetch: Leggere 2 byte dalla memoria e formare opcode
  - Decode & Execute: Switch su primo nibble (4 bit)
  - Implementare 35 opcodes CHIP-8
- **UpdateTimers()**: Decremento timer a ogni ciclo

### 4. Interfaccia Grafica (main.cpp)

- Inizializzazione SDL2
- Creazione finestra (64x32 con scala 10x)
- Loop principale a 60 FPS
- Polling eventi (SDL_PollEvent)
- Mappatura tastiera → 16 tasti CHIP-8 (0-F)
- Rendering video buffer SDL_Texture
- Cleanup risorse SDL2

### 5. Compilazione e Test

- Build con Makefile
- Testare con ROM pubbliche (IBM_Logo.ch8, Pong.ch8, ecc.)
- Debug con GDB in VS Code

## 🏗️ Architettura CHIP-8

| Aspetto  | Dettagli                   |
| -------- | -------------------------- |
| CPU      | 8-bit, 500-600 Hz          |
| Memoria  | 4KB (0x000-0xFFF)          |
| Registri | 16 (V0-VF, 8-bit)          |
| Stack    | 16 livelli                 |
| Schermo  | 64×32 pixel, monocromatico |
| Tastiera | 16 tasti esadecimali (0-F) |
| Opcodes  | 35 istruzioni              |

## 📚 Risorse Utili

- [Cowgod's Chip-8 Reference](http://devernay.free.fr/hacks/chip8/C8TECH10.HTM)
- [CHIP-8 Wikipedia](https://en.wikipedia.org/wiki/CHIP-8)
- [Chip-8 Technical Reference](https://github.com/mattmikolay/chip-8/wiki/CHIP%E2%80%908-Technical-Reference)
