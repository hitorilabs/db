# Add the executable
add_executable(rocks main.cpp)

set_target_properties(rocks PROPERTIES
  RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
)

# Find the required libraries
find_package(ZLIB REQUIRED)
find_package(BZip2 REQUIRED)

find_library(ZSTD_LIBRARIES NAMES zstd PATHS /lib/x86_64-linux-gnu)
find_library(LZ4_LIBRARIES NAMES lz4 PATHS /lib/x86_64-linux-gnu)
find_library(SNAPPY_LIBRARIES NAMES snappy PATHS /lib/x86_64-linux-gnu)

# Include directories for header files
target_include_directories(rocks PRIVATE
    ${PROJECT_SOURCE_DIR}/rocksdb/include
)

# Link the precompiled static library
add_library(rocksdb STATIC IMPORTED)
set_target_properties(rocksdb PROPERTIES IMPORTED_LOCATION ${PROJECT_SOURCE_DIR}/rocksdb/librocksdb.a)

# Link the static library to the executable
target_link_libraries(rocks
    rocksdb
    ${ZLIB_LIBRARIES}
    ${BZIP2_LIBRARIES}
    ${ZSTD_LIBRARIES}
    ${LZ4_LIBRARIES}
    ${SNAPPY_LIBRARIES}
)

