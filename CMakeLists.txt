cmake_minimum_required(VERSION 3.15)
# Project name reflects the CLI/tool name "veraser"
project(veraser C)

# Build a single-binary CLI from the single implementation file.
# The core library code and the CLI live in the same C file under VE_BUILD_CLI.
add_executable(veraser veraser.c)

# Enable the CLI entrypoint (main) guarded by VE_BUILD_CLI in the source.
target_compile_definitions(veraser PRIVATE VE_BUILD_CLI)

# On Windows, link against bcrypt for CNG RNG/AES APIs used by the implementation.
if (WIN32)
  target_link_libraries(veraser bcrypt)
endif()