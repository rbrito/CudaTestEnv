cmake_minimum_required(VERSION 2.6)

project(hetero)

# FLAGS for the compiler
set(CMAKE_CXX_FLAGS "-Os -Wall -Wextra -DCUDA_EMU")

# Specify what we need to use
set(Boost_USE_MULTITHREADED ON)
find_package(Boost COMPONENTS thread REQUIRED)
find_package(Boost COMPONENTS system) # Is system REALLY required?
include_directories(${Boost_INCLUDE_DIRS})

# The project specific includes (wb.h etc.)
include_directories(${hetero_SOURCE_DIR}/include)

# Where to put the generated binaries
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/build)

# The real sources
set(SRCS
  src/mp1.cc
  src/mp2.cc
  src/mp3.cc
)

# The data-generation programs
set(TESTS
  tests/GenDataMP1.cpp
  tests/GenDataMP2.cpp
)

# Set destination and libraries for the MPs
foreach(NEXT_SRC ${SRCS})
  get_filename_component(next_BIN ${NEXT_SRC} NAME_WE)
  add_executable(${next_BIN} ${NEXT_SRC})
  target_link_libraries(${next_BIN} ${Boost_LIBRARIES})
endforeach(NEXT_SRC)

# Set destination for the data-generation programs
foreach(NEXT_SRC ${TESTS})
  get_filename_component(next_BIN ${NEXT_SRC} NAME_WE)
  add_executable(${next_BIN} ${NEXT_SRC})
endforeach(NEXT_SRC)
