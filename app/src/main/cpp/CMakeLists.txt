cmake_minimum_required(VERSION 3.6.0)

# Main
add_library(
    NativeLib
    SHARED
    NativeMain.cpp
)

# Other Library

## log
### android_native_app_glue でログの出力が行われるため記述
find_library(log-lib log)

## android_native_app_glue
add_library(
    android_native_app_glue
    STATIC
    ${ANDROID_NDK}/sources/android/native_app_glue/android_native_app_glue.c
)

### NativeMain.h で android_native_app_glue.h を参照するため記述
include_directories(${ANDROID_NDK}/sources/android/native_app_glue/)


# それぞれリンク
target_link_libraries(
    NativeLib
    android
    android_native_app_glue
    ${log-lib}
)
