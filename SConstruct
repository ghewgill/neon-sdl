import os
import re
import shutil
import sys
import tarfile

libsdl = None

env = Environment()
if sys.platform == "win32":
    env.Append(CXXFLAGS=["/EHsc"])
if "RELEASE" not in env or not env["RELEASE"]:
    if sys.platform == "win32":
        env.Append(CXXFLAGS=[
            "/MDd",
            "/Zi",
            "/Od",
        ])

libsdlenv = Environment()
if "RELEASE" not in env or not env["RELEASE"]:
    if sys.platform == "win32":
        libsdlenv.Append(CFLAGS=[
            "/MDd",
            "/Zi",
            "/Od",
        ])

if GetOption("clean"):
    shutil.rmtree("SDL2-2.0.3", ignore_errors=True)
elif not os.path.exists("SDL2-2.0.3/configure"):
    tarfile.open("SDL2-2.0.3.tar.gz").extractall(".")
    if sys.platform == "win32":
        config = open("SDL2-2.0.3/include/SDL_config_windows.h").read()
        config = re.sub(r"SDL_AUDIO_DRIVER_XAUDIO2\s+1", "SDL_AUDIO_DRIVER_XAUDIO2 0", config)
        open("SDL2-2.0.3/include/SDL_config_windows.h", "w").write(config)
        dynapi = open("SDL2-2.0.3/src/dynapi/SDL_dynapi.h").read()
        dynapi = re.sub(r"SDL_DYNAMIC_API\s+1", "SDL_DYNAMIC_API 0", dynapi)
        open("SDL2-2.0.3/src/dynapi/SDL_dynapi.h", "w").write(dynapi)

