cmake_minimum_required(VERSION 3.5)
project(terps)

add_executable(frotz
    frotz/buffer.c frotz/err.c frotz/fastmem.c frotz/files.c frotz/input.c
    frotz/main.c frotz/math.c frotz/object.c frotz/process.c frotz/quetzal.c
    frotz/random.c frotz/redirect.c frotz/sound.c frotz/stream.c frotz/table.c
    frotz/text.c frotz/variable.c frotz/glkscreen.c frotz/glkmisc.c)
target_link_libraries(frotz PRIVATE garglk)

add_executable(magnetic magnetic/Glk/glk.c magnetic/Generic/emu.c)
target_link_libraries(magnetic PRIVATE garglk)
target_include_directories(magnetic PRIVATE magnetic/Generic)

add_executable(nitfol 
    nitfol/automap.c nitfol/solve.c nitfol/infix.c nitfol/copying.c
    nitfol/debug.c nitfol/inform.c nitfol/quetzal.c nitfol/undo.c
    nitfol/op_call.c nitfol/decode.c nitfol/errmesg.c nitfol/globals.c
    nitfol/iff.c nitfol/init.c nitfol/ nitfol/io.c nitfol/z_io.c
    nitfol/op_jmp.c nitfol/op_math.c nitfol/op_save.c nitfol/op_table.c
    nitfol/op_v6.c nitfol/oplist.c nitfol/stack.c nitfol/zscii.c
    nitfol/tokenise.c nitfol/struct.c nitfol/objects.c nitfol/portfunc.c
    nitfol/hash.c nitfol/sound.c nitfol/graphics.c nitfol/blorb.c
    nitfol/main.c nitfol/startunix.c)
target_compile_definitions(nitfol PRIVATE SMART_TOKENISER DEBUGGING USE_INLINE NO_TICK)
target_link_libraries(nitfol PRIVATE garglk)


