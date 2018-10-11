set(LLVM_LINK_COMPONENTS support)

include_directories(include)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/enumivo-ld.cpp.in ${CMAKE_BINARY_DIR}/enumivo-ld.cpp)

add_clang_executable(enumivo-ld ${CMAKE_BINARY_DIR}/enumivo-ld.cpp)
target_compile_options(enumivo-ld PRIVATE -fexceptions)
target_include_directories(enumivo-ld PUBLIC ${CMAKE_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/../include)
target_link_libraries(enumivo-ld PRIVATE
  clangTooling
  clangBasic
  clangASTMatchers)

install(FILES ${CMAKE_BINARY_DIR}/bin/enumivo-ld DESTINATION ${CMAKE_INSTALL_BINDIR} PERMISSIONS OWNER_READ OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE)

