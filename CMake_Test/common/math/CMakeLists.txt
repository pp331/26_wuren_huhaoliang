aux_source_directory(src Path_Math)

find_package(OpenCV REQUIRED)

add_library(Math STATIC ${Path_Math})

target_include_directories(Math PUBLIC include)
target_include_directories(Math PUBLIC ${OpenCV_INCLUDE_DIRS})
target_link_libraries(Math PUBLIC ${OpenCV_LIBS})