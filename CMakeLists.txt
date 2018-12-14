project(Cg)

message("CMAKE_SIZEOF_VOID_P: ${CMAKE_SIZEOF_VOID_P}")

if (WIN32)
  # manually copy to build and install the correct DLL
  if (CMAKE_SIZEOF_VOID_P EQUAL 8)
    file(GLOB CG_FILES "bin64/*.exe" "bin64/*.dll" "lib64/*.lib")
  else ()
    file(GLOB CG_FILES "bin/*.exe" "bin/*.dll" "lib/*.lib")
  endif ()

elseif (UNIX)
  # manually install the correct .so
  if (CMAKE_SIZEOF_VOID_P EQUAL 8)
    file(GLOB CG_FILES "lib64/*.so")
  else ()
    file(GLOB CG_FILES "lib/*.so")
  endif ()
endif ()

install(DIRECTORY include/ DESTINATION include)
install(FILES ${CG_FILES} DESTINATION bin)
