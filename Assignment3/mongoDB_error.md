## MongoDB Error in Assignment 3
The error is due to the Atlas API endpoint being deprecated. The gem5 moved away from mongoDB, but the version pined in the assignment still uses the old API. We are working on updating the assignment, but in the meantime, you can use the following workaround to bypass the error:

Error Output:
```bash
gem5 run.py
gem5 Simulator System.  https://www.gem5.org
gem5 is copyrighted software; use the --copyright option for details.

gem5 version 24.1.0.0
gem5 compiled Dec  9 2024 21:50:01
gem5 started Apr 28 2026 23:07:08
gem5 executing on 473d740cc3fd, pid 1119
command line: gem5 run.py

info: Using config file specified by $GEM5_CONFIG
info: Using config file at /workspaces/gem5-getting-started/gem5-config.json
warn: Attempt 1 of Atlas HTTP Request failed.
Purpose of Request: Get Access Token with API key.

Failed with Exception:
HTTP Error 410: Gone

Retrying after 2 seconds...
warn: Attempt 2 of Atlas HTTP Request failed.
Purpose of Request: Get Access Token with API key.

Failed with Exception:
HTTP Error 410: Gone

Retrying after 4 seconds...
^CKeyboardInterrupt: <EMPTY MESSAGE>

At:
  src/python/gem5/resources/client_api/atlasclient.py(154): _atlas_http_json_req
  src/python/gem5/resources/client_api/atlasclient.py(94): get_token
  src/python/gem5/resources/client_api/atlasclient.py(186): get_resources
  src/python/gem5/resources/client_api/abstract_client.py(166): get_resources_by_id
  src/python/gem5/resources/client.py(330): _get_all_resources_by_id
  src/python/gem5/resources/client.py(275): _get_resource_json_obj_from_client
  src/python/gem5/resources/client.py(183): get_resource_json_obj
  src/python/gem5/resources/resource.py(958): obtain_resource
  run.py(13): <module>
  src/python/m5/main.py(675): main
root@473d740cc3fd:/workspaces/gem5-getting-started#
```

### 1. Cross compile the hello world riscv binary:
hello.c:
```c
#include <stdio.h>

int main() {
    printf("Hello world!\n");
    return 0;
}
```

compile with:
```bash
riscv64-linux-gnu-gcc -static hello.c -o hello
```
### 2. Replace the line `resource.obtain_resource()` in `run.py` with the path to the compiled binary:
```python
# from gem5.resources.resource import obtain_resource
from gem5.resources.resource import BinaryResource

# board.set_workload(obtain_resource("hello_world_workload"))
board.set_se_binary_workload(BinaryResource(local_path="hello"))
```
### 3. Run the simulation with the same command:
```bash
gem5 run.py
```
