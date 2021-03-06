# Copyright (c) 2016 Alain Martin
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

cmake_minimum_required(VERSION 3.0)


list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/../../cmake")
include(Reprojucer)


set(JUCE_ROOT "${CMAKE_CURRENT_LIST_DIR}/../../../JUCE" CACHE PATH "Path to JUCE")

set(JuceDemoPlugin_jucer_FILE
  "${JUCE_ROOT}/examples/audio plugin demo/JuceDemoPlugin.jucer"
  CACHE PATH "Path to JuceDemoPlugin.jucer"
)

get_filename_component(JuceDemoPlugin_jucer_DIR "${JuceDemoPlugin_jucer_FILE}" DIRECTORY)

file(COPY "${JuceDemoPlugin_jucer_DIR}/Source" DESTINATION "${CMAKE_CURRENT_LIST_DIR}")


jucer_project_begin(
  PROJECT_NAME "JuceDemoPlugin"
  PROJECT_VERSION "1.0.0"
  COMPANY_NAME "ROLI Ltd."
  COMPANY_WEBSITE "www.juce.com"
  COMPANY_EMAIL "info@juce.com"
  PROJECT_TYPE "Audio Plug-in"
  BUNDLE_IDENTIFIER "com.juce.JuceDemoPlugin"
  BINARYDATACPP_SIZE_LIMIT "Default"
  # BINARYDATA_NAMESPACE
  # PREPROCESSOR_DEFINITIONS
  PROJECT_ID "0nRd9LLGO"
)

jucer_audio_plugin_settings(
  BUILD_VST ON
  BUILD_AUDIOUNIT ON
  PLUGIN_NAME "Juce Demo Plugin"
  PLUGIN_DESCRIPTION "Juce Demo Plugin"
  PLUGIN_MANUFACTURER "ROLI Ltd."
  PLUGIN_MANUFACTURER_CODE "ROLI"
  PLUGIN_CODE "Jcdm"
  # PLUGIN_CHANNEL_CONFIGURATIONS
  PLUGIN_IS_A_SYNTH FALSE
  PLUGIN_MIDI_INPUT ON
  PLUGIN_MIDI_OUTPUT ON
  MIDI_EFFECT_PLUGIN OFF
  KEY_FOCUS ON
  PLUGIN_AU_EXPORT_PREFIX "JuceDemoProjectAU"
  # PLUGIN_AU_MAIN_TYPE
  # VST_CATEGORY
)

jucer_project_files("JuceDemoPlugin/Source"
  "Source/PluginEditor.cpp"
  "Source/PluginEditor.h"
  "Source/PluginProcessor.cpp"
  "Source/PluginProcessor.h"
  "Source/SinewaveSynth.h"
)

jucer_project_module(
  juce_audio_basics
  PATH "${JuceDemoPlugin_jucer_DIR}/../../modules"
)

jucer_project_module(
  juce_audio_devices
  PATH "${JuceDemoPlugin_jucer_DIR}/../../modules"
  # JUCE_ASIO
  # JUCE_WASAPI
  # JUCE_WASAPI_EXCLUSIVE
  # JUCE_DIRECTSOUND
  # JUCE_ALSA
  # JUCE_JACK
  # JUCE_USE_ANDROID_OPENSLES
)

jucer_project_module(
  juce_audio_formats
  PATH "${JuceDemoPlugin_jucer_DIR}/../../modules"
  # JUCE_USE_FLAC
  # JUCE_USE_OGGVORBIS
  # JUCE_USE_MP3AUDIOFORMAT
  # JUCE_USE_LAME_AUDIO_FORMAT
  # JUCE_USE_WINDOWS_MEDIA_FORMAT
)

jucer_project_module(
  juce_audio_plugin_client
  PATH "${JuceDemoPlugin_jucer_DIR}/../../modules"
  # JUCE_FORCE_USE_LEGACY_PARAM_IDS
  # JUCE_USE_STUDIO_ONE_COMPATIBLE_PARAMETERS
)

jucer_project_module(
  juce_audio_processors
  PATH "${JuceDemoPlugin_jucer_DIR}/../../modules"
  JUCE_PLUGINHOST_VST OFF
  # JUCE_PLUGINHOST_VST3
  JUCE_PLUGINHOST_AU OFF
)

jucer_project_module(
  juce_audio_utils
  PATH "${JuceDemoPlugin_jucer_DIR}/../../modules"
  # JUCE_USE_CDREADER
  # JUCE_USE_CDBURNER
)

jucer_project_module(
  juce_core
  PATH "${JuceDemoPlugin_jucer_DIR}/../../modules"
  # JUCE_FORCE_DEBUG
  # JUCE_LOG_ASSERTIONS
  # JUCE_CHECK_MEMORY_LEAKS
  # JUCE_DONT_AUTOLINK_TO_WIN32_LIBRARIES
  # JUCE_INCLUDE_ZLIB_CODE
  # JUCE_USE_CURL
  # JUCE_CATCH_UNHANDLED_EXCEPTIONS
  # JUCE_ALLOW_STATIC_NULL_VARIABLES
)

jucer_project_module(
  juce_data_structures
  PATH "${JuceDemoPlugin_jucer_DIR}/../../modules"
)

jucer_project_module(
  juce_events
  PATH "${JuceDemoPlugin_jucer_DIR}/../../modules"
)

jucer_project_module(
  juce_graphics
  PATH "${JuceDemoPlugin_jucer_DIR}/../../modules"
  # JUCE_USE_COREIMAGE_LOADER
  # JUCE_USE_DIRECTWRITE
)

jucer_project_module(
  juce_gui_basics
  PATH "${JuceDemoPlugin_jucer_DIR}/../../modules"
  # JUCE_ENABLE_REPAINT_DEBUGGING
  # JUCE_USE_XSHM
  # JUCE_USE_XRENDER
  # JUCE_USE_XCURSOR
)

jucer_project_module(
  juce_gui_extra
  PATH "${JuceDemoPlugin_jucer_DIR}/../../modules"
  # JUCE_WEB_BROWSER
  # JUCE_ENABLE_LIVE_CONSTANT_EDITOR
)

jucer_project_end()
