set(PDCOBJSC)
foreach(PDCOBJ ${PDCOBJS})
    list(APPEND PDCOBJSC ${PDCOBJ}.c)
endforeach()

add_library(PDCWinCon $<TARGET_OBJECTS:LIB> ${PDCOBJSC})

target_link_libraries(PDCWinCon PUBLIC HDR)

set_target_properties(PDCWinCon PROPERTIES
    OUTPUT_NAME pdcurses-wincon)
