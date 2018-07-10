set(PDCOBJSC)
foreach(PDCOBJ ${PDCOBJS})
    list(APPEND PDCOBJSC ${PDCOBJ}.c)
endforeach()

add_library(PDCSDL1 $<TARGET_OBJECTS:LIB> ${PDCOBJSC})

target_link_libraries(PDCSDL1 PUBLIC HDR)

target_link_libraries(PDCSDL1 PRIVATE ${SDL_LIBRARY})
target_include_directories(PDCSDL1 PRIVATE "${SDL_INCLUDE_DIR}")

set_target_properties(PDCSDL1 PROPERTIES
    OUTPUT_NAME pdcurses-sdl1)
