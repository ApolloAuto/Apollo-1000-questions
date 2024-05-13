# Apollo高精度地图格式是什么？

Apollo高精度地图的格式是什么？请简要描述其特点和应用场景。

- 维护者：<daohu527@gmail.com>
- 版本：1.0.0
- 日期：05/09/2024
- 描述：

## 回答

Apollo高精度地图格式参考了[ASAM OpenDRIVE](https://www.asam.net/standards/detail/opendrive/)，针对自动驾驶的实际需求进行了优化。详细的地图格式请参考[Apollo高精度地图格式规范](https://github.com/ApolloAuto/apollo/files/12481150/EN_APOLLO_HDMap_OpenDrive_Specs_A3.0.1.pdf)。

Apollo的优化主要体现在两个方面：车道的离散化表示和车道元素的简化。

### 连续到离散

OpenDRIVE标准中，车道线分为以下几种类型：直线、螺旋线、弧线、参数三次曲线、三次多项式（已弃用）。

<a href="https://publications.pages.asam.net/standards/ASAM_OpenDRIVE/ASAM_OpenDRIVE_Specification/latest/specification/09_geometries/09_01_introduction.html"><img src="https://publications.pages.asam.net/standards/ASAM_OpenDRIVE/ASAM_OpenDRIVE_Specification/latest/specification/_images/09_geometry/geom_overview.png" width="100%"/></a>

以直线为例，通过起点坐标（x, y）、角度hdg和长度来定义，从而可以计算出直线上任意一点的坐标。

```
<planView>
    <geometry s="0.0000000000000000e+00"
              x="-4.7170752711170401e+01"
              y="7.2847983820912710e-01"
              hdg="6.5477882613167993e-01"
              length="5.7280000000000000e+01">
        <line/>
    </geometry>
</planView>
```

然而，在自动驾驶系统中，规划算法通常基于采样后的点进行工作。对于连续的曲线，这意味着需要实时进行计算，增加了系统的计算负担。为了简化这一过程，Apollo选择将车道离散化，将连续的曲线转换为一系列离散的点，这些点可以直接用于自动驾驶的规划和决策过程。

### 简化车道元素

在OpenDRIVE中，只提供了车道中心线的坐标，但车道的左右边界则需要根据车道宽度和偏移量进行计算得出。这种设计增加了地图使用的复杂性，特别是在判断自动驾驶车辆是否在车道内时，需要额外计算车道的左右边界。

<a href="https://publications.pages.asam.net/standards/ASAM_OpenDRIVE/ASAM_OpenDRIVE_Specification/latest/specification/11_lanes/11_04_lane_offset.html"><img src="https://publications.pages.asam.net/standards/ASAM_OpenDRIVE/ASAM_OpenDRIVE_Specification/latest/specification/_images/11_lanes/lanes_offset.png" width="100%"/></a>

为了简化这一过程，Apollo在地图中直接保存了每条车道的左右边界和邻接关系。这意味着，在判断自动驾驶车辆位置时，无需再进行实时计算，可以直接使用地图中存储的边界信息。这一设计显著提高了地图的易用性和效率。

基于以上2点，Apollo的高精度地图通过离散化车道和简化车道元素，为自动驾驶系统提供了更加高效、易用的地图数据支持。
