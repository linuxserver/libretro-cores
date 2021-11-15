# Notes

Compiled inside `git.libretro.com:5050/libretro-infrastructure/libretro-build-emscripten:latest` container, general steps: 

Clone code for libretro emu:
```
git clone https://github.com/libretro/stella2014-libretro.git
```

Compile bc file:
```
emmake make -f Makefile platform=emscripten
```

Grab pre-compiled libretro emscripten: (example old assets)
```
wget "https://git.libretro.com/libretro/RetroArch/-/jobs/1110508/artifacts/download?file_type=archive" -O precompiled.zip
```

Copy bc file to precompiled source as `libretro_emscripten.bc` and compile with: 
```
emmake make -f Makefile.emscripten -j$NUMPROC LIBRETRO=stella2014
```

### Virtual Jaguar
```
add STATIC_LINKING=1 to makefile
LDFLAGS="$CFLAGS -s TOTAL_MEMORY=33554432" emmake make -f Makefile platform=emscripten
```

### beetle-pce-fast

Built at commit 1efc0309b65ce77ad5121a6c5f329ad9e26a6ded before breaking filestream changes. Slight makefile tweaks for static chd support: 

```
# Emscripten
else ifeq ($(platform), emscripten)
   TARGET := $(TARGET_NAME)_libretro_$(platform).bc
   fpic    := -fPIC
   SHARED  := -shared -Wl,--no-undefined -Wl,--version-script=link.T
   HAVE_CHD = 1
   HAVE_CDROM = 0
   HAVE_NEON = 0
   STATIC_LINKING = 1
```

### melonds
```
else ifeq ($(platform), emscripten)
   TARGET := $(TARGET_NAME)_libretro_emscripten.bc
   fpic := -fPIC
   SHARED := -shared -Wl,--version-script=$(CORE_DIR)/link.T -Wl,--no-undefined
```

