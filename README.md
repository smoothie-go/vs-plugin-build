# vs-plugin-build

[VapourSynth](https://www.vapoursynth.com/) plugin build system for Linux/macOS. It is recommended to use [vsrepo](https://github.com/vapoursynth/vsrepo/) to install the plugins.
Currently most plugins included are simple to compile (no dependencies and standard build system). Other plugins will be added over time (pull requests to add new plugins are very welcome!).

## Plugin compatibility

Default requirements:
- linux-glibc-x86_64 (Linux 64-Bit, high compatibility): libc6 at least 2.17, Linux Kernel at least 3.2 (compiled with GCC 11)
- linux-glibc-x86_64-v3 (Linux 64-Bit, high performance): libc6 at least 2.35, Linux Kernel at least 6.1 (compiled with GCC 15.2)
- darwin-x86_64 (Intel Mac): At least OS X 10.11 El Capitan
- darwin-aarch64 (Apple Silicon Mac): At least macOS 11 Big Sur

If a plugin has higher or other requirements this is shown in the list.

### linux-glibc-x86_64-v3
These builds will only work on more recent Linux distributions and recent processors (x86-64-v3: Intel Core-i 4xxx or newer, all AMD Ryzen),
they provide higher perfomance, especially for plugins that don't already contain custom SSE/AVX optimizations.

## Plugin list

For each category the number of currently available plugins in this repo and the total number of plugins in vsrepo is given.
For a nice list of all plugins (and scripts/wheels) with more details, see the [VapourSynth Database](https://vsdb.top/vsrepogui).

|Name                                                        |  Linux (x86_64)  | macOS (Intel) |macOS (Apple Silicon)|
|------------------------------------------------------------|------------------|---------------|---------------------|
|[BestSource](https://github.com/vapoursynth/bestsource)      |        ✅         |  ✅ (10.15)  |      ✅       |
|[BM3D](https://github.com/HomeOfVapourSynthEvolution/VapourSynth-BM3D)              |        ✅         |      ✅      |      ✅       |
|[fmtconv](https://gitlab.com/EleonoreMizo/fmtconv)                          |        ✅         |      ✅      |      ✅       |
|[FrameBlender](https://github.com/couleurm/vs-frameblender)|        ✅         |      ✅      |      ✅       |
|[MVTools](https://github.com/dubhater/vapoursynth-mvtools)                            |        ✅         |      ✅      |      ✅       |

## Plugin issues

All 5 supported plugins build cleanly on all supported platforms.

### Howto fix build issues:
These are a few ideas how to fix build issues on Darwin/macOS:
- Configure or linking failures: These can most likely be fixed by using a newer (better) build system like meson. Creating a meson.build File for a plugin is very easy, see [here](https://github.com/dubhater/vapoursynth-mvtools/blob/master/meson.build) for an example (with nasm and dependencies).
- Only x86 supported / x86 intrinsics: [sse2neon](https://github.com/DLTcollab/sse2neon) can be used to convert SSE intrinsics to NEON. *sse2neon can also be used to convert SSE code to NEON for plugins that can already be build on aarch64 (Apple Silicon) to improve performance.*

If you like to help fixing these issues it is recommended that you open an issue on the plugin repository (or create an pull request that fixes the issue there) with the hope the author will release a new version with a fix. If the plugin is unmaintained (or the maintainer does not respond) you can may open an issue here, so the patch can be included in the build system (less desirable option).
