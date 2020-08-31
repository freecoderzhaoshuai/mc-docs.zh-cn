---
title: geo_polygon_densify() - Azure 数据资源管理器
description: 本文介绍 Azure 数据资源管理器中的 geo_polygon_densify()。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: mbrichko
ms.service: data-explorer
ms.topic: reference
origin.date: 07/01/2020
ms.date: 08/18/2020
ms.openlocfilehash: 1a9cd6dbc535793a6ee158b96bc5ee9e24a3a996
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556523"
---
# <a name="geo_polygon_densify"></a>geo_polygon_densify()

通过添加中间点将多边形或多多边形的平面边缘转换为测地线。

## <a name="syntax"></a>语法

`geo_polygon_densify(`*polygon*`, `*tolerance*`)`

## <a name="arguments"></a>参数

* polygon：采用 [GeoJSON 格式](https://tools.ietf.org/html/rfc7946)的 [dynamic](./scalar-data-types/dynamic.md) 数据类型的多边形或多多边形。
* tolerance：一个可选数值，用于定义原始平面边缘与转换后的测地线边缘链之间的最大距离（以米为单位）。 支持的值范围为 [0.1, 10000]。 如果未指定，则使用默认值 `10`。

## <a name="returns"></a>返回

采用 [GeoJSON 格式](https://tools.ietf.org/html/rfc7946)的 [dynamic](./scalar-data-types/dynamic.md) 数据类型的致密多边形。 如果多边形或公差无效，则查询会生成 null 结果。

> [!NOTE]
> * 对按照 [WGS-84](https://earth-info.nga.mil/GandG/update/index.php?action=home) 坐标参考系统表示的地理空间坐标进行解释。
> * 必须正确定义多边形，但此函数并不检查多边形有效性。

**多边形定义**

dynamic({"type":"Polygon","coordinates": [ LinearRingShell, LinearRingHole_1 ,..., LinearRingHole_N ]})

dynamic({"type":"MultiPolygon","coordinates": [[ LinearRingShell, LinearRingHole_1 ,..., LinearRingHole_N ] ,..., [LinearRingShell, LinearRingHole_1 ,..., LinearRingHole_M]]})

* LinearRingShell 是必需的，定义为 `counterclockwise` 有序坐标数组 [[lng_1,lat_1],...,[lng_i,lat_i],...,[lng_j,lat_j],...,[lng_1,lat_1]]。 只能有一个 shell。
* LinearRingHole 是可选的，定义为 `clockwise` 有序坐标数组 [[lng_1,lat_1],...,[lng_i,lat_i],...,[lng_j,lat_j],...,[lng_1,lat_1]]。 可以有任意数量的内部环和孔。
* LinearRing 顶点必须很独特，至少有三个坐标。 第一个坐标必须等于最后一个坐标。 至少需要四个条目。
* 坐标 [经度,纬度] 必须有效。 经度必须是 [-180, +180] 范围内的实数，纬度必须是 [-90, +90] 范围内的实数。
* LinearRingShell 最多包含球体的一半。 LinearRing 将球体分成两个区域。 将选择这两个区域中较小的一个。
* LinearRing 边缘长度必须小于 180 度。 将选择两个顶点之间的最短边缘。

**约束**

* 致密多边形的最大点数限制为 10485760。
* 以 [dynamic](./scalar-data-types/dynamic.md) 格式存储多边形有大小限制。
* 致密化有效多边形可能会使其无效。 此算法以非均匀的方式添加点，因此可能导致边缘彼此缠绕。

**动机**

* [GeoJSON 格式](https://tools.ietf.org/html/rfc7946)将两点之间的边定义为直笛卡尔线。
* 是使用测地线还是平面边缘可能取决于数据集，在长边中尤其如此。

## <a name="examples"></a>示例

以下示例致密化曼哈顿中央公园多边形。 这些边缘较短，平面边缘与其对应的测地线之间的距离小于公差规定的距离。 因此，结果保持不变。

```kusto
print densified_polygon = tostring(geo_polygon_densify(dynamic({"type":"Polygon","coordinates":[[[-73.958244,40.800719],[-73.949146,40.79695],[-73.973093,40.764226],[-73.982062,40.768159],[-73.958244,40.800719]]]})))
```

|densified_polygon|
|---|
|{"type":"Polygon","coordinates":[[[-73.958244,40.800719],[-73.949146,40.79695],[-73.973093,40.764226],[-73.982062,40.768159],[-73.958244,40.800719]]]}|

以下示例致密化多边形的两条边。 致密化后的边长度约为 110 公里

```kusto
print densified_polygon = tostring(geo_polygon_densify(dynamic({"type":"Polygon","coordinates":[[[10,10],[11,10],[11,11],[10,11],[10,10]]]})))
```

|densified_polygon|
|---|
|{"type":"Polygon","coordinates":[[[10,10],[10.25,10],[10.5,10],[10.75,10],[11,10],[11,11],[10.75,11],[10.5,11],[10.25,11],[10,11],[10,10]]]}|

下面的示例由于坐标输入无效而返回 null 结果。

```kusto
print densified_polygon = geo_polygon_densify(dynamic({"type":"Polygon","coordinates":[[[10,900],[11,10],[11,11],[10,11],[10,10]]]}))
```

|densified_polygon|
|---|
||

下面的示例由于公差输入无效而返回 null 结果。

```kusto
print densified_polygon = geo_polygon_densify(dynamic({"type":"Polygon","coordinates":[[[10,10],[11,10],[11,11],[10,11],[10,10]]]}), 0)
```

|densified_polygon|
|---|
||
