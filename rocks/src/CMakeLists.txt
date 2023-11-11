# Add the executable
add_executable(rocks main.cpp)

set_target_properties(rocks PROPERTIES
  RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
)


# Find the required libraries
find_package(ZLIB REQUIRED)
find_package(BZip2 REQUIRED)

# Include directories for header files if there are any
include_directories(${PROJECT_SOURCE_DIR}/rocksdb/include)
include_directories(${ZLIB_INCLUDE_DIRS})
include_directories(${BZIP2_INCLUDE_DIR})

# Link the precompiled static library
add_library(rocksdb STATIC IMPORTED)
set_target_properties(rocksdb PROPERTIES IMPORTED_LOCATION ${PROJECT_SOURCE_DIR}/rocksdb/librocksdb.a)

# Link the static library to the executable
target_link_libraries(rocks rocksdb ${ZLIB_LIBRARIES} ${BZIP2_LIBRARIES})

