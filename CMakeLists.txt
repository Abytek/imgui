cmake_minimum_required(VERSION 3.16)
project(ImGui LANGUAGES CXX)

option(IMGUI_ENABLE_WIN32 "Enable Win32 backend" ON)
option(IMGUI_ENABLE_DIRECTX12 "Enable DX12 backend" OFF)

add_library(ImGui STATIC
    imgui.cpp
    imgui_draw.cpp
    imgui_tables.cpp
    imgui_widgets.cpp
)

if(IMGUI_ENABLE_WIN32)
    target_sources(ImGui
        PRIVATE
            backends/imgui_impl_win32.cpp
    )
    target_include_directories(ImGui
        PUBLIC backends
    )
endif()

if(IMGUI_ENABLE_DIRECTX12)
    target_sources(ImGui PRIVATE
        backends/imgui_impl_dx12.cpp
    )
endif()

target_include_directories(ImGui PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
)
