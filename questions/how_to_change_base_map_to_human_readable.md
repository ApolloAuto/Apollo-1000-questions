## How to change base_map.bin to human-readable base_map.txt`?

In apollo docker run below cmds
```shell
source scripts/apollo_base.sh

protoc --decode apollo.hdmap.Map modules/map/proto/map.proto < modules/map/data/sunnyvale_loop/base_map.bin > base_map.txt
```