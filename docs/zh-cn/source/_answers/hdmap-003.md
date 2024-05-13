# 如何将二进制（bin）格式的地图转换为文本（txt）格式？

二进制格式地图和文本格式地图的区别是什么？它们之间如何相互转换？

- 维护者：<daohu527@gmail.com>
- 版本：1.0.0
- 日期：05/09/2024
- 描述：

## 回答

Apollo高精度地图主要基于protobuf协议进行实现，其存储方式支持两种文件格式：bin和txt。

- **bin格式** 是一种紧凑型的文件格式，其优势在于能够显著减少文件的大小，从而减少存储和传输的开销。然而，由于它是二进制编码，因此无法直接通过文本编辑器进行阅读。

- **txt格式** 是基于文本的存储方式，使得地图数据可以直观地以文本形式展现，便于开发人员查看和调试。然而，这种格式会占用较大的存储空间，并且传输效率相对较低。

在实际应用中，为了确保地图数据的高效存储和传输，Apollo系统通常选择使用bin格式进行地图的保存和加载。而txt格式则主要作为调试和查看的辅助手段，方便开发人员理解和验证地图数据。

### 二进制（bin）转文本（txt）

1. 安装protoc

安装protoc，参考[Installing protoc](https://google.github.io/proto-lens/installing-protoc.html)。

2. 运行命令

```shell
# modules/map/data/borregas_ave/base_map.bin（替换为你想要转换的地图）

protoc --decode apollo.hdmap.Map modules/map/proto/map.proto < modules/map/data/borregas_ave/base_map.bin > base_map.txt
```

3. 转换后的地图文件`base_map.txt`保存在当前工作目录下。

### 文本（txt）转二进制（bin）

1. 安装protoc

同上。

2. 运行命令

```shell
# modules/map/data/demo/base_map.txt（替换为你想要转换的地图）

protoc --encode apollo.hdmap.Map modules/map/proto/map.proto < modules/map/data/demo/base_map.txt > base_map.bin
```

3. 转换后的地图文件`base_map.bin`保存在当前工作目录下。
