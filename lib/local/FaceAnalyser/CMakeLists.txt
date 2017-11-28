#TBB library
include_directories(${TBB_ROOT_DIR}/include)
include_directories(${BLAS_ROOT_DIR})

include_directories(${BOOST_INCLUDE_DIR})

#OpenBlas library
include_directories(../../3rdParty/OpenBLAS/include)

#LandmarkDetector library
include_directories(../../local/LandmarkDetector/include)

SET(SOURCE
    src/Face_utils.cpp
	src/FaceAnalyser.cpp
	src/FaceAnalyserParameters.cpp
	src/PAW.cpp
	src/PDM.cpp		
	src/SVM_dynamic_lin.cpp
	src/SVM_static_lin.cpp
	src/SVR_dynamic_lin_regressors.cpp
	src/SVR_static_lin_regressors.cpp
)

SET(HEADERS
    include/OpenFace/FaceAnalyser/Face_utils.h	
	include/OpenFace/FaceAnalyser/FaceAnalyser.h
	include/OpenFace/FaceAnalyser/FaceAnalyserParameters.h
	include/OpenFace/FaceAnalyser/PAW.h
	include/OpenFace/FaceAnalyser/PDM.h		
	include/OpenFace/FaceAnalyser/SVM_dynamic_lin.h
	include/OpenFace/FaceAnalyser/SVM_static_lin.h
	include/OpenFace/FaceAnalyser/SVR_dynamic_lin_regressors.h
	include/OpenFace/FaceAnalyser/SVR_static_lin_regressors.h
)

include_directories(./include)
include_directories(${FACEANALYSER_SOURCE_DIR}/include)

add_library( FaceAnalyser ${SOURCE} ${HEADERS})

target_link_libraries(FaceAnalyser PUBLIC ${OpenCV_LIBS} ${Boost_LIBRARIES} ${TBB_LIBRARIES} ${BLAS_LIBRARIES})
target_link_libraries(FaceAnalyser PUBLIC dlib)
target_include_directories(FaceAnalyser PUBLIC ${BLAS_INCLUDE_DIRS})
target_include_directories(FaceAnalyser PUBLIC ${OpenCV_INCLUDE_DIRS})
target_include_directories(FaceAnalyser PUBLIC ${Boost_INCLUDE_DIRS})


install (TARGETS FaceAnalyser DESTINATION lib)
install (FILES ${HEADERS} DESTINATION include/OpenFace/FaceAnalyser)
