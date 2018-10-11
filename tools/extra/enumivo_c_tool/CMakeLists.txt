set(LLVM_LINK_COMPONENTS support)

include_directories(include)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/enumivo-cc.cpp.in ${CMAKE_BINARY_DIR}/enumivo-cc.cpp)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/enumivo-cpp.cpp.in ${CMAKE_BINARY_DIR}/enumivo-cpp.cpp)

add_clang_executable(enumivo-cc ${CMAKE_BINARY_DIR}/enumivo-cc.cpp)
target_compile_options(enumivo-cc PRIVATE -fexceptions)
target_include_directories(enumivo-cc PUBLIC ${CMAKE_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/../include)
target_link_libraries(enumivo-cc PRIVATE
  clangTooling
  clangBasic
  clangASTMatchers)

add_clang_executable(enumivo-cpp ${CMAKE_BINARY_DIR}/enumivo-cpp.cpp)
target_compile_options(enumivo-cpp PRIVATE -fexceptions)
target_include_directories(enumivo-cpp PUBLIC ${CMAKE_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/../include)
target_link_libraries(enumivo-cpp PRIVATE
  clangTooling
  clangBasic
  clangASTMatchers)

install(FILES ${CMAKE_BINARY_DIR}/bin/enumivo-cpp DESTINATION ${CMAKE_INSTALL_BINDIR} PERMISSIONS OWNER_READ OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE)
install(FILES ${CMAKE_BINARY_DIR}/bin/enumivo-cc DESTINATION ${CMAKE_INSTALL_BINDIR} PERMISSIONS OWNER_READ OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE)
