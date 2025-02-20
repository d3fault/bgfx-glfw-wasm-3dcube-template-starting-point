# bgfx glfw3 wasm 3d cube template starting point

A basic spinning 3D cube, using bgfx and glfw3 compiling for WebAssembly (wasm) using Emscripten. Additionally compiles to native Linux/X11. Tested on Debian Bookworm (12), might work on Debian Bullseye (11). Very specific versions of bgfx and Emscripten are targeted; upgrading to newer versions may or may not work.

[Demo](http://d3fault.github.io/wasm-3d-demos/bgfx-glfw-wasm-3dcube-template-starting-point/index.html)

## WebAssembly

### Dependencies (WebAssembly)

* `# apt install git python3 xz-utils cmake make`

#### Install emscripten sdk and prepare build environment

* `git clone https://github.com/emscripten-core/emsdk.git`
* `cd emsdk`
* `./emsdk install 3.1.51 #only tested version. I've heard newer builds don't work, but they might now`
* `./emsdk activate 3.1.51`
* `source ./emsdk_env.sh`
* `cd ..`

### Building (WebAssembly)

* `git clone https://github.com/d3fault/bgfx-glfw-wasm-3dcube-template-starting-point.git`
* `cd bgfx-glfw-wasm-3dcube-template-starting-point`
* `git submodule update --init --recursive`
* `cd bgfx`
* `emmake make wasm-debug #it will probably error out on one of the examples, this is fine. just make sure bgfxDebug.bc, bxDebug.bc, and bimgDebug.bc exist in bgfx/.build/wasm/bin/`
* `cd ..`
* `emcmake cmake -B buildwasm`
* `cd buildwasm`
* `emmake make`

### Running (WebAssembly)

* `python -m SimpleHTTPServer 8080 #or other webserver`
* In your web browser: http://localhost:8080/index.html

## Native Linux/X11

### Dependencies (Linux/X11)

`# apt install git build-essential cmake libglfw3-dev`

### Building (Linux/X11)

* `git clone https://github.com/d3fault/bgfx-glfw-wasm-3dcube-template-starting-point.git`
* `cd bgfx-glfw-wasm-3dcube-template-starting-point`
* `git submodule update --init --recursive`
* `cd bgfx`
* `make linux-debug64 #it might error out on one of the examples, this is fine. just make sure libbgfx-shared-libDebug.so exists in bgfx/.build/linux64_gcc/bin/`
* `cd ..`
* `cmake -B buildnative`
* `cd buildnative`
* `cmake --build . --parallel`

### Running (Linux/X11)

* `./bgfx-glfw-wasm-3dcube-template-starting-point`

## TODO (patches welcome)

* Release builds
* Multi-threading(?)
* Newer Emscripten and bgfx versions
* Auto-detect screen dimensions
