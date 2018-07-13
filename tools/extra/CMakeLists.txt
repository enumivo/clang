set(ENUMIVO_VER_MAJOR "1")
set(ENUMIVO_VER_MINOR "0")
set(ENUMIVO_VER_REVISION "0")

add_subdirectory(enumivo_c_tool)
add_subdirectory(enumivo_ld_tool)

set(ENUMIVO_STACK_SIZE "8192")

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/compiler_options.hpp.in ${CMAKE_BINARY_DIR}/compiler_options.hpp)


