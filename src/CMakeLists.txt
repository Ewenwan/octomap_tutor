# 增加PCL库的依赖
FIND_PACKAGE( PCL REQUIRED COMPONENTS common io )

#  SET设置变量 支持C++11    -O2  优化等级
SET(CMAKE_C_FLAGS "${CMAK_C_FLAGS} -g -Wall -O2 -std=c11")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}  -g -Wall -O2 -std=c++11")
# 支持C++14, when gcc version > 5.1, use -std=c++14 instead of c++1y
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}  -g -Wall -O2 -std=c++1y")


# 添加头文件和库文件
ADD_DEFINITIONS( ${PCL_DEFINITIONS} )
INCLUDE_DIRECTORIES( ${PCL_INCLUDE_DIRS}  )
LINK_LIBRARIES( ${PCL_LIBRARY_DIRS} )

# octomap
FIND_PACKAGE( octomap REQUIRED )
INCLUDE_DIRECTORIES( ${OCTOMAP_INCLUDE_DIRS} )

ADD_EXECUTABLE( pcd2octomap pcd2octomap.cpp )
TARGET_LINK_LIBRARIES( pcd2octomap
    ${PCL_LIBRARIES}
    ${OCTOMAP_LIBRARIES})

ADD_EXECUTABLE( pcd2colorOctomap pcd2colorOctomap.cpp )
TARGET_LINK_LIBRARIES( pcd2colorOctomap
    ${PCL_LIBRARIES}
    ${OCTOMAP_LIBRARIES})

FIND_PACKAGE(OpenCV REQUIRED)

ADD_EXECUTABLE( joinmap joinMap.cpp )
TARGET_LINK_LIBRARIES( joinmap
    ${OCTOMAP_LIBRARIES}
    ${OpenCV_LIBS})

