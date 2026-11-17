# data_climate

中国区域气候与太阳辐射栅格数据集（GeoTIFF，月度）。

## 数据下载

14 GB 原始数据不在 git 中，请从 Releases 页面下载：

**https://github.com/tricia1353/data_climate/releases/latest**

| Release 附件 | 内容 | 数量 |
| --- | --- | --- |
| `solar_radiation_*.zip` | 太阳辐射月度栅格，2007–2020（14 年 × 12 月） | 14 个压缩包 / 168 个 tif |
| `temperature_*.zip` | 气温月度栅格，2006–2020（15 年） | 8 个压缩包 / 176 个 tif |

合计 344 个 GeoTIFF 文件，解压后约 14 GB。

## 文件命名

```
<variable>_<year>_<month>.tif
```

| 变量 | 说明 | 单文件大小 | 时间范围 |
| --- | --- | --- | --- |
| `solar_radiation` | 太阳辐射（月度栅格） | 约 20 MB | 2007-01 – 2020-12（完整 168 个月） |
| `temperature` | 气温（月度栅格） | 约 65 MB | 2006-01 – 2020-12（部分月份缺失） |

缺失月份：`temperature_2006` 缺 2 个月，`temperature_2011` 缺 2 个月，`temperature_2015` 缺 1 个月。

## 使用示例

```python
import rasterio
import glob

# 解压后按年份读取
for path in sorted(glob.glob("temperature_2020_*.tif")):
    with rasterio.open(path) as src:
        arr = src.read(1)
        print(path, arr.shape, src.crs, src.bounds)
```

```python
# 或者直接用 xarray
import xarray as xr
ds = xr.open_rasterio("solar_radiation_2020_07.tif")
```

## 仓库结构

```
.
├── README.md        # 本文件
├── MANIFEST.txt     # 全部 344 个 tif 文件清单
└── .gitignore       # 忽略 *.zip / *.tif
```

## 许可

数据来源与使用许可由数据提供方决定，使用前请确认原始来源的授权条款。
