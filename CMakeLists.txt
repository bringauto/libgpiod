cmake_minimum_required(VERSION 3.10)
project(libgpiod_autogen NONE)
file(MAKE_DIRECTORY ${CMAKE_BINARY_DIR}/autogen)
add_custom_target(autogen ALL
  WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/autogen
  COMMAND ${CMAKE_COMMAND} -E echo "Running autogen.sh..."
  COMMAND ${CMAKE_COMMAND} -E chdir ${CMAKE_BINARY_DIR}/autogen /bin/sh ${CMAKE_SOURCE_DIR}/autogen.sh --prefix=${CMAKE_INSTALL_PREFIX} --enable-bindings-cxx --enable-static=no --build=${CMAKE_SYSTEM_PROCESSOR} --host=x86_64-linux-gnu
  COMMAND ${CMAKE_COMMAND} -E chdir ${CMAKE_BINARY_DIR}/autogen make
  VERBATIM
)

install(CODE "execute_process(COMMAND ${CMAKE_COMMAND} -E chdir ${CMAKE_BINARY_DIR}/autogen make install)")