if sys.platform == "win32":
    env.Append(LIBS=["gdi32", "imm32", "kernel32", "ole32", "oleaut32", "shell32", "user32", "version", "winmm"])
    libsdlenv.Append(CPPPATH=["SDL2-2.0.3/include"])
    libsdl = libsdlenv.Library("SDL2-2.0.3/sdl.lib", [
        "SDL2-2.0.3/src/SDL.c",
        "SDL2-2.0.3/src/SDL_assert.c",
        "SDL2-2.0.3/src/SDL_error.c",
        "SDL2-2.0.3/src/SDL_hints.c",
        "SDL2-2.0.3/src/SDL_log.c",
        "SDL2-2.0.3/src/atomic/SDL_atomic.c",
        "SDL2-2.0.3/src/atomic/SDL_spinlock.c",
        "SDL2-2.0.3/src/audio/SDL_audio.c",
        "SDL2-2.0.3/src/audio/SDL_audiocvt.c",
        "SDL2-2.0.3/src/audio/SDL_audiotypecvt.c",
        "SDL2-2.0.3/src/audio/SDL_mixer.c",
        "SDL2-2.0.3/src/audio/directsound/SDL_directsound.c",
        "SDL2-2.0.3/src/audio/disk/SDL_diskaudio.c",
        "SDL2-2.0.3/src/audio/dummy/SDL_dummyaudio.c",
        "SDL2-2.0.3/src/audio/winmm/SDL_winmm.c",
        "SDL2-2.0.3/src/audio/xaudio2/SDL_xaudio2.c",
        "SDL2-2.0.3/src/core/windows/SDL_windows.c",
        "SDL2-2.0.3/src/cpuinfo/SDL_cpuinfo.c",
        "SDL2-2.0.3/src/events/SDL_clipboardevents.c",
        "SDL2-2.0.3/src/events/SDL_dropevents.c",
        "SDL2-2.0.3/src/events/SDL_events.c",
        "SDL2-2.0.3/src/events/SDL_gesture.c",
        "SDL2-2.0.3/src/events/SDL_keyboard.c",
        "SDL2-2.0.3/src/events/SDL_mouse.c",
        "SDL2-2.0.3/src/events/SDL_quit.c",
        "SDL2-2.0.3/src/events/SDL_touch.c",
        "SDL2-2.0.3/src/events/SDL_windowevents.c",
        "SDL2-2.0.3/src/file/SDL_rwops.c",
        "SDL2-2.0.3/src/haptic/SDL_haptic.c",
        "SDL2-2.0.3/src/haptic/windows/SDL_syshaptic.c",
        "SDL2-2.0.3/src/joystick/SDL_gamecontroller.c",
        "SDL2-2.0.3/src/joystick/SDL_joystick.c",
        "SDL2-2.0.3/src/joystick/windows/SDL_dxjoystick.c",
        "SDL2-2.0.3/src/libm/e_atan2.c",
        "SDL2-2.0.3/src/libm/e_log.c",
        "SDL2-2.0.3/src/libm/e_pow.c",
        "SDL2-2.0.3/src/libm/e_rem_pio2.c",
        "SDL2-2.0.3/src/libm/e_sqrt.c",
        "SDL2-2.0.3/src/libm/k_cos.c",
        "SDL2-2.0.3/src/libm/k_rem_pio2.c",
        "SDL2-2.0.3/src/libm/k_sin.c",
        "SDL2-2.0.3/src/libm/s_atan.c",
        "SDL2-2.0.3/src/libm/s_copysign.c",
        "SDL2-2.0.3/src/libm/s_cos.c",
        "SDL2-2.0.3/src/libm/s_fabs.c",
        "SDL2-2.0.3/src/libm/s_floor.c",
        "SDL2-2.0.3/src/libm/s_scalbn.c",
        "SDL2-2.0.3/src/libm/s_sin.c",
        "SDL2-2.0.3/src/loadso/windows/SDL_sysloadso.c",
        "SDL2-2.0.3/src/render/SDL_d3dmath.c",
        "SDL2-2.0.3/src/render/SDL_render.c",
        "SDL2-2.0.3/src/render/SDL_yuv_sw.c",
        "SDL2-2.0.3/src/render/direct3d/SDL_render_d3d.c",
        "SDL2-2.0.3/src/render/opengl/SDL_render_gl.c",
        "SDL2-2.0.3/src/render/opengl/SDL_shaders_gl.c",
        "SDL2-2.0.3/src/render/opengles2/SDL_render_gles2.c",
        "SDL2-2.0.3/src/render/opengles2/SDL_shaders_gles2.c",
        "SDL2-2.0.3/src/render/software/SDL_blendfillrect.c",
        "SDL2-2.0.3/src/render/software/SDL_blendline.c",
        "SDL2-2.0.3/src/render/software/SDL_blendpoint.c",
        "SDL2-2.0.3/src/render/software/SDL_drawline.c",
        "SDL2-2.0.3/src/render/software/SDL_drawpoint.c",
        "SDL2-2.0.3/src/render/software/SDL_render_sw.c",
        "SDL2-2.0.3/src/render/software/SDL_rotate.c",
        "SDL2-2.0.3/src/stdlib/SDL_getenv.c",
        "SDL2-2.0.3/src/stdlib/SDL_iconv.c",
        "SDL2-2.0.3/src/stdlib/SDL_malloc.c",
        "SDL2-2.0.3/src/stdlib/SDL_qsort.c",
        "SDL2-2.0.3/src/stdlib/SDL_stdlib.c",
        "SDL2-2.0.3/src/stdlib/SDL_string.c",
        "SDL2-2.0.3/src/thread/SDL_thread.c",
        "SDL2-2.0.3/src/thread/generic/SDL_syscond.c",
        "SDL2-2.0.3/src/thread/windows/SDL_sysmutex.c",
        "SDL2-2.0.3/src/thread/windows/SDL_syssem.c",
        "SDL2-2.0.3/src/thread/windows/SDL_systhread.c",
        "SDL2-2.0.3/src/thread/windows/SDL_systls.c",
        "SDL2-2.0.3/src/timer/SDL_timer.c",
        "SDL2-2.0.3/src/timer/windows/SDL_systimer.c",
        "SDL2-2.0.3/src/video/SDL_blit.c",
        "SDL2-2.0.3/src/video/SDL_blit_0.c",
        "SDL2-2.0.3/src/video/SDL_blit_1.c",
        "SDL2-2.0.3/src/video/SDL_blit_A.c",
        "SDL2-2.0.3/src/video/SDL_blit_auto.c",
        "SDL2-2.0.3/src/video/SDL_blit_copy.c",
        "SDL2-2.0.3/src/video/SDL_blit_N.c",
        "SDL2-2.0.3/src/video/SDL_blit_slow.c",
        "SDL2-2.0.3/src/video/SDL_bmp.c",
        "SDL2-2.0.3/src/video/SDL_egl.c",
        "SDL2-2.0.3/src/video/SDL_fillrect.c",
        "SDL2-2.0.3/src/video/SDL_pixels.c",
        "SDL2-2.0.3/src/video/SDL_rect.c",
        "SDL2-2.0.3/src/video/SDL_RLEaccel.c",
        "SDL2-2.0.3/src/video/SDL_shape.c",
        "SDL2-2.0.3/src/video/SDL_stretch.c",
        "SDL2-2.0.3/src/video/SDL_surface.c",
        "SDL2-2.0.3/src/video/SDL_video.c",
        "SDL2-2.0.3/src/video/dummy/SDL_nullevents.c",
        "SDL2-2.0.3/src/video/dummy/SDL_nullframebuffer.c",
        "SDL2-2.0.3/src/video/dummy/SDL_nullvideo.c",
        "SDL2-2.0.3/src/video/windows/SDL_windowsclipboard.c",
        "SDL2-2.0.3/src/video/windows/SDL_windowsevents.c",
        "SDL2-2.0.3/src/video/windows/SDL_windowsframebuffer.c",
        "SDL2-2.0.3/src/video/windows/SDL_windowskeyboard.c",
        "SDL2-2.0.3/src/video/windows/SDL_windowsmessagebox.c",
        "SDL2-2.0.3/src/video/windows/SDL_windowsmodes.c",
        "SDL2-2.0.3/src/video/windows/SDL_windowsmouse.c",
        "SDL2-2.0.3/src/video/windows/SDL_windowsopengl.c",
        "SDL2-2.0.3/src/video/windows/SDL_windowsopengles.c",
        "SDL2-2.0.3/src/video/windows/SDL_windowsshape.c",
        "SDL2-2.0.3/src/video/windows/SDL_windowsvideo.c",
        "SDL2-2.0.3/src/video/windows/SDL_windowswindow.c",
    ])
else:
    libsdl = libsdlenv.Command("SDL2-2.0.3/build/.libs/libSDL2.a", "SDL2-2.0.3/configure", "cd lib/sdl/SDL2-2.0.3 && env CFLAGS=-fPIC ./configure && make")
    if sys.platform.startswith("darwin"):
        env.Append(LIBS=["iconv", "objc"])
        env.Append(FRAMEWORKS=["AppKit", "AudioUnit", "Carbon", "CoreAudio", "CoreFoundation", "CoreGraphics", "ForceFeedback", "IOKit"])
    else:
        env.Append(LIBS="pthread")

env.Append(CPPPATH=["SDL2-2.0.3/include"])

env.Append(CPPPATH=["../../common"])
env.Append(LIBS=[libsdl])
env.SharedLibrary("neon_sdl", "sdl.cpp")
