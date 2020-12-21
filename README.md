Rindow CLBlast PHP extension
============================
CLBlast binding for PHP.

CLBlast is BLAS library on OpenCL. [Click here for details](https://github.com/CNugteren/CLBlast).

Rindow-CLBlast allows you to harness the power of your GPU with Rindow-Neural-Network-Library. Take full advantage of your machine and feel free to use machine learning on your cheap laptop.

Requirements
============

- PHP7.2 or PHP7.3 or PHP7.4
- [interop-phpobjects/polite-math](https://github.com/interop-phpobjects/polite-math) 1.0.2 or later
- [Rindow OpenCL](https://github.com/rindow/rindow-opencl)
- Windows 10
- OpenCL 1.2 drivers and libraries

You can use AMD GPU/APU Laptop computers drivers for windows10
(Probably Intel OpenCL drivers).

$ composer update
$ /path/to/php-devel-pack-7.x.x-Win32-VC15-x64/phpize.bat
$ configure --enable-rindow_clblast --with-prefix=/path/to/php-installation-path --with-opencl=/path/to/OpenCL-devel-directory --with-clblast=/path/to/CLBlast-sdk-directory --with-rindow_opencl=/path/to/Rindow-OpenCL-devel-directory

How to build from source code on Windows
========================================

### Install VC15
Developing PHP extensions from php7.2 to php7.4 requires VC15 instead of the latest VC.

- Install Microsoft Visual Studio 2019 or later installer
- Run Installer with vs2017 build tools option.

### php sdk and devel-pack binaries for windows

- You must know that PHP 7.2,7.3 and 7.4 needs environment for the MSVC version vc15 (that means Visual Studio 2017). php-sdk releases 2.1.9 supports vc15.
- Download https://github.com/microsoft/php-sdk-binary-tools/releases/tag/php-sdk-2.1.9
- Extract to c:\php-sdk
- Download target OpenCL headers from https://github.com/KhronosGroup/OpenCL-Headers
- Extract to /path/to/OpenCL/include
- Download target CLBlast sdk for Windows-x64 binary from https://github.com/CNugteren/CLBlast/releases
- Extract to /path/to/OpenCL/include
- Download target Rindow-OpenCL headers from https://github.com/rindow/rindow-opencl
- Extract to /path/to/Rindow-OpenCL

For execution
- Download Rindow-OpenBLAS binaries from https://github.com/rindow/rindow-openblas-binaries
- Download flang.dll binaries from https://github.com/rindow/rindow-openblas-binaries
- Extract and install to php extension and some directory

### Exports OpenCL binding library
C:\visual\studio\path>vcvars64 -vcvars_ver=14.16
C:\visual\studio\path>cd /path/to/OpenCL
C:\some-path\OpenCL>mkdir lib
C:\some-path\OpenCL>cd lib
C:\some-path\OpenCL\lib>dumpbin /exports C:\Windows\System32\OpenCL.dll > OpenCL.def
C:\some-path\OpenCL\lib>notepad OpenCL.def                     #### edit def file
EXPORTS

clBuildProgram
.....

C:\path\OpenCL\lib>lib /def:OpenCL.def /machine:x64

The OpenCL.lib file is created.

### Install and setup rindow_openblas for test

In order to execute rindow_opencl, you need a buffer object that implements the LinearBuffer interface. Please install rindow_openblas to run the tests.
See https://github.com/rindow/rindow-openblas/ for more information.

```shell
C:\tmp>copy rindow_openblas.dll /path/to/php-installation-path/ext
C:\tmp>echo extension=rindow_openblas.dll >> /path/to/php-installation-path/php.ini
C:\tmp>PATH %PATH%;/path/to/miniconda3-directory/Library/bin
```

### start php-sdk for target PHP version

Open Visual Studio Command Prompt for VS for the target PHP version(see stepbystepbuild.)
Note that you must explicitly specify the version of vc15 for which php.exe was built.
The -vcvars_ver=14.16 means vc15.

```shell
C:\visual\studio\path>vcvars64 -vcvars_ver=14.16

C:\tmp>cd c:\php-sdk
C:\php-sdk>phpsdk-vc15-x64.bat
```

### Build

```shell
$ PATH %PATH%;/path/to/miniconda3/bin;/path/to/CLBlast-devel-directory/lib
$ cd /path/to/here
$ composer update
$ /path/to/php-devel-pack-7.x.x-Win32-VC15-x64/phpize.bat
$ configure --enable-rindow_clblast --with-prefix=/path/to/php-installation-path --with-opencl=/path/to/OpenCL-devel-directory --with-clblast=/path/to/CLBlast-devel-directory --with-rindow_opencl=/path/to/Rindow-OpenCL-devel-directory
$ nmake clean
$ nmake
$ nmake test
```

How to build from source code on Linux
========================================
Need to be described ......  

$ sudo apt install clinfo
$ sudo apt-get install ocl-icd-opencl-dev
