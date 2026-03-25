## Homework

Представьте, что вы стажер в компании "Formatter Inc.".
### Задание 1
Вам поручили перейти на систему автоматизированной сборки **CMake**.
Исходные файлы находятся в директории [formatter_lib](formatter_lib).
В этой директории находятся файлы для статической библиотеки *formatter*.
Создайте `CMakeList.txt` в директории [formatter_lib](formatter_lib),
с помощью которого можно будет собирать статическую библиотеку *formatter*.
```
$ git clone https://github.com/tp-labs/lab03
Cloning into 'lab03'...
remote: Enumerating objects: 91, done.
remote: Counting objects: 100% (30/30), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 91 (delta 23), reused 21 (delta 21), pack-reused 61 (from 1)
Receiving objects: 100% (91/91), 1.02 MiB | 754.00 KiB/s, done.
Resolving deltas: 100% (41/41), done.
$ git remote rm origin
$ git remote add orogin https://github.com/MatveyZK/lab03
$ rm LICENSE README.md CMakeLists.txt 
$ cd formatter_lib
$ nano CMakeLists.txt 
$ cat CMakeLists.txt 
cmake_minimum_required(VERSION 3.11)
project(formatter)

add_library(formatter STATIC formatter.cpp)
$ cmake -S . -B build
-- The C compiler identification is GNU 14.2.0
-- The CXX compiler identification is GNU 14.2.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (0.6s)
-- Generating done (0.0s)
-- Build files have been written to: /home/matvey/Desktop/lab03/formatter_lib/build
$ cmake --build build
[ 50%] Building CXX object CMakeFiles/formatter.dir/formatter.cpp.o
[100%] Linking CXX static library libformatter.a
[100%] Built target formatter
$ cd build/
$ ls
CMakeCache.txt  CMakeFiles  cmake_install.cmake  libformatter.a  Makefile
```

### Задание 2
У компании "Formatter Inc." есть перспективная библиотека,
которая является расширением предыдущей библиотеки. Т.к. вы уже овладели
навыком созданием `CMakeList.txt` для статической библиотеки *formatter*, ваш 
руководитель поручает заняться созданием `CMakeList.txt` для библиотеки 
*formatter_ex*, которая в свою очередь использует библиотеку *formatter*.
```
$ cd ..
$ cd ..
$ cd formatter_ex_lib/
$ nano CMakeLists.txt 
$ cat CMakeLists.txt 
cmake_minimum_required(VERSION 3.11)
project(formatter_ex)

add_library(formatter STATIC ../formatter_lib/formatter.cpp)
target_include_directories(formatter PUBLIC ../formatter_lib)
add_library(formatter_ex STATIC formatter_ex.cpp)
target_link_libraries(formatter_ex PUBLIC formatter)
$ cmake -S . -B build
-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/matvey/Desktop/lab03/formatter_ex_lib/build
$ cmake --build build
[ 25%] Building CXX object CMakeFiles/formatter.dir/home/matvey/Desktop/lab03/formatter_lib/formatter.cpp.o
[ 50%] Linking CXX static library libformatter.a
[ 50%] Built target formatter
[ 75%] Building CXX object CMakeFiles/formatter_ex.dir/formatter_ex.cpp.o
[100%] Linking CXX static library libformatter_ex.a
[100%] Built target formatter_ex
$ cd build/
$ ls
CMakeCache.txt  CMakeFiles  cmake_install.cmake  libformatter.a  libformatter_ex.a  Makefile
```
### Задание 3
Конечно же ваша компания предоставляет примеры использования своих библиотек.
Чтобы продемонстрировать как работать с библиотекой *formatter_ex*,
вам необходимо создать два `CMakeList.txt` для двух простых приложений:
* *hello_world*, которое использует библиотеку *formatter_ex*;
* *solver*, приложение которое испольует статические библиотеки *formatter_ex* и *solver_lib*.

