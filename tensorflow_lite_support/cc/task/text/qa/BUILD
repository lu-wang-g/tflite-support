load(
    "@org_tensorflow//tensorflow/lite/core/shims:cc_library_with_tflite.bzl",
    "cc_library_with_tflite",
)

package(
    default_visibility = ["//tensorflow_lite_support:users"],
    licenses = ["notice"],  # Apache 2.0
)

exports_files([
    "bert_qa_c_api.h",
])

cc_library_with_tflite(
    name = "question_answerer",
    hdrs = [
        "question_answerer.h",
    ],
    tflite_deps = [
        "//tensorflow_lite_support/cc/task/core:base_task_api",
        "//tensorflow_lite_support/cc/task/core:tflite_engine",
    ],
)

cc_library_with_tflite(
    name = "bert_question_answerer",
    srcs = [
        "bert_question_answerer.cc",
    ],
    hdrs = [
        "bert_question_answerer.h",
    ],
    tflite_deps = [
        ":question_answerer",
        "@org_tensorflow//tensorflow/lite/core/shims:builtin_ops",
        "//tensorflow_lite_support/cc/task/core:base_task_api",
        "//tensorflow_lite_support/cc/task/core:task_api_factory",
        "//tensorflow_lite_support/cc/task/core:tflite_engine",
    ],
    deps = [
        "//tensorflow_lite_support/cc/port:status_macros",
        "//tensorflow_lite_support/cc/port:statusor",
        "//tensorflow_lite_support/cc/task/core:task_utils",
        "//tensorflow_lite_support/cc/task/text/proto:bert_question_answerer_options_proto_inc",
        "//tensorflow_lite_support/cc/text/tokenizers:bert_tokenizer",
        "//tensorflow_lite_support/cc/text/tokenizers:sentencepiece_tokenizer",
        "//tensorflow_lite_support/cc/text/tokenizers:tokenizer",
        "//tensorflow_lite_support/cc/text/tokenizers:tokenizer_utils",
        "//tensorflow_lite_support/metadata:metadata_schema_cc",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/container:flat_hash_map",
        "@com_google_absl//absl/status",
        "@com_google_absl//absl/strings",
    ],
)

cc_library_with_tflite(
    name = "bert_qa_c_api",
    srcs = [
        "bert_qa_c_api.cc",
    ],
    hdrs = [
        "bert_qa_c_api.h",
    ],
    tflite_deps = [
        ":bert_question_answerer",
        ":question_answerer",
    ],
    visibility = ["//tensorflow_lite_support:__subpackages__"],
)
