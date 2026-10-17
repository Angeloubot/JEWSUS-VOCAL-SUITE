
cmake_minimum_required(VERSION 3.22)

project(KiidAngelVocalSuite VERSION 0.1.0)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(NOT EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/JUCE/CMakeLists.txt")
    message(FATAL_ERROR "JUCE framework was not downloaded.")
endif()

add_subdirectory(JUCE)

juce_add_plugin(KiidAngelVocalSuite
    COMPANY_NAME "Angelous Jew Records"
    BUNDLE_ID "com.angelousjewrecordsvocal.suite"
    PLUGIN_MANUFACTURER_CODE KdAn
    PLUGIN_CODE KAvS
    FORMATS VST3
    PRODUCT_NAME "Kiid Angel Vocal Suite"
    DESCRIPTION "Vocal processing plugin"
    IS_SYNTH FALSE
    NEEDS_MIDI_INPUT FALSE
    NEEDS_MIDI_OUTPUT FALSE
    IS_MIDI_EFFECT FALSE
    EDITOR_WANTS_KEYBOARD_FOCUS FALSE
    COPY_PLUGIN_AFTER_BUILD FALSE
)

target_sources(KiidAngelVocalSuite
    PRIVATE
        Source/PluginProcessor.cpp
        Source/PluginProcessor.h
        Source/PluginEditor.cpp
        Source/PluginEditor.h
)

target_compile_definitions(KiidAngelVocalSuite
    PUBLIC
        JUCE_WEB_BROWSER=0
        JUCE_USE_CURL=0
        JUCE_VST3_CAN_REPLACE_VST2=0
)

target_link_libraries(KiidAngelVocalSuite
    PRIVATE
        juce::juce_audio_utils
        juce::juce_dsp
    PUBLIC
        juce::juce_recommended_config_flags
        juce::juce_recommended_lto_flags
        juce::juce_recommended_warning_flags
)
