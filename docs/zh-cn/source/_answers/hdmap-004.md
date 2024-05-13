# 如何转换OpenDRIVE格式地图到Apollo格式地图?

如何将这2种地图格式进行相互转换？

- 维护者：<daohu527@gmail.com>
- 版本：1.0.0
- 日期：05/09/2024
- 描述：

## 回答

以下是2种地图格式的转换方法。

### OpenDRIVE转Apollo

可以使用[imap](https://github.com/daohu527/imap)工具来转换OpenDRIVE格式地图到Apollo格式地图。

1. 安装imap

```shell
pip3 install imap_box
```

2. 转换格式

```shell
# data/town.xodr (OpenDRIVE格式地图)
# data/apollo_map.txt (Apollo格式地图)
imap -f -i data/town.xodr -o data/apollo_map.txt
```

### Apollo转OpenDRIVE

Todo：目前没有相应的转换工具
