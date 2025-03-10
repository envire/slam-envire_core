find_package(Boost COMPONENTS serialization filesystem system thread)

set(headers items/ItemBase.hpp
            items/Item.hpp
            items/Frame.hpp
            items/Transform.hpp
            items/Environment.hpp
            items/AlignedBoundingBox.hpp
            items/RandomGenerator.hpp
            items/SpatialItem.hpp
            items/BoundingVolume.hpp
            items/ItemMetadata.hpp
            items/SpatioTemporal.hpp
            graph/GraphExceptions.hpp
            graph/GraphVisitors.hpp
            graph/TreeView.hpp
            graph/GraphTypes.hpp
            graph/Graph.hpp
            graph/TransformGraph.hpp
            graph/EnvireGraph.hpp
            graph/Path.hpp
            graph/GraphDrawing.hpp
            events/GraphEvent.hpp
            events/GraphEventSubscriber.hpp
            events/GraphEventDispatcher.hpp
            events/GraphEventPublisher.hpp
            events/GraphEventQueue.hpp
            events/EdgeEvents.hpp
            events/ItemAddedEvent.hpp
            events/ItemRemovedEvent.hpp
            events/FrameEvents.hpp
            events/GraphItemEventDispatcher.hpp
            events/GraphEventExceptions.hpp
            serialization/Serialization.hpp
            serialization/SerializationHandle.hpp
            serialization/SerializationRegistration.hpp
            serialization/ItemHeader.hpp
            serialization/BinaryBufferHelper.hpp
            serialization/SerializableConcept.hpp
            util/Demangle.hpp
            util/Exceptions.hpp
            util/ThreadSaveEnvireGraph.hpp
            util/EnvireManager.hpp)

            
set(sources items/ItemBase.cpp
            items/AlignedBoundingBox.cpp
            items/ItemMetadata.cpp
            events/GraphEvent.cpp
            events/GraphEventPublisher.cpp
            events/GraphEventDispatcher.cpp
            events/GraphEventSubscriber.cpp
            events/GraphEventQueue.cpp
            graph/EnvireGraph.cpp
            graph/TreeView.cpp
            graph/Path.cpp
            serialization/Serialization.cpp
            util/Demangle.cpp
            util/EnvireManager.cpp)
            
set(deps_pkg_config base-types boost_serialization)

if(PLUGIN_LIBS_FOUND)

  set(headers ${headers}
              plugin/ClassLoader.hpp
              plugin/Plugin.hpp)
  set(sources ${sources}
              plugin/ClassLoader.cpp)
  set(deps_pkg_config ${deps_pkg_config} class_loader_melodic plugin_manager)
  
endif()

             

rock_library(envire_core
    HEADERS ${headers}
    SOURCES ${sources}
    DEPS_CMAKE Glog
    DEPS_PKGCONFIG ${deps_pkg_config}
    DEPS
        Boost::filesystem
        Boost::serialization
        Boost::system
        Boost::thread
)


install(FILES
    all
    DESTINATION include/envire_core)
