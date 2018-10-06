# Divisor: CMake C++ Project Template

Thank you for your interest in this project!

Are you just starting with `CMake` or C++? 

Do you need some easy-to-use starting point, but one that has the basic moving parts you are likely going to need on any medium sized project?

Do you believe in test-driven development, or at the very lest — write your tests *together* with the feature code? If so you'd want to start your project pre-integrated with a good testing framework.

Divisor is a minimal project and when built it produces:

 * **A command line binary `divisor`** that computes modulo of its argument over 2, or the third argument.
 * **An executable unit test**  using [Google Test library](https://github.com/google/googletest)
 
## Usage

### Prerequisites

You need:

 * C++ compiler
 * CMake 3.2+ installed (on a Mac, run `brew install cmake`)
 * If you prefer to code in a great IDE, I highly recommend [Jetbrains CLion](https://www.jetbrains.com/clion/). It is fully compatible with this project.

### Building on the Command Line

Follow the steps:

```bash
$ cd ${insert your workspace folder here}
$ git clone https://github.com/kigster/cmake-project-template 
$ cd cmake-project-template
``` 

Now we should be in the project's top level folder. First step is to remove (any possible existing) and re-create the 'build' folder


```bash
$ rm -rf build && mkdir build
$ cd build
$ cmake ..
$ make && make install
```

### Building in CLion

Before starting CLion, I recommend removing any previous `build` folder with `rm -rf build`.

Next, start CLion, and open the project's top level folder. CLion should automatically detect the project and run CMake file, which generates (git-ignored) Makefiles — the regular old-school C Makefiles.

Select menu option **Run ➜ Build**, and then **Run ➜ Install**.

Hopefully you get no errors, and the project builds.


### Example Project — "Divis"

For simplicity's sake  we'll build a simple command line tool that for every input number prints out if it's libdivision by two. Having said that, the denominator can also be supplied as an argument.

We'll call this tool **libdivision**, and that name will now be our project's name too.

Our goal is to have a working binary, such as :

```bash
$ bin/divis value [ denominator ]

❯ src/divis 34 6
Number 34 modulo 6 is = 4

❯ src/divis 10 454
Number 10 modulo 454 is = 10
```

And C++ usage:

```C++
#include <iostream>
#include <divisible>

std::cout << Divisible.new(int denominator).modulo();

```

Sources:

 * `src/*` — C++ code that ultimately compiles into a library
 * We'll also build a library `libdivisible.a` and install into `lib/`
 * `src/CLI.cpp` C++ CLI interface parser that parses arguments and flags passed to a binary
 * a tiny `src/main.cpp` that calls into the CLI, which then calls the library.
 
Tests: 

 * A `test` folder with the automated tests and fixtures that mimics the directory structure of `src`.
 * For every C++ file in `src/A/B/<name>.cpp` there is a corresponding test file `test/A/B/<name>_test.cpp`
 * Tests compile into a single binary `test/bin/runner` that is run on a command line to run the tests.
 * `test/lib` folder with a git submodule in `test/lib/googletest`, and possibly other libraries.
 
 
Here is the structure proposed here:
 

```
divisible/ 
   CMakeLists.txt       -> Top level CMake file
   bin/                 -> exported compiled executables
   doc/                 -> and compiled documentation
       usage/           -> documentation folder for how to use the tool
       design/          -> documentation folder for the developers of the tool
   include/             -> externally exported header files
       name/
   lib/                 -> compiled library we are exporting
       extern/          -> external libraries if they must be included
      
   src/                 -> sources of the project
       CLI.cpp          -> the CLI argument parser/wrapper
       main.cpp         -> small main.cpp that calls into the CLI module
       divisible/       -> cmake project that produces divisible library
          CMakeLists.txt
          Divisible.cpp
          Divisible.h
   test/                -> sources for all the tests
       bin/             -> where the binary `test-runner` is installed
       lib/             -> where any external libraries live
           googletest/ -> most importantly, our googletest library as a submodule
       src/
   util/                -> any bash tools, build wrappers, etc.
```


 
## Development

TBD. 

#### Contributing

Bug reports and pull requests are welcome on GitHub at [https://github.com/kigster/cmake-project-template](https://github.com/kigster/cmake-project-template)

### License

**CMake Project Template** is &copy; 2017 Konstantin Gredeskoul, available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT). 

### Acknowledgements

 sThis project is a derivative of the [CMake Tutorial](https://cmake.org/cmake-tutorial/), and is aimed at saving time for starting new projects in C++ that use CMake and GoogleTest.

