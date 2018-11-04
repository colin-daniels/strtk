cmake_minimum_required(VERSION 3.0)
project(strtk CXX)

option(STRTK_ENABLE_TESTS   "Enable tests for project" ON)

set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)

set(Boost_USE_MULTITHREADED ON)
# not sure why but cmake refuses to find boost lexical cast?
find_package(Boost REQUIRED COMPONENTS 
    random regex)

add_library(strtk INTERFACE)

target_include_directories(strtk INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    ${Boost_INCLUDE_DIRS})
        
target_link_libraries(strtk INTERFACE
    ${Boost_LIBRARIES})

if(STRTK_ENABLE_TESTS)
    add_executable(strtk_tokenizer_test
        strtk_tokenizer_test.cpp)
        
    target_link_libraries(strtk_tokenizer_test PRIVATE strtk)

    add_executable(strtk_parse_test
        strtk_parse_test.cpp)
        
    target_link_libraries(strtk_parse_test PRIVATE strtk)
        
    enable_testing()
    add_test(strtk_tokenizer_test strtk_tokenizer_test)
    add_test(strtk_parse_test strtk_parse_test)
endif()
