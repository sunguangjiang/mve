# Introduction

The Multi-View Environment is an effort to ease the work with multi-view
datasets and to support the development of algorithms based on multiple
views. It features Structure from Motion, Multi-View Stereo and Surface
Reconstruction. MVE is developed at the TU Darmstadt. Visit the following
websites for more details.

 * http://www.gris.tu-darmstadt.de/projects/multiview-environment/
 * http://www.gris.tu-darmstadt.de/
 * http://www.tu-darmstadt.de/

This README covers compilation and basic information about the
pipeline. For documentation, please refer to the Wiki pages on GitHub.

  * https://github.com/simonfuhrmann/mve/wiki


# Building MVE and UMVE

To download and build MVE, type:

    $ git clone https://github.com/simonfuhrmann/mve.git
    $ cd mve
    $ make -j8

To compile and run UMVE, the Qt user interface, type:

    $ cd apps/umve/
    $ qmake && make -j8
    $ ./umve

System requirements to compile and run MVE or UVME are:

 * libjpeg (for MVE, http://www.ijg.org/)
 * libpng (for MVE, http://www.libpng.org/pub/png/libpng.html)
 * libtiff (for MVE, http://www.libtiff.org/)
 * OpenGL (for libogl in MVE and UMVE)
 * Qt 5 (for UMVE, http://www.qt.io)

Windows and OS X: Please refer to the Wiki pages for instructions.


# The Reconstruction Pipeline

The MVE reconstruction pipeline is composed of the following components:

* Creating a dataset, by converting input photos into the MVE File Format.
* Structure from Motion, which reconstructs the camera parameters.
* Multi-View Stereo, which reconstructs dense depth maps for each photo.
* Surface Reconstruction, which reconstructs a surface mesh.

The reconstruction tools can be found under `mve/apps/`. Please refer to the 
[MVE Users Guide](https://github.com/simonfuhrmann/mve/wiki/MVE-Users-Guide)
for a more detailed description how to use these tools. Note that UMVE is
merely an interface for scene inspection and does not support reconstuction.


# Licensing

Most of MVE is licensed under the BSD 3-Clause license. Some parts are
licensed using the GPL 3 license. See the source file headers or the
LICENSE.txt file for more details.

#Building on Windows

Building MVE on Windows is possible, but unsupported. There are a few issues when compiling with Visual Studio which have been patched in the "cmake" branch of Andre Schulz' fork of MVE (https://github.com/andre-schulz/mve.git). A list of patched issues follows:

Replace GNU make build system with CMake
Downgraded OpenMP 3.0+ code back to 2.0 because Visual Studio only supports OpenMP 2.0
Export MainWindowTab symbol for UMVE plugins
Requirements:

64-bit Windows
Visual Studio 2015 (64-bit) or newer
CMake 3.1 or newer
Build instructions:

Pull from https://github.com/andre-schulz/mve.git
Switch to the "cmake" branch (respectively "remotes/origin/cmake")
First, we will build the required 3rd party libraries:

Run cmake (configure + generate) in the "3rdparty" folder
Make sure that the build folder is the same as the source code folder
Open "3rdparty.sln"
Set the solution configuration to "Release"
Build the solution
Second, we will build MVE itself:

Run cmake (configure + generate) in "mve" folder
Open "MVE.sln"
Set your desired solution configuration (you'll most likely want "Release")
Build the solution
Build the CMake predefined target "PACKAGE"
This will create a .ZIP archive in the build folder named "MVE-0.1.1-win64.zip" which contains all binaries and their required libraries.

