set(LIBOBJSC)
foreach(LIBOBJ ${LIBOBJS})
    list(APPEND LIBOBJSC ${LIBOBJ}.c)
endforeach()

add_library(LIB OBJECT ${LIBOBJSC})

target_include_directories(LIB PRIVATE ..)
