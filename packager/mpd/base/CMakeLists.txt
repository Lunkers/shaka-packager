add_proto_library(media_info_proto STATIC
    media_info.proto
)

add_library(manifest_base STATIC
    bandwidth_estimator.cc
)

add_library(mpd_builder STATIC
    adaptation_set.cc
    content_protection_element.cc
    mpd_builder.cc
    mpd_notifier_util.cc
    mpd_notifier.h
    mpd_options.h
    mpd_utils.cc
    period.cc
    representation.h
    segment_info.h
    simple_mpd_notifier.cc
)


# TODO: add libraries (absl, etc)
target_link_libraries(mpd_builder
    file
    media_base
    version
    libxml2
    manifest_base
    media_info_proto
    absl::strings
    absl::synchronization
    absl::flags
    absl::str_format
    glog
)

add_library(mpd_mocks STATIC
    mock_mpd_builder.cc
    mock_mpd_notifier.cc
)

target_link_libraries(mpd_mocks
    gmock
    mpd_builder
)

add_executable(mpd_base_unittest
    adaptation_set_unittest.cc
    bandwidth_estimator_unittest.cc
    mpd_builder_unittest.cc
    mpd_utils_unittest.cc
    period_unittest.cc
    representation_unittest.cc
    simple_mpd_notifier_unittest.cc
)

target_link_libraries(mpd_base_unittest
    file
    media_base
    mpd_builder
    mpd_mocks
    gtest
    gflags
    glog
)

add_test(NAME mpd_base_unittest COMMAND mpd_base_unittest)

add_subdirectory(xml)