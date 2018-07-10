set(PDCOBJSC)
foreach(PDCOBJ ${PDCOBJS})
    list(APPEND PDCOBJSC ${PDCOBJ}.c)
endforeach()

add_library(PDCSDL2 $<TARGET_OBJECTS:LIB> ${PDCOBJSC})

target_link_libraries(PDCSDL2 PUBLIC HDR)

if(TARGET SDL2::SDL2)
    target_link_libraries(PDCSDL2 PRIVATE SDL2::SDL2)
    get_target_property(SDL2_INCLUDE_DIR SDL2::SDL2 INTERFACE_INCLUDE_DIRECTORIES)
    if(EXISTS ${SDL2_INCLUDE_DIR}/SDL2)
        target_include_directories(PDCSDL2 PRIVATE "${SDL2_INCLUDE_DIR}/SDL2")
    endif()
else()
    target_link_libraries(PDCSDL2 PRIVATE ${SDL2_LIBRARIES})
    target_include_directories(PDCSDL2 PRIVATE "${SDL2_INCLUDE_DIRS}")
endif()

set_target_properties(PDCSDL2 PROPERTIES
    OUTPUT_NAME pdcurses-sdl2)
