cmake_minimum_required(VERSION 2.8)
project(helloFoam)
add_executable(helloFoam helloFoam.C)

include_directories($ENV{FOAM_SRC}/finiteVolume/lnInclude)
include_directories($ENV{FOAM_SRC}/OpenFOAM/lnInclude)
include_directories($ENV{FOAM_SRC}/OSspecific/POSIX/lnInclude)

add_definitions(-D$ENV{WM_ARCH} -DWM_$ENV{WM_PRECISION_OPTION})
        
link_directories($ENV{FOAM_LIBBIN})
target_link_libraries(helloFoam 
    $ENV{FOAM_LIBBIN}/libfiniteVolume.so 
    $ENV{FOAM_LIBBIN}/libOpenFOAM.so)

install(TARGETS helloFoam 
        RUNTIME DESTINATION $ENV{FOAM_USER_APPBIN})
