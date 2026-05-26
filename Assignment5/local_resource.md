Use the same work around to load local resource as in [assignment 3](Assignment3/mongoDB_error.md). You can find the path to the binary resource by looking at the `workloads/resources.json` file. 

For example, The script look for `workload_se = obtain_resource(f"{workload_name}_x86_run")` whiel `workload_name == bfs`. Searching in `workloads/resources.json` for `bfs_x86_run` will give you the following entry:

```json
{
        "category": "binary",
        "id": "bfs-x86",
        "description": "A simple implementation of Breadth-First Search in x86 with gem5 ROI annotations",
        "resource_version": "1.0.0",
        "gem5_versions": [
            "24.1"
        ],
        "url": "file:///workspaces/virtual-memory/workloads/bfs/bfs-x86",
        "md5sum": "72530a1a9a2a45be6ee3e590dcdfa0cb"
    },
    {
        "category": "workload",
        "id": "bfs_x86_run",
        "description": "A workload that runs Breadth-First Search in x86 with gem5 ROI annotations",
        "function": "set_se_binary_workload",
        "resource_version": "1.0.0",
        "gem5_versions": [
            "24.1"
        ],
        "resources": {
            "binary": {
                "id": "bfs-x86",
                "resource_version": "1.0.0"
            }
        }
    },
```

you can then use it in your script like this:

```python
board.set_se_binary_workload(BinaryResource(local_path="workloads/bfs/bfs-x86"))
```

and if you want to pass arguments to the binary, you can do it like this:

```python
board.set_se_binary_workload(
    BinaryResource(local_path="workloads/bfs/bfs-x86")
    arguments=["64"] 
)
```