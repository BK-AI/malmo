## Windows: Installing Pre-requisite software ##

This is software that Project Malmo needs to work, some of it is required for software compiling later in this document.

###  1. Install CMake:

  * Download and run e.g. `cmake-3.5.0-win32-x86.msi` from https://cmake.org/download/
  * If you are new to CMake, see [some notes](cmake_readme.md) [(doc link)](@ref md_doc_cmake_readme).

###  2. Install FFMPEG: 
  * Download [64-bit Static](http://ffmpeg.zeranoe.com/builds/win64/static/ffmpeg-latest-win64-static.7z) from [Zeranoe](http://ffmpeg.zeranoe.com/builds/).
  * Unpack the contents of the zip (bin folder etc.) to `C:\ffmpeg`
  * Add `C:\ffmpeg\bin` to your `PATH` ([PATH: How To](https://support.microsoft.com/en-us/kb/310519))
  * Check that typing `ffmpeg` at a command prompt works.

###  3. Install git
  * Get the latest Windows git from https://git-scm.com/downloads
  * Check that git is in your path.  

###  4. Install Visual Studio
  * Download and install Visual Studio 2015 community edition (this is the equivalent of VS2015 Professional) from http://visualstudio.com
#### Note: VS2015 does not install C++ by default, it is now an 'Optional' language, you need to actively select it in the options section of the installer.

### 5. Install the Java SE Development Kit (JDK) ###

  * Visit http://www.oracle.com/technetwork/java/javase/downloads/index.html and download the latest 64-bit version 
e.g. `jdk-8u101-windows-x64.exe`

  * Run the downloaded file to install the JDK. Make a note of the install location.

  * Add the bin folder (e.g. `C:\Program Files\Java\jdk1.8.0_101\bin` ) to your PATH ([How To](https://support.microsoft.com/en-us/kb/310519))

  * Set the JAVA_HOME environment variable to be the location of the JDK:

  * Open the Control Panel: e.g. in Windows 10: right-click on `This PC` in File Explorer and select `Properties`
  * Navigate to: Control Panel > System and Security > System
  * Select `Advanced system settings` on the left
  * Select `Environment variables...`
  * Under `User variables` select `New...`
  * Enter `JAVA_HOME` as the varible name
  * Enter e.g. `C:\Program Files\Java\jdk1.8.0_101` as the variable value. Replace this with the location of your  
    JDK installation.
  
#### Check that `java -version` and `javac -version` and `set JAVA_HOME` all report the same 64-bit version.
 
### 6. Install python

  * Download and install python 2.7.x [Python 2.7 (64-bit)](https://www.python.org/ftp/python/2.7.12/python-2.7.12.amd64.msi)

### 7. Download and install Doxygen
  * Download e.g. `doxygen-1.8.11-setup.exe` from http://www.stack.nl/~dimitri/doxygen/download.html
  * Run the exe to install.

### 8. Install SWIG
  * Browse to http://swig.org/download.html and download the latest version of `swigwin`.
  * Unzip the directory and copy it to your `C:\` drive.
  * Add (e.g.) `C:\swigwin-3.0.10` to your PATH. CMake should then find swig automatically.
    
### 9. Install CodeSynthesis XSD 
  * Download from: http://www.codesynthesis.com/products/xsd/download.xhtml
  * to its default location `C:\Program Files (x86)\CodeSynthesis XSD 4.0\`
  *  You don't need to set up the VS search paths.
    
### 10. Install xsltproc
 
  * Visit ftp://ftp.zlatkovic.com/libxml/ and download libxslt, libxml2, zlib and iconv:
    * Download e.g. `libxslt-1.1.26.win32.zip` and extract to `C:\XSLT`
    * Download e.g. `libxml2-2.7.8.win32.zip` and extract to `C:\XSLT`
    * Download e.g. `zlib-1.2.5.win32.zip` and extract to `C:\XSLT`
    * Download e.g. `iconv-1.9.2.win32.zip` and extract to `C:\XSLT`
  * Add their `bin` folders to your PATH: ([How To](https://support.microsoft.com/en-us/kb/310519))
    * Add `C:\XSLT\libxslt-1.1.26.win32\bin` to your PATH.
    * Add `C:\XSLT\libxml2-2.7.8.win32\bin` to your PATH.
    * Add `C:\XSLT\iconv-1.9.2.win32\bin` to your PATH.
  * Copy `C:\XSLT\zlib-1.2.5\bin\zlib1.dll` to `C:\XSLT\libxslt-1.1.26.win32\bin`
  * Check that running `xsltproc` from a new command prompt works, printing the options.

## Building and compiling


### 1. Download and install ZLib 



  * Download e.g. `zlib-1.2.8.zip` from http://zlib.net/
  * Extract to `C:\zlib-1.2.8\`
  * Open a Visual Studio 2013 x64 command prompt with Admin rights ([How-To](https://technet.microsoft.com/en-us/library/cc947813(v=ws.10).aspx))
  * `cd C:\zlib-1.2.8\`
  * `mkdir build`
  * `cd build`
  * `cmake -G "Visual Studio 14 2015 Win64" ..`
  * `cmake --build . --config Debug --target install`
  * `cmake --build . --config Release --target install`
  * Add `C:\Program Files\zlib\bin` to your PATH ([How To](https://support.microsoft.com/en-us/kb/310519))

###6. Install and build Boost 1.59.0 or later: 
####(NOTE - if you have Python31 installed, ensure that it isn't picked up by the boost build - make sure it comes _after_ Python27 in your path)
  * Download e.g. `boost_1_59_0.zip` from http://boost.org
  * Extract to `c:\boost`
  * Open a Visual Studio 2013 x64 command prompt with Admin rights ([How-To](https://technet.microsoft.com/en-us/library/cc947813(v=ws.10).aspx))
  * e.g. `cd c:\boost\boost_1_59_0`
  * `bootstrap.bat`
  * `b2.exe toolset=msvc-14.0 address-model=64 -sZLIB_SOURCE="C:\zlib-1.2.8" -j%NUMBER_OF_PROCESSORS%`
  * For more information on installing Boost with ZLib support, see [here](http://www.boost.org/doc/libs/1_59_0/libs/iostreams/doc/installation.html)

## Build Malmo:

  * Open The Visual Studio 2015 x64 MSbuild command prompt in administrator mode

    1. `mkdir MalmoPlatform` (wherever you want)
    2. `cd MalmoPlatform`
    3. `git clone https://github.com/Microsoft/malmo.git .`
    4. Save xs3p.xsl from https://raw.githubusercontent.com/bitfehler/xs3p/1b71310dd1e8b9e4087cf6120856c5f701bd336b/xs3p.xsl to the Schemas folder.
    5. Add a new environment variable `MALMO_XSD_PATH` and set it to the path to `MalmoPlatform\Schemas`. You will need to open a fresh command prompt for this to take effect.
    6. `mkdir build`
    7. `cd build`
    8. `cmake -G "Visual Studio 14 2015 Win64" ..`
    9. If it fails to find things, use `cmake-gui ..` and give hints, as described above.  
       * #### If you have cygwin installed, check that cmake isn't using the cygwin python and lua executables.
    10. For a Debug build: `msbuild INSTALL.vcxproj`  
    11.  For a Release build: `msbuild INSTALL.vcxproj /p:Configuration=Release`
 
## Test Malmo:
  * After building Debug: `ctest -C Debug`
  * After building Release: `ctest -C Release`
  * Add `-E Integration` to exclude the integration tests.
  * Add `-R <test>` where <test> is everything after test_ eg PythonIntegrationTests_MazeRunner becomes `-R Mazerunner` 
  * Add `-VV` to get verbose output (Two V's not one W), Combine with the above to get detailed debug output on failed individual tests
  * Or build the RUN_TESTS project in Visual Studio and look in the Output tab

## Make a distributable:

Once all the tests are complete you can build the distributable version you will use for working with malmo


  * (Optional unless actually distributing.) Change the version number in CMakeLists.txt and Minecraft/src/main/java/com/microsoft/Malmo/MalmoMod.java, and commit.
  * `msbuild PACKAGE.vcxproj /p:Configuration=<target>` <target is either Release or Debug currently malmo only works with one or the other, if you need both you need dual distributions
####Note that building the package overwrites previous package




