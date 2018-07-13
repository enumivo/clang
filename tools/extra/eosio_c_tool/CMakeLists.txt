set(LLVM_LINK_COMPONENTS support)

set(Boost_USE_STATIC_LIBS ON)
find_package(Boost 1.67.0 REQUIRED system filesystem)
if(Boost_FOUND)
   include_directories (SYSTEM ${Boost_INCLUDE_DIR})
endif()

include_directories(include)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/enumivo-cc.cpp.in ${CMAKE_BINARY_DIR}/enumivo-cc.cpp)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/enumivo-cpp.cpp.in ${CMAKE_BINARY_DIR}/enumivo-cpp.cpp)

add_clang_executable(enumivo-cc ${CMAKE_BINARY_DIR}/enumivo-cc.cpp ${CMAKE_CURRENT_SOURCE_DIR}/../whereami.cpp)
target_compile_options(enumivo-cc PRIVATE -fexceptions)
target_include_directories(enumivo-cc PUBLIC ${Boost_INCLUDE_DIR} ${CMAKE_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/../enumivo_tool_include ${CMAKE_CURRENT_SOURCE_DIR}/../)
target_link_libraries(enumivo-cc PRIVATE
  clangTooling
  clangBasic
  clangASTMatchers
  ${Boost_LIBRARIES})

add_clang_executable(enumivo-cpp ${CMAKE_BINARY_DIR}/enumivo-cpp.cpp ${CMAKE_CURRENT_SOURCE_DIR}/../whereami.cpp)
target_compile_options(enumivo-cpp PRIVATE -fexceptions)
target_include_directories(enumivo-cpp PUBLIC ${Boost_INCLUDE_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/../enumivo_tool_include ${CMAKE_CURRENT_SOURCE_DIR}/../ ${CMAKE_BINARY_DIR})
target_link_libraries(enumivo-cpp PRIVATE
  clangTooling
  clangBasic
  clangASTMatchers
  ${Boost_LIBRARIES})

install(FILES ${CMAKE_BINARY_DIR}/bin/enumivo-cpp DESTINATION ${CMAKE_INSTALL_BINDIR} PERMISSIONS OWNER_READ OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE)
install(FILES ${CMAKE_BINARY_DIR}/bin/enumivo-cc DESTINATION ${CMAKE_INSTALL_BINDIR} PERMISSIONS OWNER_READ OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE)
