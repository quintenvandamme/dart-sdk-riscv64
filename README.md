# dart-sdk-riscv64
The dart sdk for riscv64

![Dart-platforms](https://user-images.githubusercontent.com/58103738/205509126-c0d3ba61-dbae-4bdb-b8d8-39230479c999.svg)


# Linux x86_64 (Ubuntu)

Install build tools:

```
sudo apt-get install git python3 curl g++-riscv64-linux-gnu
```

Install Chromium's depot tools:

```
git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
export PATH="$PATH:$PWD/depot_tools"
```

Get the dart sdk:

```
mkdir dart-sdk
cd dart-sdk
fetch dart
```


Patch the build files:

```
cd sdk
sed -i '/-Werror/d' runtime/BUILD.gn
sed -i '/-Wno-unused-private-field/d' runtime/BUILD.gn
sed -i '/-Werror/d' build/config/compiler/BUILD.gn
```

Build the sdk. Note that you don't need to add the g++ suffix to the riscv64 cross compiler path.

```
./tools/build.py --no-goma --no-clang -m release -a riscv64 -t riscv64=/usr/bin/riscv64-linux-gnu- create_sdk
```
