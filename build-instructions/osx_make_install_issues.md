# Xrootd make install

After building the xrootd project with cmake, the installation process can be run, via the bash `make` command.

According to the osx-specific [build script](https://github.com/xrootd/xrootd/blob/master/.gitlab-ci.yml#L268-L279), one can `cd` into the source directory of the `xrd` client API and install the necessary files with the help of the recipe.

## Issue with the make process for `xrdcl` sources

[x] - fix issue

There is an issue with the [cmake install file](../../0xrootd_project/build/src/XrdCl/cmake_install.cmake) after the build process is finished.

* Inside the `build/` directory, the paths were missing quotes, which resulted in installing errors of the following form:

```text
-- Up-to-date: /Users/basavyr/Library/Mobile Documents/com~apple~CloudDocs/Work/Pipeline/DFCTI/CERN_project/0xrootd_project/tarball/xrootd/share/man/man1/xrdcp.1
-- Up-to-date: /Users/basavyr/Library/Mobile Documents/com~apple~CloudDocs/Work/Pipeline/DFCTI/CERN_project/0xrootd_project/tarball/xrootd/share/man/man1/xrdmapc.1
CMake Error at cmake_install.cmake:156 (EXECUTE_PROCESS):
  EXECUTE_PROCESS given unknown argument
  "Documents/com~apple~CloudDocs/Work/Pipeline/DFCTI/CERN_project/0xrootd_project/tarball/xrootd/share/man/man1".
```

Example in the cmake file:

```cmake
if("x${CMAKE_INSTALL_COMPONENT}x" STREQUAL "xUnspecifiedx" OR NOT CMAKE_INSTALL_COMPONENT)
  
    EXECUTE_PROCESS(
      COMMAND ln -sf xrdcp xrdcopy
      WORKING_DIRECTORY "$ENV{DESTDIR}//Users/basavyr/Library/Mobile Documents/com~apple~CloudDocs/Work/Pipeline/DFCTI/CERN_project/0xrootd_project/tarball/xrootd/bin ")    # <-------- the original file had no squiggles around the path
endif()
```

> Changing the path in the cmake file, for all the required files, fixes the issue and the make process finishes successfully .

## Issue with the make-process for `python-bindings`

When installing the python sources in the build directory, there is an issue with the python 2.7 header file, namely:

```bash
In file included from /System/Library/Frameworks/Python.framework/Versions/2.7/include/python2.7/Python.h:38:
/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/../include/c++/v1/string.h:60:15: fatal error:
      'string.h' file not found
#include_next <string.h>
              ^~~~~~~~~~
1 error generated.
error: command '/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/cc' failed with exit status 1
make[2]: *** [bindings/python/python_bindings] Error 1
make[1]: *** [bindings/python/CMakeFiles/python_target.dir/all] Error 2
make: *** [all] Error 2
```

The `string.h` header seems to be missing.

The CLANG compiler provided by Xcode does not work. Info about system's compiler:

```zsh
    …/code     master ●  /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/cc -v
Apple clang version 11.0.3 (clang-1103.0.32.59)
Target: x86_64-apple-darwin19.3.0
Thread model: posix
InstalledDir: /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin
    …/code     master ●  which clang                                                              13/05/20 | 18:36    11.40G 
/usr/bin/clang
    …/code     master ●  clang -v                                                                 13/05/20 | 18:36    11.41G 
Apple clang version 11.0.3 (clang-1103.0.32.59)
Target: x86_64-apple-darwin19.3.0
Thread model: posix
InstalledDir: /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin
```