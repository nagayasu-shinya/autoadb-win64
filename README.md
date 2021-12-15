# autoadb-win64
AutoAdb binary file (executable file) for 64bit Windows.

## what's AutoAdb ?
This command-line tool allows to execute a command whenever a new device is connected to adb.

* [Official GitHub](https://github.com/rom1v/autoadb)

## How to install AutoAdb for win64 ?

Just download autoadb.exe and set PATH to the files.

## How to use ?

For example,

```
autoadb.exe scrcpy.exe -s {}
```

{} replaces the serial of the device detected.


### How to build this binary

This binary is build on Ubuntu 20.04. All it takes is following.

```bash
$ sudo apt install gcc-mingw-w64-x86-64
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

And close terminal and restart.

```bash
$ rustup target add x86_64-pc-windows-gnu
$ vim ~/.cargo/config
$ cat ~/.cargo/config
[target.x86_64-pc-windows-gnu]
linker = "x86_64-w64-mingw32-gcc"
ar = "x86_64-w64-mingw32-gcc-ar"
$ git clone https://github.com/rom1v/autoadb.git
$ cd autoadb/
$ cargo build --release --target=x86_64-pc-windows-gnu
```

It will generate target/x86_64-pc-windows-gnu/release/autoadb.exe.

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
