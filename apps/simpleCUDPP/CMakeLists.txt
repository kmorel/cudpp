###############################################################################
#
# Build script for project
#
###############################################################################

set(CCFILES
  scan_gold.cpp
  )
set(CUFILES
  simpleCUDPP.cu
  )

cuda_add_executable(simpleCUDPP ${CCFILES} ${CUFILES})

target_link_libraries(simpleCUDPP
  cudpp
  )
