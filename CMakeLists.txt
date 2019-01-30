cmake_minimum_required(VERSION 3.0)

project(vmlib)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_BUILD_TYPE Debug)


set(VM_SOURCE   vm.hpp
                vm.cpp
                src/instruction.hpp
                src/opcode.hpp
                src/chunk.hpp
                src/value.hpp
                src/object.hpp
                src/instruction.cpp
                src/chunk.cpp
                src/value.cpp
                src/opcode.cpp
                src/object.cpp)

add_library(vmlib STATIC ${VM_SOURCE})

set_target_properties(vmlib PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/lib"
)

install(TARGETS vmlib ARCHIVE DESTINATION "${PROJECT_SOURCE_DIR}/lib" COMPONENT VMLIB )
export ( TARGETS vmlib FILE vmlib-config.cmake)

link_directories("${PROJECT_SOURCE_DIR}/lib")

add_executable(vm-test main.cpp)

TARGET_LINK_LIBRARIES(vm-test vmlib)
