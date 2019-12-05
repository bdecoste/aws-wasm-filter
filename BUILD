licenses(["notice"])  # Apache 2

proto_library(
    name = "filter_proto",
    srcs = [
        "filter.proto",
    ],
)

cc_proto_library(
    name = "filter_cc_proto",
    deps = [":filter_proto"],
)

cc_library(
    name = "aws_authenticator_lib",
    srcs = ["aws_authenticator.cc"],
    hdrs = ["aws_authenticator.h"],
    deps = [
        "@envoy_wasm_api//include/envoy/buffer:buffer_interface",
        "@envoy_wasm_api//include/envoy/http:header_map_interface",
        "@envoy_wasm_api//source/common/common:assert_lib",
        "@envoy_wasm_api//source/common/common:empty_string",
        "@envoy_wasm_api//source/common/common:hex_lib",
        "@envoy_wasm_api//source/common/http:headers_lib",
        "@envoy_wasm_api//source/common/http:utility_lib",
    ],
)

cc_library(
    name = "aws_lambda_filter_lib",
    srcs = [
        "aws_lambda_filter.cc",
    ],
    hdrs = [
        "aws_lambda_filter.h",
    ],
    deps = [
        ":aws_authenticator_lib",
        ":config_lib",
        "@envoy_wasm_api//api/envoy/config/filter/http/aws_lambda/v2:pkg_cc_proto",
        "@envoy_wasm_api//source/common/http:solo_filter_utility_lib",
        "@envoy_wasm_api//source/extensions/filters/http:solo_well_known_names",
        "@envoy_wasm_api//source/common/http:utility_lib",
    ],
)

cc_binary(
    name = "filter.wasm",
    srcs = [
        "config.cc",
	"config.h"
    ],
    deps = [
        ":aws_authenticator_lib",
        "@envoy_wasm_api//api/envoy/config/filter/http/aws_lambda/v2:pkg_cc_proto",
        "@envoy_wasm_api//source/common/http:solo_filter_utility_lib",
        "@envoy_wasm_api//source/extensions/filters/http:solo_well_known_names",
        "@envoy_wasm_api//source/common/http:utility_lib",
        "@envoy_wasm_api//source/extensions/filters/http/common/aws:credentials_provider_impl_lib",
        "@envoy_wasm_api//source/extensions/filters/http/common/aws:credentials_provider_interface",
        "@envoy_wasm_api//source/extensions/filters/http/common/aws:utility_lib",
    ],
)

cc_library(
    name = "aws_lambda_filter_config_lib",
    srcs = ["aws_lambda_filter_config_factory.cc"],
    hdrs = ["aws_lambda_filter_config_factory.h"],
    deps = [
        ":aws_lambda_filter_lib",
        "@envoy_wasm_api//include/envoy/registry",
        "@envoy_wasm_api//include/envoy/server:filter_config_interface",
        "@envoy_wasm_api//source/extensions/filters/http/common:factory_base_lib",
    ],
)
