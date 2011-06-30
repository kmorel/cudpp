###############################################################################
#
# Build script for project
#
###############################################################################

set(CCFILES
  scan_gold.cpp
  compact_gold.cpp
  spmvmult_gold.cpp
  cudpp_testrig_options.cpp
  )
set(CUFILES
  cudpp_testrig.cu
  )

cuda_add_executable(cudpp_testrig ${CCFILES} ${CUFILES})

target_link_libraries(cudpp_testrig
  cudpp
  )
