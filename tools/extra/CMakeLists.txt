add_subdirectory(enumivo_c_tool)
add_subdirectory(enumivo_ld_tool)
add_subdirectory(enumivo_abigen_tool)

if ("${Boost_INCLUDE_DIRS}" STREQUAL "")
   set(Boost_INCLUDE_DIRS "${BOOST_ROOT}/include")
endif()

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/include/compiler_options.hpp.in ${CMAKE_BINARY_DIR}/compiler_options.hpp)
