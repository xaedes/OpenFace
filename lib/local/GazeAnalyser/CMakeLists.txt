#TBB library
include_directories(${TBB_ROOT_DIR}/include)
include_directories(${BLAS_ROOT_DIR})

include_directories(${BOOST_INCLUDE_DIR})

#OpenBlas library
include_directories(../../3rdParty/OpenBLAS/include)

#LandmarkDetector library
include_directories(../../local/LandmarkDetector/include)

SET(SOURCE
    src/GazeEstimation.cpp
)

SET(HEADERS
    include/OpenFace/GazeAnalyser/GazeEstimation.h
)

include_directories(./include)
include_directories(${GAZEANALYSER_SOURCE_DIR}/include)

add_library( GazeAnalyser ${SOURCE} ${HEADERS})

target_link_libraries(GazeAnalyser PUBLIC ${OpenCV_LIBS} ${Boost_LIBRARIES} ${TBB_LIBRARIES} ${BLAS_LIBRARIES})
target_link_libraries(GazeAnalyser PUBLIC dlib)
target_include_directories(GazeAnalyser PUBLIC ${BLAS_INCLUDE_DIRS})
target_include_directories(GazeAnalyser PUBLIC ${OpenCV_INCLUDE_DIRS})
target_include_directories(GazeAnalyser PUBLIC ${Boost_INCLUDE_DIRS})

install (TARGETS GazeAnalyser DESTINATION lib)
install (FILES ${HEADERS} DESTINATION include/OpenFace/GazeAnalyser)
