# Using LSP's with Sublime
## For C language
### Installation
- install clang on the system with the package manager (sudo pacman -S clang)
- install LSP with package control (Ctrl-shift-p)
- install LSP-clangd with package control
- restart sublime-text

### Usage
- clangd need to know all the locations where file from the project are located.
- for cmake project use the ```-DCMAKE_EXPORT_COMPILE_COMMANDS=1``` to compile the project or use ```SET(CMAKE_EXPORT_COMPILE_COMMANDS 1)```
  this way the "compile_commands.json" file will be generated, which is used by clangd to find everything
- if the "compile_commands.json" file is not found by the clangd add a ".clangd" file as far up in the project hirarchy as possilbe and indicate where the "compile_commands.json" file can be found.
- contenet of ".clangd" is as follows:
```
CompileFlags:
  CompilationDatabase: build/       # Search build/ directory for compile_commands.json path must be relative to ".clangd"
```
`
