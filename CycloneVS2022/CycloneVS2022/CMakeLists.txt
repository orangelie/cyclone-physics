cmake_minimum_required (VERSION 3.8)

set(BODY "./src/body.cpp" "./include/cyclone/body.h")
set(CORE "./src/core.cpp" "./include/cyclone/core.h")
set(COLLIDE_COARSE "./src/collide_coarse.cpp" "./include/cyclone/collide_coarse.h")
set(COLLIDE_FINE "./src/collide_fine.cpp" "./include/cyclone/collide_fine.h")
set(CONTACTS "./src/contacts.cpp" "./include/cyclone/contacts.h")
set(CYCLONE "./include/cyclone/cyclone.h")
set(FGEN "./src/fgen.cpp" "./include/cyclone/fgen.h")
set(JOINTS "./src/joints.cpp" "./include/cyclone/joints.h")
set(PARTICLE "./src/particle.cpp" "./include/cyclone/particle.h")
set(PFGEN "./src/pfgen.cpp" "./include/cyclone/pfgen.h")
set(PCONTACTS "./src/pcontacts.cpp" "./include/cyclone/pcontacts.h")
set(PLINKS "./src/plinks.cpp" "./include/cyclone/plinks.h")
set(PRECISION "./include/cyclone/precision.h")
set(PWORLD "./src/pworld.cpp" "./include/cyclone/pworld.h")
set(RANDOM "./src/random.cpp" "./include/cyclone/random.h")
set(WORLD "./src/world.cpp" "./include/cyclone/world.h")
set(CYCLONE_INC ${BODY} ${CORE} ${COLLIDE_COARSE} ${COLLIDE_FINE} ${CONTACTS} ${CYCLONE} ${FGEN} ${JOINTS} ${PFGEN} ${PARTICLE} ${PCONTACTS} ${PLINKS} ${PRECISION} ${PWORLD} ${RANDOM} ${WORLD})

set(APP "./src/demos/app.cpp" "./src/demos/app.h")
set(TIMING "./src/demos/timing.cpp" "./src/demos/timing.h")
set(CYCLONE_MAIN "./src/demos/main.cpp" "./src/demos/ogl_headers.h" ${APP} ${TIMING})


find_package(OpenGL REQUIRED)
link_directories(${CMAKE_SOURCE_DIR}/CycloneVS2022/lib)




# ballistic
add_executable (ballistic ${CYCLONE_INC} ${CYCLONE_MAIN} "./src/demos/ballistic/ballistic.cpp")
include_directories(ballistic "./include")
target_link_libraries(ballistic OpenGL::GL)

# bigballistic
add_executable (bigballistic ${CYCLONE_INC} ${CYCLONE_MAIN} "./src/demos/bigballistic/bigballistic.cpp")
include_directories(bigballistic "./include")
target_link_libraries(bigballistic OpenGL::GL)

# blob
add_executable (blob ${CYCLONE_INC} ${CYCLONE_MAIN} "./src/demos/blob/blob.cpp")
include_directories(blob "./include")
target_link_libraries(blob OpenGL::GL)

# bridge
add_executable (bridge ${CYCLONE_INC} ${CYCLONE_MAIN} "./src/demos/bridge/bridge.cpp")
include_directories(bridge "./include")
target_link_libraries(bridge OpenGL::GL)

# explosion
add_executable (explosion ${CYCLONE_INC} ${CYCLONE_MAIN} "./src/demos/explosion/explosion.cpp")
include_directories(explosion "./include")
target_link_libraries(explosion OpenGL::GL)

# fireworks
add_executable (fireworks ${CYCLONE_INC} ${CYCLONE_MAIN} "./src/demos/fireworks/fireworks.cpp")
include_directories(fireworks "./include")
target_link_libraries(fireworks OpenGL::GL)

# flightsim
add_executable (flightsim ${CYCLONE_INC} ${CYCLONE_MAIN} "./src/demos/flightsim/flightsim.cpp")
include_directories(flightsim "./include")
target_link_libraries(flightsim OpenGL::GL)

# fracture
add_executable (fracture ${CYCLONE_INC} ${CYCLONE_MAIN} "./src/demos/fracture/fracture.cpp")
include_directories(fracture "./include")
target_link_libraries(fracture OpenGL::GL)

# platform
add_executable (platform ${CYCLONE_INC} ${CYCLONE_MAIN} "./src/demos/platform/platform.cpp")
include_directories(platform "./include")
target_link_libraries(platform OpenGL::GL)

# ragdoll
add_executable (ragdoll ${CYCLONE_INC} ${CYCLONE_MAIN} "./src/demos/ragdoll/ragdoll.cpp")
include_directories(ragdoll "./include")
target_link_libraries(ragdoll OpenGL::GL)

# sailboat
add_executable (sailboat ${CYCLONE_INC} ${CYCLONE_MAIN} "./src/demos/sailboat/sailboat.cpp")
include_directories(sailboat "./include")
target_link_libraries(sailboat OpenGL::GL)




if(MSVC)
  set(CMAKE_EXE_LINKER_FLAGS
      "${CMAKE_EXE_LINKER_FLAGS} /NODEFAULTLIB:libcmt.lib /NODEFAULTLIB:libcpmt.lib")
endif()

add_custom_command(TARGET bigballistic POST_BUILD
  COMMAND ${CMAKE_COMMAND} -E copy_directory
      ${CMAKE_SOURCE_DIR}/CycloneVS2022/bin
      ${CMAKE_BINARY_DIR}/CycloneVS2022)