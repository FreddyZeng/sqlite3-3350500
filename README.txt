sqlite3-3350500最新源码的原始项目编译，支持FTS5中文全文搜索。这是基于官方的autotool方便编译。
编译：./configure;make
安装：make install

参考此文集成https://blog.csdn.net/xiaogangwang2012/article/details/82979642。所以使用者需要在编译环境下安装好ICU4C就可以了
但是去掉了icucompat,因为发现FTS5的分词插件未使用icucompat，icucompat看起来是一些兼容性的函数。

推荐类似的项目https://github.com/wangfenjin/simple

------------------------------------------------------------------------------

This package contains:

 * the SQLite library amalgamation source code file: sqlite3.c
 * the sqlite3.h and sqlite3ext.h header files that define the C-language
   interface to the sqlite3.c library file
 * the shell.c file used to build the sqlite3 command-line shell program
 * autoconf/automake installation infrastucture for building on POSIX
   compliant systems
 * a Makefile.msc, sqlite3.rc, and Replace.cs for building with Microsoft
   Visual C++ on Windows

SUMMARY OF HOW TO BUILD
=======================

  Unix:      ./configure; make
  Windows:   nmake /f Makefile.msc

BUILDING ON POSIX
=================

The generic installation instructions for autoconf/automake are found
in the INSTALL file.

The following SQLite specific boolean options are supported:

  --enable-readline           use readline in shell tool   [default=yes]
  --enable-threadsafe         build a thread-safe library  [default=yes]
  --enable-dynamic-extensions support loadable extensions  [default=yes]

The default value for the CFLAGS variable (options passed to the C
compiler) includes debugging symbols in the build, resulting in larger
binaries than are necessary. Override it on the configure command
line like this:

  $ CFLAGS="-Os" ./configure

to produce a smaller installation footprint.

Other SQLite compilation parameters can also be set using CFLAGS. For
example:

  $ CFLAGS="-Os -DSQLITE_THREADSAFE=0" ./configure


BUILDING WITH MICROSOFT VISUAL C++
==================================

To compile for Windows using Microsoft Visual C++:

  $ nmake /f Makefile.msc

Using Microsoft Visual C++ 2005 (or later) is recommended.  Several Windows
platform variants may be built by adding additional macros to the NMAKE
command line.

Building for WinRT 8.0
----------------------

  FOR_WINRT=1

Using Microsoft Visual C++ 2012 (or later) is required.  When using the
above, something like the following macro will need to be added to the
NMAKE command line as well:

  "NSDKLIBPATH=%WindowsSdkDir%\..\8.0\lib\win8\um\x86"

Building for WinRT 8.1
----------------------

  FOR_WINRT=1

Using Microsoft Visual C++ 2013 (or later) is required.  When using the
above, something like the following macro will need to be added to the
NMAKE command line as well:

  "NSDKLIBPATH=%WindowsSdkDir%\..\8.1\lib\winv6.3\um\x86"

Building for UWP 10.0
---------------------

  FOR_WINRT=1 FOR_UWP=1

Using Microsoft Visual C++ 2015 (or later) is required.  When using the
above, something like the following macros will need to be added to the
NMAKE command line as well:

  "NSDKLIBPATH=%WindowsSdkDir%\..\10\lib\10.0.10586.0\um\x86"
  "PSDKLIBPATH=%WindowsSdkDir%\..\10\lib\10.0.10586.0\um\x86"
  "NUCRTLIBPATH=%UniversalCRTSdkDir%\..\10\lib\10.0.10586.0\ucrt\x86"

Building for the Windows 10 SDK
-------------------------------

  FOR_WIN10=1

Using Microsoft Visual C++ 2015 (or later) is required.  When using the
above, no other macros should be needed on the NMAKE command line.

Other preprocessor defines
--------------------------

Additionally, preprocessor defines may be specified by using the OPTS macro
on the NMAKE command line.  However, not all possible preprocessor defines
may be specified in this manner as some require the amalgamation to be built
with them enabled (see http://www.sqlite.org/compile.html). For example, the
following will work:

  "OPTS=-DSQLITE_ENABLE_STAT4=1 -DSQLITE_ENABLE_JSON1=1"

However, the following will not compile unless the amalgamation was built
with it enabled:

  "OPTS=-DSQLITE_ENABLE_UPDATE_DELETE_LIMIT=1"
