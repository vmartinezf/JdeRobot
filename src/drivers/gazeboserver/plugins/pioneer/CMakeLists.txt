include_directories(
	${GAZEBO_INCLUDE_DIRS}
    ${INTERFACES_CPP_DIR}
    ${LIBS_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR})

link_directories(${GAZEBO_LIBRARY_DIRS})
#boost_system 
add_library(motors SHARED motors.cc)
target_link_libraries(motors 
	${GAZEBO_libraries} 
	${ZeroCIce_LIBRARIES} 

    colorspacesmm
    JderobotInterfaces) 
    
add_library(pose3d_pioneer SHARED pose3d.cc)
target_link_libraries(pose3d_pioneer
	${GAZEBO_libraries} 

	${ZeroCIce_LIBRARIES} 
    colorspacesmm
    JderobotInterfaces)   

add_library(laser SHARED laser.cc)
target_link_libraries(laser 
	RayPlugin 
	${GAZEBO_libraries} 
	${ZeroCIce_LIBRARIES} 
    colorspacesmm
    JderobotInterfaces) 

add_library(camera_dump SHARED camera_dump.cc)
target_link_libraries(camera_dump ${GAZEBO_libraries} 
	CameraPlugin 
	colorspacesmm	
	${ZeroCIce_LIBRARIES}     
    JderobotInterfaces)
    
    
add_library(pose3dencoders SHARED pose3dencoders.cc)
target_link_libraries(pose3dencoders ${GAZEBO_libraries} 	 	
	${GAZEBO_libraries} 
	${ZeroCIce_LIBRARIES} 
    colorspacesmm
    JderobotInterfaces)


INSTALL (TARGETS motors laser camera_dump pose3dencoders pose3d_pioneer DESTINATION share/jderobot/gazebo/plugins/pioneer/ COMPONENT core)
FILE(GLOB_RECURSE CFG_FILES ${CMAKE_CURRENT_SOURCE_DIR}/*.cfg)
INSTALL (FILES ${CFG_FILES} DESTINATION ${CMAKE_INSTALL_PREFIX}/share/jderobot/conf COMPONENT core)
