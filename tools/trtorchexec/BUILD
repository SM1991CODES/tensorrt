package(default_visibility = ["//visibility:public"])

cc_binary(
    name = "trtorchexec",
    srcs = [
        "main.cpp",
    ],
    deps = [
        "//cpp:torch_tensorrt",
        "@libtorch",
        "@libtorch//:caffe2",
    ],
)
