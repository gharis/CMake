## creating exe/dll
https://cmake.org/cmake/help/latest/command/target_link_libraries.html

https://cmake.org/cmake/help/latest/command/add_library.html
## Cmake Generators 


find_package(Idlpp-cxx PATHS ${CMAKE_CURRENT_SOURCE_DIR}/dds/idlpp-cxx)

#make dll from source files
add_library(MyProject SHARED MyProject.h MyProject.cpp) # MyProject.dll

# Link both dlls to idl data type library and ddscxx.
target_link_libraries(MyProject MyProjectData_lib CycloneDDS-CXX::ddscxx)  

# Copy dlls to executable directory for runtime, Adds a post-build event to MyProject runtime 
add_custom_command(TARGET MyProject POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
        "$(TargetPath)"
