load(
    "//bazel:envoy_build_system.bzl",
    "envoy_benchmark_test",
    "envoy_cc_benchmark_binary",
    "envoy_cc_fuzz_test",
    "envoy_cc_test",
    "envoy_cc_test_library",
    "envoy_package",
    "envoy_proto_library",
    "envoy_select_enable_http3",
)

licenses(["notice"])  # Apache 2

envoy_package()

envoy_cc_test(
    name = "async_client_impl_test",
    srcs = ["async_client_impl_test.cc"],
    deps = [
        ":common_lib",
        "//source/common/buffer:buffer_lib",
        "//source/common/http:async_client_lib",
        "//source/common/http:context_lib",
        "//source/common/http:headers_lib",
        "//source/common/http:utility_lib",
        "//source/common/router:context_lib",
        "//source/extensions/upstreams/http/generic:config",
        "//test/mocks:common_lib",
        "//test/mocks/buffer:buffer_mocks",
        "//test/mocks/http:http_mocks",
        "//test/mocks/local_info:local_info_mocks",
        "//test/mocks/router:router_mocks",
        "//test/mocks/runtime:runtime_mocks",
        "//test/mocks/stats:stats_mocks",
        "//test/mocks/upstream:cluster_manager_mocks",
        "//test/test_common:test_time_lib",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
        "@envoy_api//envoy/config/route/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "async_client_utility_test",
    srcs = ["async_client_utility_test.cc"],
    deps = [
        "//source/common/http:async_client_utility_lib",
        "//test/mocks/http:http_mocks",
    ],
)

envoy_cc_test(
    name = "codec_client_test",
    srcs = ["codec_client_test.cc"],
    deps = [
        ":common_lib",
        "//source/common/buffer:buffer_lib",
        "//source/common/event:dispatcher_lib",
        "//source/common/http:codec_client_lib",
        "//source/common/http:exception_lib",
        "//source/common/network:utility_lib",
        "//source/common/stream_info:stream_info_lib",
        "//source/common/upstream:upstream_includes",
        "//source/common/upstream:upstream_lib",
        "//test/common/upstream:utility_lib",
        "//test/mocks:common_lib",
        "//test/mocks/event:event_mocks",
        "//test/mocks/http:http_mocks",
        "//test/mocks/network:network_mocks",
        "//test/mocks/ssl:ssl_mocks",
        "//test/mocks/upstream:cluster_info_mocks",
        "//test/test_common:environment_lib",
        "//test/test_common:network_utility_lib",
        "//test/test_common:utility_lib",
    ],
)

envoy_proto_library(
    name = "codec_impl_fuzz_proto",
    srcs = ["codec_impl_fuzz.proto"],
    deps = ["//test/fuzz:common_proto"],
)

envoy_cc_fuzz_test(
    name = "codec_impl_fuzz_test",
    srcs = ["codec_impl_fuzz_test.cc"],
    corpus = "codec_impl_corpus",
    deps = [
        ":codec_impl_fuzz_proto_cc_proto",
        "//source/common/http:conn_manager_lib",
        "//source/common/http:header_map_lib",
        "//source/common/http/http1:codec_lib",
        "//source/common/http/http2:codec_lib",
        "//test/common/http/http2:codec_impl_test_util",
        "//test/fuzz:utility_lib",
        "//test/mocks/http:http_mocks",
        "//test/mocks/network:network_mocks",
    ],
)

envoy_cc_test(
    name = "filter_manager_test",
    srcs = ["filter_manager_test.cc"],
    deps = [
        "//source/common/http:filter_manager_lib",
        "//test/mocks/event:event_mocks",
        "//test/mocks/http:http_mocks",
        "//test/mocks/local_reply:local_reply_mocks",
        "//test/mocks/network:network_mocks",
    ],
)

envoy_cc_test(
    name = "codec_wrappers_test",
    srcs = ["codec_wrappers_test.cc"],
    deps = [
        "//source/common/http:codec_wrappers_lib",
        "//test/mocks/http:http_mocks",
        "//test/test_common:utility_lib",
    ],
)

envoy_cc_test(
    name = "codes_test",
    srcs = ["codes_test.cc"],
    deps = [
        "//source/common/common:empty_string",
        "//source/common/http:codes_lib",
        "//source/common/http:header_map_lib",
        "//source/common/stats:stats_lib",
        "//test/mocks/stats:stats_mocks",
        "//test/test_common:utility_lib",
    ],
)

envoy_cc_benchmark_binary(
    name = "codes_speed_test",
    srcs = ["codes_speed_test.cc"],
    external_deps = [
        "benchmark",
    ],
    deps = [
        "//source/common/http:codes_lib",
        "//source/common/stats:isolated_store_lib",
        "//source/common/stats:stats_lib",
    ],
)

envoy_benchmark_test(
    name = "codes_speed_test_benchmark_test",
    benchmark_binary = "codes_speed_test",
)

envoy_cc_test_library(
    name = "common_lib",
    srcs = ["common.cc"],
    hdrs = ["common.h"],
    deps = [
        "//include/envoy/http:conn_pool_interface",
        "//include/envoy/http:header_map_interface",
        "//source/common/http:codec_client_lib",
        "//test/mocks:common_lib",
        "//test/mocks/event:event_mocks",
    ],
)

envoy_proto_library(
    name = "conn_manager_impl_fuzz_proto",
    srcs = ["conn_manager_impl_fuzz.proto"],
    deps = [
        "//test/fuzz:common_proto",
        "@envoy_api//envoy/extensions/filters/network/http_connection_manager/v3:pkg",
    ],
)

envoy_cc_fuzz_test(
    name = "conn_manager_impl_fuzz_test",
    srcs = ["conn_manager_impl_fuzz_test.cc"],
    corpus = "conn_manager_impl_corpus",
    deps = [
        ":conn_manager_impl_fuzz_proto_cc_proto",
        "//source/common/common:empty_string",
        "//source/common/http:conn_manager_lib",
        "//source/common/http:context_lib",
        "//source/common/http:date_provider_lib",
        "//source/common/http:header_utility_lib",
        "//source/common/network:address_lib",
        "//source/common/network:utility_lib",
        "//source/server:drain_manager_lib",
        "//test/fuzz:utility_lib",
        "//test/mocks/access_log:access_log_mocks",
        "//test/mocks/http:http_mocks",
        "//test/mocks/local_info:local_info_mocks",
        "//test/mocks/network:network_mocks",
        "//test/mocks/router:router_mocks",
        "//test/mocks/runtime:runtime_mocks",
        "//test/mocks/server:server_mocks",
        "//test/mocks/ssl:ssl_mocks",
        "//test/mocks/tracing:tracing_mocks",
        "//test/mocks/upstream:cluster_manager_mocks",
        "//test/test_common:simulated_time_system_lib",
        "@envoy_api//envoy/extensions/filters/network/http_connection_manager/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "conn_manager_impl_test",
    srcs = [
        # Split to avoid compiler OOM, especially on ASAN.
        "conn_manager_impl_test.cc",
        "conn_manager_impl_test_2.cc",
        "conn_manager_impl_test_base.cc",
        "conn_manager_impl_test_base.h",
    ],
    shard_count = 3,
    deps = [
        ":ip_detection_extensions_lib",
        "//source/common/http:conn_manager_lib",
        "//source/common/http:context_lib",
        "//source/extensions/access_loggers/common:file_access_log_lib",
        "//source/extensions/request_id/uuid:config",
        "//test/mocks/access_log:access_log_mocks",
        "//test/mocks/event:event_mocks",
        "//test/mocks/http:http_mocks",
        "//test/mocks/local_info:local_info_mocks",
        "//test/mocks/network:network_mocks",
        "//test/mocks/router:router_mocks",
        "//test/mocks/runtime:runtime_mocks",
        "//test/mocks/server:factory_context_mocks",
        "//test/mocks/ssl:ssl_mocks",
        "//test/test_common:delegating_route_utility_lib",
        "//test/test_common:logging_lib",
        "//test/test_common:simulated_time_system_lib",
        "//test/test_common:test_runtime_lib",
    ],
)

envoy_cc_test(
    name = "conn_manager_utility_test",
    srcs = ["conn_manager_utility_test.cc"],
    deps = [
        ":ip_detection_extensions_lib",
        "//source/common/common:random_generator_lib",
        "//source/common/event:dispatcher_lib",
        "//source/common/http:conn_manager_lib",
        "//source/common/http:headers_lib",
        "//source/common/network:address_lib",
        "//source/common/network:utility_lib",
        "//source/common/runtime:runtime_lib",
        "//source/extensions/request_id/uuid:config",
        "//test/mocks/http:http_mocks",
        "//test/mocks/local_info:local_info_mocks",
        "//test/mocks/network:network_mocks",
        "//test/mocks/runtime:runtime_mocks",
        "//test/mocks/ssl:ssl_mocks",
        "//test/mocks/upstream:upstream_mocks",
        "//test/test_common:test_runtime_lib",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/extensions/filters/network/http_connection_manager/v3:pkg_cc_proto",
        "@envoy_api//envoy/type/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "date_provider_impl_test",
    srcs = ["date_provider_impl_test.cc"],
    deps = [
        "//source/common/http:date_provider_lib",
        "//source/common/http:header_map_lib",
        "//test/mocks/event:event_mocks",
        "//test/mocks/thread_local:thread_local_mocks",
    ],
)

envoy_cc_test(
    name = "header_map_impl_test",
    srcs = ["header_map_impl_test.cc"],
    deps = [
        "//source/common/http:header_list_view_lib",
        "//source/common/http:header_map_lib",
        "//source/common/http:header_utility_lib",
        "//test/test_common:test_runtime_lib",
        "//test/test_common:utility_lib",
    ],
)

envoy_cc_benchmark_binary(
    name = "header_map_impl_speed_test",
    srcs = ["header_map_impl_speed_test.cc"],
    external_deps = [
        "benchmark",
    ],
    deps = [
        "//source/common/http:header_map_lib",
    ],
)

envoy_benchmark_test(
    name = "header_map_impl_speed_test_benchmark_test",
    benchmark_binary = "header_map_impl_speed_test",
)

envoy_proto_library(
    name = "header_map_impl_fuzz_proto",
    srcs = ["header_map_impl_fuzz.proto"],
)

envoy_cc_fuzz_test(
    name = "header_map_impl_fuzz_test",
    srcs = ["header_map_impl_fuzz_test.cc"],
    corpus = "header_map_impl_corpus",
    deps = [
        ":header_map_impl_fuzz_proto_cc_proto",
        "//source/common/http:header_map_lib",
        "//test/fuzz:utility_lib",
        "//test/test_common:test_runtime_lib",
    ],
)

envoy_cc_test(
    name = "header_utility_test",
    srcs = ["header_utility_test.cc"],
    deps = [
        "//source/common/http:header_utility_lib",
        "//test/test_common:test_runtime_lib",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/config/route/v3:pkg_cc_proto",
    ],
)

envoy_cc_test(
    name = "user_agent_test",
    srcs = ["user_agent_test.cc"],
    deps = [
        "//source/common/http:header_map_lib",
        "//source/common/http:user_agent_lib",
        "//test/mocks/stats:stats_mocks",
        "//test/test_common:simulated_time_system_lib",
        "//test/test_common:utility_lib",
    ],
)

envoy_proto_library(
    name = "utility_fuzz_proto",
    srcs = ["utility_fuzz.proto"],
    deps = ["@envoy_api//envoy/config/core/v3:pkg"],
)

envoy_cc_fuzz_test(
    name = "utility_fuzz_test",
    srcs = ["utility_fuzz_test.cc"],
    corpus = "utility_corpus",
    deps = [
        ":utility_fuzz_proto_cc_proto",
        "//source/common/http:utility_lib",
        "//test/fuzz:utility_lib",
        "//test/test_common:utility_lib",
    ],
)

envoy_cc_test(
    name = "utility_test",
    srcs = ["utility_test.cc"],
    deps = [
        "//source/common/http:exception_lib",
        "//source/common/http:header_map_lib",
        "//source/common/http:utility_lib",
        "//source/common/network:address_lib",
        "//test/mocks/http:http_mocks",
        "//test/mocks/upstream:upstream_mocks",
        "//test/test_common:test_runtime_lib",
        "//test/test_common:utility_lib",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
    ],
)

PATH_UTILITY_TEST_DEPS = [
    "//source/common/http:header_map_lib",
    "//source/common/http:path_utility_lib",
]

envoy_cc_test(
    name = "path_utility_test",
    srcs = ["path_utility_test.cc"],
    deps = PATH_UTILITY_TEST_DEPS,
)

envoy_cc_test(
    name = "legacy_path_utility_test",
    srcs = ["path_utility_test.cc"],
    args = ["--runtime-feature-disable-for-tests=envoy.reloadable_features.remove_forked_chromium_url"],
    deps = PATH_UTILITY_TEST_DEPS,
)

envoy_cc_test(
    name = "status_test",
    srcs = ["status_test.cc"],
    deps = [
        "//source/common/http:status_lib",
    ],
)

envoy_cc_test(
    name = "mixed_conn_pool_test",
    srcs = ["mixed_conn_pool_test.cc"],
    deps = [
        ":common_lib",
        "//source/common/http:mixed_conn_pool",
        "//test/common/upstream:utility_lib",
        "//test/mocks:common_lib",
        "//test/mocks/buffer:buffer_mocks",
        "//test/mocks/http:http_mocks",
        "//test/mocks/local_info:local_info_mocks",
        "//test/mocks/network:connection_mocks",
        "//test/mocks/router:router_mocks",
        "//test/mocks/runtime:runtime_mocks",
        "//test/mocks/stats:stats_mocks",
    ],
)

# TODO(alyssawilk): The conn pool grid should work correctly without H3. Circle back and figure
# out the right way of handling the lack of H3 in the build.
envoy_cc_test(
    name = "conn_pool_grid_test",
    srcs = envoy_select_enable_http3(["conn_pool_grid_test.cc"]),
    deps = envoy_select_enable_http3([
        ":common_lib",
        "//source/common/http:conn_pool_grid",
        "//test/common/upstream:utility_lib",
        "//test/mocks:common_lib",
        "//test/mocks/buffer:buffer_mocks",
        "//test/mocks/http:http_mocks",
        "//test/mocks/ssl:ssl_mocks",
        "//test/mocks/local_info:local_info_mocks",
        "//test/mocks/network:connection_mocks",
        "//test/mocks/router:router_mocks",
        "//test/mocks/runtime:runtime_mocks",
        "//test/mocks/stats:stats_mocks",
        "//source/common/quic:quic_factory_lib",
        "//source/common/quic:quic_transport_socket_factory_lib",
        "//source/common/quic:client_connection_factory_lib",
    ]),
)

envoy_cc_test(
    name = "http3_status_tracker_test",
    srcs = ["http3_status_tracker_test.cc"],
    deps = [
        ":common_lib",
        "//source/common/http:http3_status_tracker",
        "//test/mocks:common_lib",
    ],
)

envoy_cc_test(
    name = "alternate_protocols_cache_impl_test",
    srcs = ["alternate_protocols_cache_impl_test.cc"],
    deps = [
        ":common_lib",
        "//source/common/http:alternate_protocols_cache",
        "//test/mocks:common_lib",
        "//test/test_common:simulated_time_system_lib",
    ],
)

envoy_proto_library(
    name = "path_utility_fuzz_proto",
    srcs = ["path_utility_fuzz.proto"],
    deps = [
        "//test/fuzz:common_proto",
    ],
)

envoy_cc_fuzz_test(
    name = "path_utility_fuzz_test",
    srcs = ["path_utility_fuzz_test.cc"],
    corpus = "path_utility_corpus",
    deps = [
        ":path_utility_fuzz_proto_cc_proto",
        "//source/common/http:header_map_lib",
        "//source/common/http:path_utility_lib",
        "//test/fuzz:utility_lib",
    ],
)

envoy_cc_test_library(
    name = "ip_detection_extensions_lib",
    srcs = ["ip_detection_extensions.cc"],
    hdrs = ["ip_detection_extensions.h"],
    deps = [
        "//source/extensions/http/original_ip_detection/custom_header:custom_header_lib",
        "//source/extensions/http/original_ip_detection/xff:xff_lib",
    ],
)
