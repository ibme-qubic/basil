cmake_minimum_required(VERSION 2.7)

# Extract GIT revision for versioning
execute_process(COMMAND
  git describe --dirty
  WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
  OUTPUT_VARIABLE GIT_SHA1
  ERROR_QUIET OUTPUT_STRIP_TRAILING_WHITESPACE)

execute_process(COMMAND
  git log -1 --format=%ad --date=local
  WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
  OUTPUT_VARIABLE GIT_DATE
  ERROR_QUIET OUTPUT_STRIP_TRAILING_WHITESPACE)

configure_file(basil.in basil @ONLY)
configure_file(basil_var.in basil_var @ONLY)
INSTALL(PROGRAMS ${CMAKE_CURRENT_BINARY_DIR}/basil ${CMAKE_CURRENT_BINARY_DIR}/basil_var DESTINATION bin)

