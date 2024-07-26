# raylib-rlights-fix
A simple rlights.h fix from raysan5/raylib/examples/shaders for ziggers (0.12.0)

# Problems
UpdateLightValues doesn't work, because light itself passed as structure (not pointer). It's okay for C/C++ but might cause problems with translators (as it is in zig currently)
No `#define` in zig, so `#if defined(RLIGHTS_IMPLEMENTATION)` will always hide implementation.
# Solutions
Redesigned `void UpdateLightValues(Shader, Light)` to `void UpdateLightValues(Shader, Light*)`. Using new function you will pass an address of light (which makes sense) so `zig translate-c` works too.
Removed `defined(RLIGHTS_IMPLEMENTATION)` so there is no need to `#define`
