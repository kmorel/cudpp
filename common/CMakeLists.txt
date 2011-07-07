
set(CCFILES
  src/bank_checker.cpp
  src/cmd_arg_reader.cpp
  src/cutil.cpp
  src/stopwatch.cpp
  src/stopwatch_linux.cpp
  src/findFile.cpp
  )

cuda_add_library(cutil ${CCFILES})

install(TARGETS cutil
  DESTINATION lib
  EXPORT cudpp-targets
  )
