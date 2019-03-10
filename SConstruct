import os
PLATFORM = Platform()
DEBUG = ARGUMENTS.get("debug", 0)

CUDA_PATH = os.environ['CUDA_PATH']
CUDA_INCLUDE_PATH = CUDA_PATH + "/include"
OPTIX_PATH = os.environ.get('OPTIX_PATH', os.environ['HOME'] + "/.local/bin/optix")
OPTIX_INCLUDE_PATH = OPTIX_PATH + "/include"

ENV = Environment(CPPPATH = ['.', OPTIX_INCLUDE_PATH, "./contrib/OpenImageIO/include", CUDA_INCLUDE_PATH
],
                  CCFLAGS="-std=c++11 /EHsc")

# Used for debbugging
if int(DEBUG):
    ENV.Append(CCFLAGS=' -ggdb3')

SOURCES = Glob("src/*.cpp")

LIBPATH = []
if PLATFORM.name == "darwin":
    LIBPATH.append("/usr/local/lib")
if PLATFORM.name == "win32":
    LIBPATH.append("./contrib/OpenImageIO/lib")
    LIBPATH.append(CUDA_PATH + "/lib/x64")
if PLATFORM.name == "linux":
    LIBPATH.append("./contrib/optix/lib64")
    LIBPATH.append(CUDA_PATH + "/lib/x64")


LIBS = []
LIBS.append("optix")
LIBS.append("OpenImageIO")
LIBS.append("cudart_static")
if PLATFORM.name == "win32":
    LIBS.append("Cfgmgr32")

LINKFLAGS = []
LINKFLAGS.append("-Wl,-rpath=.")

program = ENV.Program(target="bin/Denoiser", source=SOURCES, LIBPATH=LIBPATH, LIBS=LIBS, LINKFLAGS=LINKFLAGS)
