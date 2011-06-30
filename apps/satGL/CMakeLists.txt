###############################################################################
#
# Build script for project
#
###############################################################################

set(CCFILES
  main.cpp
  )
set(CUFILES
  satGL.cu
  )

find_package(OpenGL REQUIRED)
find_package(GLUT REQUIRED)
find_package(GLEW REQUIRED)

include_directories(
  ${OPENGL_INCLUDE_DIR}
  ${GLUT_INCLUDE_DIR}
  ${GLEW_INCLUDE_DIR}
  )

cuda_add_executable(satGL ${CCFILES} ${CUFILES})

target_link_libraries(satGL
  cudpp
  ${OPENGL_LIBRARIES}
  ${GLUT_LIBRARIES}
  ${GLEW_LIBRARY}
  )
