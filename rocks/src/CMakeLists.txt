# Add the executable
add_executable(rocks main.cpp)

set_target_properties(rocks PROPERTIES
  RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
)

# Find the required libraries
find_package(ZLIB REQUIRED)
find_package(BZip2 REQUIRED)

find_library(ZSTD_LIBRARY NAMES zstd PATHS /lib/x86_64-linux-gnu)
find_library(LZ4_LIBRARY NAMES lz4 PATHS /lib/x86_64-linux-gnu)
find_library(SNAPPY_LIBRARY NAMES snappy PATHS /lib/x86_64-linux-gnu)

# Include directories for header files
target_include_directories(rocks PRIVATE
    ${PROJECT_SOURCE_DIR}/rocksdb/include
    ${ZLIB_INCLUDE_DIRS}
    ${BZIP2_INCLUDE_DIR}
)

# Link the precompiled static library
add_library(rocksdb STATIC IMPORTED)
set_target_properties(rocksdb PROPERTIES IMPORTED_LOCATION ${PROJECT_SOURCE_DIR}/rocksdb/librocksdb.a)

# Link the static library to the executable
target_link_libraries(rocks
    rocksdb
    ${ZLIB_LIBRARIES}
    ${BZIP2_LIBRARIES}
    ${ZSTD_LIBRARY}
    ${LZ4_LIBRARY}
    ${SNAPPY_LIBRARY}
)

