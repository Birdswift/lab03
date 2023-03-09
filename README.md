# lab03
Лабораторная работа №3

Задание 1

1)С помощью sudo apt install cmake скачиваю необходимые инструменты

2)Создаю директорию mkdir formatter_lib

3)Перехожу в директорию cd formatter_lib

4)Создаю папку mkdir b

5)Перехожу в папку cd b

6)В папку скачиваю программы с гитхаб в "сыром" виде

wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_lib/formatter.h

wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_lib/formatter.cpp

7) Перехожу в formatter_lib, создаю там папку prep

cd ..

mkdir prep 

8)Далее необходимо проверить версию CMake cmake --verison

9)Также проверяю путь до g++ which g++

10)Открываю редактор nano CMakeLists.txt

11)В нем прописываю следующие строчки

cmake_minimum_required(VERSION 3.22.1) - объявляю версию cmake

set(CMAKE_CXX_COMPILER "/usr/bin/g++") - объявляю версию компилятора и путь до него

project(Formatter) - даю название проекту

set(Formation ~/formatter_lib/b/formatter.cpp ~/formatter_lib/b/formatter.h) - прокладываю путь до файлов

add_library(mylib STATIC ${Formation}) - компилирую файлы в необходимую мне директорию

12) Перехожу в cd prep 

Компилирую сюда файлы cmake .. ("..") - сдвиг вниз по папке

cmake --build . - из данной папки

Задание 2

1)Создаю директорию mkdir formatter_ex_lib

2)Перехожу в директорию cd formatter_ex_lib

3)Создаю папку mkdir bcd

4)Перехожу в папку cd b

5)В папку скачиваю программы с гитхаб в "сыром" виде

wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_lib/formatter_ex.h

wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_lib/formatter_ex.cpp

6) Перехожу в formatter_ex_lib, создаю там папку prep

cd .. 

mkdir prep 

7)Открываю редактор nano CMakeLists.txt

Пишу в него следующее 

cmake_minimum_required(VERSION 3.22.1) 

set(CMAKE_CXX_COMPILER "/usr/bin/g++") 

project(formatter_ex_lib VERSION 0.0.1) 

set(Formation_ex ~/formatter_ex_lib/b/formatter_ex.cpp) 

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib formatter_lib_dir) 

add_library(formatter_ex_lib STATIC ${Formation_ex}) 

target_include_directories(formatter_ex_lib PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib/b)

target_link_libraries(formatter_ex_lib formatter_lib)

8) Перехожу в cd prep 

Компилирую сюда файлы cmake .. ("..") - сдвиг вниз по папке

cmake --build . - из данной папки

Задание 3

Для hello_world

1) Создал mkdir hw

cd hw

2) Создал mkdir build

cd build

3) Скачал wget  https://raw.githubusercontent.com/tp-labs/lab03/master/hello_world_application/hello_world.cpp

4)Спустился на одну вниз cd .. 

5)Создал и отредактировал nano CMakeLists.txt

cmake_minimum_required(VERSION 3.22.1 FATAL_ERROR)

set(CMAKE_CXX_COMPILER "/usr/bin/g++")

project(hello_world VERSION 0.0.1)

include_directories("~/formatter_lib/b")

include_directories("~/formatter_ex_lib/b")

add_library(formatter_lib STATIC "~/formatter_lib/b/formatter.cpp")

add_library(formatter_ex_lib STATIC "~/formatter_ex_lib/b/formatter_ex.cpp")

add_executable(hello_exec "~/hw/build/hello_world.cpp")

target_link_libraries(hello_exec formatter_lib formatter_ex_lib) - линкую библиотеки

6)Закрываю редактор, перехожу в папку cd build, cmake .., cmake -- .

для solver

1)mkdir solver_lib

2)cd solver_lib

3)mkdir build

4)cd build

5)wget https://raw.githubusercontent.com/tp-labs/lab03/blob/master/solver_lib/solver.cpp

wget https://raw.githubusercontent.com/tp-labs/lab03/blob/master/solver_lib/solver.h

wget https://raw.githubusercontent.com/tp-labs/lab03/blob/master/solver_application/equation.cpp

6)cd ..

7)nano CMakeLists.txt 
                           
cmake_minimum_required(VERSION 3.22.1)

set(CMAKE_CXX_COMPILER "/usr/bin/g++")

project(solver VERSION 0.0.1)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib formatter_ex_lib_dir)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib solver_lib_dir)

add_executable(solver "~/solver_lib/build/equation.cpp")

target_include_directories(solver PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib/build ${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib/build)

target_link_libraries(solver formatter_ex_lib solver_lib)

 8) cd build
 
 9) cmake ..
 
 10) cmake --build .

