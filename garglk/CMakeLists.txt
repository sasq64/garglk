find_package(Freetype)

find_package(SDL)
add_library(sdl INTERFACE)
target_link_libraries(sdl INTERFACE ${SDL_LIBRARY})
target_include_directories(sdl INTERFACE ${SDL_INCLUDE_DIR})

find_package(SDL_sound)
add_library(sdl-sound INTERFACE)
target_link_libraries(sdl-sound INTERFACE ${SDL_SOUND_LIBRARIES})
target_include_directories(sdl-sound INTERFACE ${SDL_SOUND_INCLUDE_DIRS})

find_package(SDL_mixer)
add_library(sdl-mixer INTERFACE)
target_link_libraries(sdl-mixer INTERFACE ${SDL_MIXER_LIBRARIES})
target_include_directories(sdl-mixer INTERFACE ${SDL_MIXER_INCLUDE_DIRS})

find_package(GTK2)
add_library(gtk INTERFACE)
target_link_libraries(gtk INTERFACE ${GTK2_LIBRARIES})
target_include_directories(gtk INTERFACE ${GTK2_INCLUDE_DIRS})
target_compile_definitions(gtk INTERFACE ${GTK2_DEFINITIONS})

find_package(JPEG)
find_package(PNG)

find_library(SPEECH speechd)
if(SPEECH)
    message("Found `speechd` library")
    add_library(speech ttspeechd.c)
    target_link_libraries(speech ${SPEECH})
else()
    message("Found no speech library, speech will be disabled")
    add_library(speech ttsnull.c)
endif()

add_library(garglk STATIC
    gi_blorb.c gi_dispa.c cggestal.c cgblorb.c cgfref.c cgmisc.c cgstyle.c
    cgstream.c cgunicod.c cgdate.c window.c winblank.c winpair.c wingrid.c
    wintext.c wingfx.c winmask.c event.c draw.c config.c imgload.c imgscale.c
    fontdata.c babeldata.c
    sndsdl.c
    sysgtk.c fontfc.c  
    main.c
)

target_link_libraries(garglk PUBLIC gtk Freetype::Freetype JPEG::JPEG PNG::PNG
    sdl sdl-mixer sdl-sound speech m fontconfig)
target_include_directories(garglk INTERFACE ${CMAKE_CURRENT_SOURCE_DIR})
target_compile_definitions(garglk PRIVATE GARGLKINI="/etc/garglk.ini" BUNDLED_FONTS)
