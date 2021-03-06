cmake_minimum_required(VERSION 3.15)
project(TempPlugin VERSION 1.0.0)

set(CMAKE_CXX_STANDARD 17)
add_subdirectory(modules)

# juce_set_vst2_sdk_path(C:/SDKs/VST_SDK/VST2_SDK/)

juce_add_plugin(TempPlugin
    COMPANY_NAME chowdsp
    PLUGIN_MANUFACTURER_CODE Chow
    PLUGIN_CODE tmp3
    FORMATS AU VST3 Standalone #VST
    ProductName "TempPlugin")

juce_generate_juce_header(TempPlugin)
add_subdirectory(src)
add_subdirectory(res)

target_compile_definitions(TempPlugin
    PUBLIC
    JUCE_DISPLAY_SPLASH_SCREEN=0
    JUCE_REPORT_APP_USAGE=0
    JUCE_WEB_BROWSER=0
    JUCE_USE_CURL=0
    JUCE_VST3_CAN_REPLACE_VST2=0
    FOLEYS_SHOW_GUI_EDITOR_PALLETTE=0
    FOLEYS_ENABLE_BINARY_DATA=1)

target_link_libraries(TempPlugin PRIVATE
    BinaryData
    juce::juce_audio_utils
    foleys_gui_magic
    chowdsp_utils)
