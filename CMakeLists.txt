cmake_minimum_required(VERSION 3.5)

project(HelloWorld)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Werror -std=c++14")
set(source_dir "${PROJECT_SOURCE_DIR}/src/")

# Use GLOB to gather all .cpp files in the src/ directory for compilation
file(GLOB source_files "${source_dir}/*.cpp")

# Create an executable from the source files
add_executable(HelloWorld ${source_files})

# Specify a directory inside the build directory for generated files
set(GENERATED_OUTPUT_DIR "${CMAKE_BINARY_DIR}/generated_files")

# Create this directory during the build
file(MAKE_DIRECTORY ${GENERATED_OUTPUT_DIR})

# Set output file to be placed in the generated_files folder inside the build directory
set(OUTPUT_FILE "${GENERATED_OUTPUT_DIR}/output.txt")

# Custom command 
add_custom_command(
    TARGET HelloWorld
    POST_BUILD
    COMMAND echo "Build successful" > ${OUTPUT_FILE}
    COMMENT "Generating output.txt in the build directory"
)
