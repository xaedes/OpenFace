#TBB library
include_directories(${TBB_ROOT_DIR}/include)

include_directories(${BOOST_INCLUDE_DIR})

#OpenBlas library
include_directories(../../3rdParty/OpenBLAS/include)

SET(SOURCE
    src/CCNF_patch_expert.cpp
	src/LandmarkDetectionValidator.cpp
    src/LandmarkDetectorFunc.cpp
	src/LandmarkDetectorModel.cpp
    src/LandmarkDetectorUtils.cpp
	src/LandmarkDetectorParameters.cpp
	src/Patch_experts.cpp
	src/PAW.cpp
    src/PDM.cpp
	src/SVR_patch_expert.cpp
	src/stdafx.cpp
)

SET(HEADERS
    include/OpenFace/LandmarkDetector/CCNF_patch_expert.h	
    include/OpenFace/LandmarkDetector/LandmarkCoreIncludes.h
	include/OpenFace/LandmarkDetector/LandmarkDetectionValidator.h
    include/OpenFace/LandmarkDetector/LandmarkDetectorFunc.h
	include/OpenFace/LandmarkDetector/LandmarkDetectorModel.h
	include/OpenFace/LandmarkDetector/LandmarkDetectorParameters.h
	include/OpenFace/LandmarkDetector/LandmarkDetectorUtils.h
	include/OpenFace/LandmarkDetector/Patch_experts.h	
    include/OpenFace/LandmarkDetector/PAW.h
	include/OpenFace/LandmarkDetector/PDM.h
	include/OpenFace/LandmarkDetector/SVR_patch_expert.h		
	include/OpenFace/LandmarkDetector/stdafx.h
)

include_directories(./include)
include_directories(${LandmarkDetector_SOURCE_DIR}/include)

add_library( LandmarkDetector ${SOURCE} ${HEADERS} )

target_link_libraries(LandmarkDetector PUBLIC ${OpenCV_LIBS} ${Boost_LIBRARIES} ${TBB_LIBRARIES} ${BLAS_LIBRARIES})
target_link_libraries(LandmarkDetector PUBLIC dlib)
target_include_directories(LandmarkDetector PUBLIC ${BLAS_INCLUDE_DIRS})
target_include_directories(LandmarkDetector PUBLIC ${OpenCV_INCLUDE_DIRS})
target_include_directories(LandmarkDetector PUBLIC ${Boost_INCLUDE_DIRS})

install (TARGETS LandmarkDetector DESTINATION lib)
install (FILES ${HEADERS} DESTINATION include/OpenFace/LandmarkDetector)
