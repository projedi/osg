IF(ANDROID)
    SET(MODULE_USER_STATIC_OR_DYNAMIC ${OPENSCENEGRAPH_USER_DEFINED_DYNAMIC_OR_STATIC})
ENDIF(ANDROID)

IF(MSVC80 OR MSVC90)
  OPTION(OSG_MSVC_GENERATE_PLUGINS_AND_WRAPPERS_MANIFESTS "Generate or not manifests files under VS8 for dynamically loaded dlls" ON)
ENDIF()

option(OSG_NO_BUILD_ALL "" OFF)
if(NOT OSG_NO_BUILD_ALL)
   set(folders
        OpenThreads
        osg
        osgDB 
        osgUtil 
        osgGA 
        osgText 
        osgViewer
        osgAnimation 
        osgFX
        osgManipulator
        osgParticle
        osgPresentation
        osgShadow
        osgSim
        osgTerrain
        osgWidget
        osgVolume
        osgWrappers/serializers
        osgWrappers/deprecated-dotosg
        osgPlugins
    )
else()
   option(OSG_BUILD_OPENTHREADS "" OFF)
   if(OSG_BUILD_OPENTHREADS)
      list(APPEND folders OpenThreads)
   endif()
   option(OSG_BUILD_OSG "" OFF)
   if(OSG_BUILD_OSG)
      list(APPEND folders osg)
   endif()
   option(OSG_BUILD_OSGDB "" OFF)
   if(OSG_BUILD_OSGDB)
      list(APPEND folders osgDB)
   endif()
   option(OSG_BUILD_OSGUTIL "" OFF)
   if(OSG_BUILD_OSGUTIL)
      list(APPEND folders osgUtil)
   endif()
   option(OSG_BUILD_OSGGA "" OFF)
   if(OSG_BUILD_OSGGA)
      list(APPEND folders osgGA)
   endif()
   option(OSG_BUILD_OSGTEXT "" OFF)
   if(OSG_BUILD_OSGTEXT)
      list(APPEND folders osgText)
   endif()
   option(OSG_BUILD_OSGVIEWER "" OFF)
   if(OSG_BUILD_OSGVIEWER)
      list(APPEND folders osgViewer)
   endif()
   option(OSG_BUILD_OSGANIMATION "" OFF)
   if(OSG_BUILD_OSGANIMATION)
      list(APPEND folders osgAnimation)
   endif()
   option(OSG_BUILD_OSGFX "" OFF)
   if(OSG_BUILD_OSGFX)
      list(APPEND folders osgFX)
   endif()
   option(OSG_BUILD_OSGMANIPULATOR "" OFF)
   if(OSG_BUILD_OSGMANIPULATOR)
      list(APPEND folders osgManipulator)
   endif()
   option(OSG_BUILD_OSGPARTICLE "" OFF)
   if(OSG_BUILD_OSGPARTICLE)
      list(APPEND folders osgParticle)
   endif()
   option(OSG_BUILD_OSGPRESENTATION "" OFF)
   if(OSG_BUILD_OSGPRESENTATION)
      list(APPEND folders osgPresentation)
   endif()
   option(OSG_BUILD_OSGSHADOW "" OFF)
   if(OSG_BUILD_OSGSHADOW)
      list(APPEND folders osgShadow)
   endif()
   option(OSG_BUILD_OSGSIM "" OFF)
   if(OSG_BUILD_OSGSIM)
      list(APPEND folders osgSim)
   endif()
   option(OSG_BUILD_OSGTERRAIN "" OFF)
   if(OSG_BUILD_OSGTERRAIN)
      list(APPEND folders osgTerrain)
   endif()
   option(OSG_BUILD_OSGWIDGET "" OFF)
   if(OSG_BUILD_OSGWIDGET)
      list(APPEND folders osgWidget)
   endif()
   option(OSG_BUILD_OSGVOLUME "" OFF)
   if(OSG_BUILD_OSGVOLUME)
      list(APPEND folders osgVolume)
   endif()
   option(OSG_BUILD_OSGSERIALIZERS "" OFF)
   if(OSG_BUILD_OSGSERIALIZERS)
      list(APPEND folders osgWrappers/serializers)
   endif()
   option(OSG_BUILD_OSGDEPRECATED "" OFF)
   if(OSG_BUILD_OSGDEPRECATED)
      list(APPEND folders osgWrappers/deprecated-dotosg)
   endif()
   list(APPEND folders osgPlugins)
endif()

FOREACH(mylibfolder ${folders})
ADD_SUBDIRECTORY(${mylibfolder})
ENDFOREACH()

IF ((QT4_FOUND OR Qt5Widgets_FOUND) AND NOT ANDROID)
    ADD_SUBDIRECTORY(osgQt)
ENDIF()

IF(ANDROID)
    configure_file("${OSG_ANDROID_TEMPLATES}/Android.mk.src.in" "${CMAKE_CURRENT_BINARY_DIR}/Android.mk")
ENDIF()

