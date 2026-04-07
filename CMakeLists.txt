cmake_minimum_required(VERSION 3.16)
project(ImGuiCore LANGUAGES CXX)

option(IMGUI_ENABLE_WIN32 "Enable Win32 backend" ON)
option(IMGUI_ENABLE_DIRECTX12 "Enable DX12 backend" OFF)

add_library(ImGuiCore STATIC
    imgui.cpp
    imgui_draw.cpp
    imgui_tables.cpp
    imgui_widgets.cpp
)

if(IMGUI_ENABLE_WIN32)
    target_sources(ImGuiCore
        PRIVATE
            backends/imgui_impl_win32.cpp
    )
    target_include_directories(ImGuiCore
        PUBLIC backends
    )
endif()

if(IMGUI_ENABLE_DIRECTX12)
    target_sources(ImGuiCore PRIVATE
        backends/imgui_impl_dx12.cpp
    )
endif()

target_include_directories(ImGuiCore PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
)