**Удачной стажировки!**
```
$ cd ../..
$ cd hello_world_application/
$ nano CMakeLists.txt 
$ cat CMakeLists.txt 
cmake_minimum_required(VERSION 3.11)
project(hello_world)

add_library(formatter STATIC ../formatter_lib/formatter.cpp)
target_include_directories(formatter PUBLIC ../formatter_lib)
add_library(formatter_ex STATIC ../formatter_ex_lib/formatter_ex.cpp)
target_include_directories(formatter_ex PUBLIC ../formatter_ex_lib)
target_link_libraries(formatter_ex formatter)
add_executable(hello_world hello_world.cpp)
target_include_directories(hello_world PUBLIC ../formatter_ex_lib)
target_link_libraries(hello_world formatter_ex)
$ cmake -S . -B build
-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/matvey/Desktop/lab03/hello_world_application/build
$ cmake --build build
[ 33%] Built target formatter
[ 66%] Built target formatter_ex
[ 83%] Linking CXX executable hello_world
[100%] Built target hello_world
$ cd build/
$ ./hello_world
-------------------------
hello, world!
-------------------------
```
```
$ cd ../..
$ cd solver_application/
$ nano CMakeLists.txt
$ cat CMakeLists.txt 
cmake_minimum_required(VERSION 3.11)
project(solver)

add_library(formatter STATIC ../formatter_lib/formatter.cpp)
target_include_directories(formatter PUBLIC ../formatter_lib)
add_library(formatter_ex STATIC ../formatter_ex_lib/formatter_ex.cpp)
target_include_directories(formatter_ex PUBLIC ../formatter_ex_lib)
target_link_libraries(formatter_ex formatter)
add_library(solver STATIC ../solver_lib/solver.cpp)
target_include_directories(solver PUBLIC ../solver_lib)
add_executable(equation equation.cpp)
target_include_directories(equation PUBLIC ../solver_lib)
target_link_libraries(equation solver formatter_ex)
$ cmake -S . -B build
-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/matvey/Desktop/lab03/solver_application/build
$ cmake --build build
[ 12%] Building CXX object CMakeFiles/formatter.dir/home/matvey/Desktop/lab03/formatter_lib/formatter.cpp.o
[ 25%] Linking CXX static library libformatter.a
[ 25%] Built target formatter
[ 37%] Building CXX object CMakeFiles/formatter_ex.dir/home/matvey/Desktop/lab03/formatter_ex_lib/formatter_ex.cpp.o
[ 50%] Linking CXX static library libformatter_ex.a
[ 50%] Built target formatter_ex
[ 62%] Building CXX object CMakeFiles/solver.dir/home/matvey/Desktop/lab03/solver_lib/solver.cpp.o
/home/matvey/Desktop/lab03/solver_lib/solver.cpp: In function ‘void solve(float, float, float, float&, float&)’:
/home/matvey/Desktop/lab03/solver_lib/solver.cpp:14:21: error: ‘sqrtf’ is not a member of ‘std’; did you mean ‘strtof’?
   14 |     x1 = (-b - std::sqrtf(d)) / (2 * a);
      |                     ^~~~~
      |                     strtof
/home/matvey/Desktop/lab03/solver_lib/solver.cpp:15:21: error: ‘sqrtf’ is not a member of ‘std’; did you mean ‘strtof’?
   15 |     x2 = (-b + std::sqrtf(d)) / (2 * a);
      |                     ^~~~~
      |                     strtof
gmake[2]: *** [CMakeFiles/solver.dir/build.make:79: CMakeFiles/solver.dir/home/matvey/Desktop/lab03/solver_lib/solver.cpp.o] Error 1
gmake[1]: *** [CMakeFiles/Makefile2:160: CMakeFiles/solver.dir/all] Error 2
gmake: *** [Makefile:91: all] Error 2
$ nano ../solver_lib/solver.cpp
$ cat ../solver_lib/solver.cpp
#include "solver.h"

#include <stdexcept>
#include <math.h>

void solve(float a, float b, float c, float& x1, float& x2)
{
    float d = (b * b) - (4 * a * c);

    if (d < 0)
    {
        throw std::logic_error{"error: discriminant < 0"};
    }

    x1 = (-b - std::sqrtf(d)) / (2 * a);
    x2 = (-b + std::sqrtf(d)) / (2 * a);
}
$ cmake -S . -B build
-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/matvey/Desktop/lab03/solver_application/build
$ cmake --build build
[ 25%] Built target formatter
[ 50%] Built target formatter_ex
[ 75%] Built target solver
[ 87%] Building CXX object CMakeFiles/equation.dir/equation.cpp.o
[100%] Linking CXX executable equation
[100%] Built target equation
$ cd build/
$ ./equation 
1
2
3 
-------------------------
error: discriminant < 0
-------------------------
```
