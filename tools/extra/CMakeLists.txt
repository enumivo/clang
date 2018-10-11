add_subdirectory(enumivo_c_tool)
add_subdirectory(enumivo_ld_tool)
add_subdirectory(enumivo_abigen_tool)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/include/compiler_options.hpp.in ${CMAKE_BINARY_DIR}/compiler_options.hpp)
