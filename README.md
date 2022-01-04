# Notes

All forked code is here: 

[https://github.com/thelamer/retrostash](https://github.com/thelamer/retrostash)

We build these cores using emsdk 1.39.5.

## Basic build instructions

```
git clone https://github.com/emscripten-core/emsdk.git
cd emsdk
./emsdk install 1.39.5
./emsdk activate 1.39.5
Follow instructions for sourcing paths to shell

git clone https://github.com/thelamer/retrostash.git
cd retrostash/libretro-fceumm
emmake make -f Makefile -j6 platform=emscripten
cd ../Retroarch/dist-scripts
cp ../../libretro-fceumm/fceumm_libretro_emscripten.bc .
emmake ./dist-cores.sh emscripten
```

Resulting build output will be in `../pkg/emscripten`.
After these files are built run the following command to utilize the pre-initiated audio context used by libretrojs: (needed for safari compatibility)

```
sed -i 's/context:undefined/context:readyAudioContext/g'
```

# Notes

### beetle-pce-fast

Built at commit 1efc0309b65ce77ad5121a6c5f329ad9e26a6ded before breaking filestream changes. Slight makefile tweaks for static chd support: 

### melonds
Need to swap the static linking include in Makefile.common

### beetle psx

Forked here also [https://github.com/thelamer/beetle-psx-libretro](https://github.com/thelamer/beetle-psx-libretro)

Tweaks for memory limits.
