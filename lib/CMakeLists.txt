project(libromfs)

set(CMAKE_CXX_STANDARD 20)

file(GLOB_RECURSE ROMFS_FILES
    "${LIBROMFS_RESOURCE_LOCATION}/*"
)

add_library(libromfs STATIC
    ${ROMFS}
    source/romfs.cpp
)

add_custom_command(OUTPUT ${ROMFS}
        COMMAND $<TARGET_FILE:generator>
        DEPENDS ../generator ${ROMFS_FILES}
        )

add_custom_target(romfs_file_packer ALL DEPENDS ${ROMFS_FILES})

target_include_directories(libromfs PUBLIC include)
