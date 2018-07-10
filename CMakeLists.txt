cmake_minimum_required(VERSION 3.3)

project(PDCurses
    LANGUAGES C)

find_package(SDL QUIET)
find_package(SDL2 QUIET)

if(WIN32)
    set(PROJECT_PLATFORM_DEFAULT "WinCon")
elseif(SDL2_FOUND)
    set(PROJECT_PLATFORM_DEFAULT "SDL2")
elseif(SDL_FOUND)
    set(PROJECT_PLATFORM_DEFAULT "SDL1")
endif()

set(${PROJECT_NAME}_PLATFORM "${PROJECT_PLATFORM_DEFAULT}" CACHE STRING
    "The PDCurses default platform used in demos")
set_property(CACHE ${PROJECT_NAME}_PLATFORM PROPERTY STRINGS
  "WinCon" "SDL1" "SDL2")

set(LIBOBJS
    addch addchstr addstr attr beep
    bkgd border clear color delch deleteln
    deprec getch getstr getyx inch inchstr
    initscr inopts insch insstr instr kernel
    keyname mouse move outopts overlay pad
    panel printw refresh scanw scr_dump scroll
    slk termattr terminfo touch util window
    debug)

set(PDCOBJS
    pdcclip pdcdisp pdcgetsc pdckbd pdcscrn
    pdcsetsc pdcutil)

set(DEMOS
    testcurs ozdemo xmas tuidemo firework
    ptest rain worm)

add_library(HDR INTERFACE)

target_include_directories(HDR INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}>
    $<INSTALL_INTERFACE:include/pdcurses>)

add_subdirectory(pdcurses)

if(WIN32)
    add_subdirectory(wincon)
endif()

if(SDL_FOUND)
    add_subdirectory(sdl1)
endif()

if(SDL2_FOUND)
    add_subdirectory(sdl2)
endif()

add_subdirectory(demos)
