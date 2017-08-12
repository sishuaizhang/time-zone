# 时区（time-zone）常见问题总结

### 1 经纬度换夏令时时区

给定经纬度，得出包含夏令时信息的UTC 偏移量

#### 1.1 `经纬度`到`时区ID`的转换

由 http://efele.net/maps/tz/(不再维护)，https://github.com/evansiroky/timezone-boundary-builder 提供的`经纬度`到`时区ID`的转换数据(由于不同国家政治策略的变动，这个数据经常更新) 

https://github.com/bradfitz/latlong (golang的库)

如：   (42.7235, -73.6931)   ---->   America/New_York

#### 1.2 `时区ID`到`具体夏令时偏移量`的转换

由 http://www.iana.org/time-zones 提供`时区ID`到`具体夏令时偏移量`的转换数据(由于不同国家政治策略的变动，这个数据经常更新)(有golang标准库)

https://golang.org/pkg/time/#LoadLocation

https://www.iana.org/time-zones/repository/tz-link.html  https://www.iana.org/time-zones/repository/releases/tzdb-2017b.tar.lz  https://github.com/eggert/tz

如    America/New_York +  2016年12月26日  -->  UTC - 5:00
       America/New_York +  2016年10月26日  -->  UTC - 4:00

```golang
    location, _:= time.LoadLocation("America/New_York")
    zone, offset := time.Now().In(location).Zone()
```
