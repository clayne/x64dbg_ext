This is the library that extends x64dbg with new features:

* Telescope
* Unicorn emulator to predict code flow

Both features actually inspired by projects like [GEF](https://github.com/hugsy/gef) and  [pwndbg](https://github.com/pwndbg/pwndbg).

# Install

Copy `ext.dp64` (original file name `x64dbg_ext.dll`) to x64dbg plugins directory.

# Usage

Plugin adds three commands:

* `telescope` recursive symbolic dereferencer. 
* `unicorn` emulation with symbolic traces.
* `context` print current context, instead of disasm print `unicorn` output and apply `telescope` to the stack.

Here is how `context` looks like:

![](pngs/Screenshot1.png)

# Build

Set `LIBCLANG_PATH` for bindgen to work

```
set LIBCLANG_PATH=C:\Program Files\LLVM\bin
cargo build --release
```

## Development build

Build [PluginDebHelper](https://github.com/x64dbg/PluginDevHelper), then:

```
mklink target\release\x64dbg_ext.dll <x64dbg plugins>\ext.dp64
PluginDevServer.exe

PluginDevBuildTool.exe unload <x64dbg plugins>\ext.dp64
cargo build --release 
PluginDevBuildTool.exe reload <x64dbg plugins>\ext.dp64
```

# Limitations

* Performance issues. Just initializing Unicorn context takes ~1GB of RAM. 
* User experience. Logs tab, despite having html support, is probably not a best place to have a UI.

# Thanks to

Special thanks for [@mrexodia](https://github.com/mrexodia) for creating and maintaing x64dbg, consider [donating](https://github.com/sponsors/mrexodia?metadata_source=x64dbg-site).
