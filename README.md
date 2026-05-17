# autoadb-win64
AutoAdb binary file (executable file) for 64bit Windows.

## What's AutoAdb?
This command-line tool allows to execute a command whenever a new device is connected to adb.

* [Official GitHub](https://github.com/rom1v/autoadb)

## How to Install AutoAdb for Win64

Just download `autoadb.exe` and add it to your Windows PATH.

## Prerequisites

Make sure `adb.exe` is in your Windows PATH. You can verify by running:

```
adb.exe version
```

If not found, add the Android SDK platform-tools directory (e.g. `C:\Users\<user>\AppData\Local\Android\Sdk\platform-tools`) to your PATH.

## Usage

For example, to launch [scrcpy](https://github.com/Genymobile/scrcpy) automatically when a device is connected:

```
autoadb.exe scrcpy.exe -s {}
```

`{}` is replaced with the serial of the detected device.

> [!NOTE]
> On Windows, shell built-in commands (like `echo`, `dir`, `type`) are not standalone executables. You must invoke them through `cmd.exe /C`:

```
autoadb.exe cmd.exe /C echo {}
```

### Usage from WSL

You can run the Windows binary directly from WSL:

```bash
autoadb.exe c:\\Programs\\scrcpy\\scrcpy.exe -s {}
```

Alternatively, use `wslpath` to convert the Windows path to WSL format:

```bash
autoadb.exe $(wslpath -w /mnt/c/Programs/scrcpy/scrcpy.exe) -s {}
```

Shell built-in commands (like `echo`) require `cmd.exe /C`:

```bash
autoadb.exe cmd.exe /C echo {}
```

## How to Build This Binary

This binary is built on Ubuntu (WSL or native). All it takes is the following:

```bash
sudo apt install gcc-mingw-w64-x86-64
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Close the terminal and restart, then:

```bash
rustup target add x86_64-pc-windows-gnu
mkdir -p ~/.cargo && echo -e '[target.x86_64-pc-windows-gnu]\nlinker = "x86_64-w64-mingw32-gcc"\nar = "x86_64-w64-mingw32-gcc-ar"' >> ~/.cargo/config
git clone https://github.com/rom1v/autoadb.git
cd autoadb/
cargo build --release --target=x86_64-pc-windows-gnu
```

The binary will be generated at `target/x86_64-pc-windows-gnu/release/autoadb.exe`.

## License
    Copyright (C) 2017 Genymobile
    Copyright (C) 2019 Romain Vimont

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
