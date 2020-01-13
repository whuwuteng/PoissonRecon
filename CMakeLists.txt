cmake_minimum_required(VERSION 3.13)

project(PoissonRecon VERSION 1.0.0 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_definitions(-DNOMINMAX)

find_package(OpenMP)
if (OPENMP_FOUND)
	add_definitions(-D_OPENMP)
	set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
	set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
	set (CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
endif()

find_package(PNG REQUIRED)
include_directories(${PNG_INCLUDE_DIR})

find_package(JPEG REQUIRED)
include_directories(${JPEG_INCLUDE_DIR})

find_package(ZLIB REQUIRED)
include_directories(${ZLIB_INCLUDE_DIR})

include_directories(include ${PROJECT_SOURCE_DIR})

add_executable(AdaptiveTreeVisualization Src/AdaptiveTreeVisualization.cpp)
target_link_libraries(AdaptiveTreeVisualization ${PNG_LIBRARIES} ${JPEG_LIBRARIES} ${ZLIB_LIBRARIES})

add_executable(ChunkPLY Src/ChunkPLY.cpp)
target_link_libraries(ChunkPLY ${PNG_LIBRARIES} ${JPEG_LIBRARIES} ${ZLIB_LIBRARIES})

add_executable(EDTInHeat Src/EDTInHeat.cpp)
target_link_libraries(EDTInHeat ${PNG_LIBRARIES} ${JPEG_LIBRARIES} ${ZLIB_LIBRARIES})

add_executable(ImageStitching Src/ImageStitching.cpp)
target_link_libraries(ImageStitching ${PNG_LIBRARIES} ${JPEG_LIBRARIES} ${ZLIB_LIBRARIES})

add_executable(PointInterpolant Src/PointInterpolant.cpp)
target_link_libraries(PointInterpolant ${PNG_LIBRARIES} ${JPEG_LIBRARIES} ${ZLIB_LIBRARIES})

add_executable(PoissonRecon Src/PoissonRecon.cpp)
target_link_libraries(PoissonRecon ${PNG_LIBRARIES} ${JPEG_LIBRARIES} ${ZLIB_LIBRARIES})

add_executable(SSDRecon Src/SSDRecon.cpp)
target_link_libraries(SSDRecon ${PNG_LIBRARIES} ${JPEG_LIBRARIES} ${ZLIB_LIBRARIES})

add_executable(SurfaceTrimmer Src/SurfaceTrimmer.cpp)
target_link_libraries(SurfaceTrimmer ${PNG_LIBRARIES} ${JPEG_LIBRARIES} ${ZLIB_LIBRARIES})
