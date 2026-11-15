# MimikaVR runtime packs

This repository holds the runtime packs that the MimikaVR web installer downloads while it installs. It contains no part
of MimikaVR itself: no code, no installer and no data.

A runtime pack is libtorch, the C++ library of PyTorch, built for CUDA 12.8, together with the NVIDIA CUDA and cuDNN
runtime libraries it is built against and the few small libraries that come with it. MimikaVR's tracking engine uses it
to run and train its models on an NVIDIA graphics card. These files make up about 4.1 GB of the 4.5 GB that MimikaVR
takes on disk. The full MimikaVR installer carries them inside itself, which makes it about 1.8 GB. The web installer
leaves them out and is about 150 MB instead: while it installs, it downloads the pack from this repository's releases.
When the same pack is already installed, for example during an update, it downloads nothing.

## Releases

Each release is one pack, named after its libtorch build. A pack comes as three 7-Zip archives, so that an interrupted
download only has to repeat one of them: `-torch.7z` holds libtorch, `-cuda.7z` the CUDA libraries and `-cudnn.7z` the
cuDNN libraries. The web installer checks the SHA-256 of each archive before it extracts it, and the release notes list
these checksums. A published pack is never changed: a new libtorch build gets a new release.

| Release | libtorch | CUDA | cuDNN |
|---|---|---|---|
| `libtorch-cuda-12.8-2.10.0` | 2.10.0 | 12.8 | 9.10.2 |

## Licenses

The files in the packs belong to their authors. They are redistributed here as part of MimikaVR, under their own
licenses:

- libtorch: the PyTorch license and the licenses of the third-party code that PyTorch includes
  ([licenses/libtorch-LICENSE.txt](licenses/libtorch-LICENSE.txt));
- the CUDA libraries: the [NVIDIA CUDA Toolkit End User License Agreement](https://docs.nvidia.com/cuda/eula/index.html),
  which allows these runtime libraries to be distributed as part of an application;
- the cuDNN libraries: the
  [NVIDIA cuDNN Software License Agreement](https://docs.nvidia.com/deeplearning/cudnn/latest/reference/eula.html),
  which allows the same;
- Intel's OpenMP runtime, libuv and zlib, which come with libtorch: their own licenses.

[NOTICE.txt](NOTICE.txt) lists every file of a pack with its license. The packs are here for MimikaVR's installer; any
other use is governed by the components' own licenses alone.
