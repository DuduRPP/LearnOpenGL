# Add GLAD source file
add_library(glad SHARED 
    glad.c
)

target_include_directories(glad PRIVATE "${Glad_SOURCE_DIR}/include/")