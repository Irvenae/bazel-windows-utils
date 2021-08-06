# bazel-windows-utils

Utilities for improving windows support on bazel.
Docker rules do not support windows.
Storing fixes here.

To update the puller to support windows add this to your workspace:

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_file")

```
http_file(
    name = "go_puller_windows",
    downloaded_file_path = "puller.exe",
    executable = True,
    sha256 = "7a9a8edf84de6678370f5f63d09ebab99e96bdeed1d5bb4e3d8056dacc0fec7f",
    urls = [("https://github.com/Irvenae/bazel-windows-utils/raw/main/docker/puller/puller.exe")],
)
```

The container pull repository rule can then be used as follows

```
container_pull(
        name = "xxx",
        tag = "xxx",
        registry = "xxx",
        repository = "xxx",
        puller_linux_amd64 = "@go_puller_windows//file:puller.exe",
    )
```

Next up, look into issues reading digester
