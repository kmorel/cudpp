##############################################################################
#
# CUDA Data Parallel Primitives (CUDPP) CMake file
#
###############################################################################

include_directories(
  ${CMAKE_CURRENT_SOURCE_DIR}/src
  ${CMAKE_CURRENT_SOURCE_DIR}/src/app
  ${CMAKE_CURRENT_SOURCE_DIR}/src/kernel
  ${CMAKE_CURRENT_SOURCE_DIR}/src/cta
  )

set(CCFILES
  src/cudpp.cpp
  src/cudpp_plan.cpp
  src/cudpp_plan_manager.cpp
  src/cudpp_maximal_launch.cpp
  )

set(CUFILES
  src/app/compact_app.cu
  src/app/scan_app.cu
  src/app/segmented_scan_app.cu
  src/app/spmvmult_app.cu
  src/app/radixsort_app.cu
  src/app/rand_app.cu 
  )

set(HFILES
  include/cudpp.h
  )

cuda_add_library(cudpp ${CCFILES} ${CUFILES})

target_link_libraries(cudpp
  cutil
  )

install(FILES ${HFILES}
  DESTINATION include
  )

install(TARGETS cudpp
  DESTINATION lib
  EXPORT cudpp-targets
  )

install(EXPORT cudpp-targets
  DESTINATION lib
  )
