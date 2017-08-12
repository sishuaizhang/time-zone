# 时区（time-zone）常见问题总结

### 1 概念

参考 https://www.iana.org/time-zones/repository/tz-link.html

|名词|英文|解释|英文解释|示例|
|---|---|---|---|---|
|地区名称|Zone Name(Location Name)|用一个地区最大的城市来命名一个地区,被写在IANA时区数据库中|The name is taken to be a location name corresponding to a file in the IANA Time Zone database, Each location in the tz database represents a region where all clocks keeping local time have agreed since 1970,Locations are identified by continent or ocean and then by the name of the location, which is typically the largest city within the region.  |America/New_York|
|时区ID|Time Zone ID|用地区名称表示时区ID| |America/New_York|
|时区名称简写|Time Zone Name|时区名称分为STD和DST|||
|时区名称简写|||the abbreviated name of the time zone (such as "CET")||
|时区UTC偏移量|||time zone's offset east of UTC.|UTC-5:30,UTC+0:00|
|世界协调时间|UTC|世界协调时间（又称世界标准时间、世界统一时间），是经过平均太阳时(以格林威治时间GMT为准)、地轴运动修正后的新时标以及以「秒」为单位的国际原子时所综合精算而成的时间，计算过程相当严谨精密，因此若以「世界标准时间」的角度来说，UTC比GMT来得更加精准。其误差值必须保持在0.9秒以内，若大于0.9秒则由位于巴黎的国际地球自转事务中央局发布闰秒，使UTC与地球自转周期一致。|||
|格林尼治标准时间|GMT|GMT是根据地球的自转和公转来计算时间，也就是太阳每天经过位于英国伦敦郊区的皇家格林威治天文台的时间就是中午12点|||



### 2 经纬度换时区

给定`经纬度`得出`时区名称`和`具体时区UTC偏移量`

https://github.com/go-utils/utils/ 的GetTimeZoneByLatlong方法(golang库)

#### 2.1 `经纬度`到`时区ID`的转换

如：

(42.7235, -73.6931)   ---->   America/New_York [Location Name]

有 http://efele.net/maps/tz/(不再维护)，https://github.com/evansiroky/timezone-boundary-builder 提供的`经纬度`到`时区ID`的转换数据(由于不同国家政治策略的变动，这个数据经常更新) 

https://github.com/darkskyapp/tz-lookup (nodejs库) [2017a]

https://github.com/go-utils/tzlookup (golang的库)  [2017a]

https://github.com/bradfitz/latlong (golang的库)   [2016d]


#### 2.2 `时区ID`到`具体夏令时偏移量`的转换

如： 

America/New_York +  2016年12月26日  -->  UTC - 5:00

America/New_York +  2016年10月26日  -->  UTC - 4:00 

有 http://www.iana.org/time-zones 提供`时区ID`到`具体夏令时偏移量`的转换数据(由于不同国家政治策略的变动，这个数据经常更新)(有golang标准库)

https://golang.org/pkg/time/#LoadLocation

```golang
package main

import (
	"fmt"
	"time"

	"github.com/bradfitz/latlong"
)

func main() {

	location, _ := time.LoadLocation(latlong.LookupZoneName(42.7235, -73.6931))
	zone, offset := time.Now().In(location).Zone()

	fmt.Print(zone, "\n")
	fmt.Print(offset / 3600)
}

//std out
//EDT
//-4
```

https://www.iana.org/time-zones/repository/tz-link.html

https://www.iana.org/time-zones/repository/releases/tzdb-2017b.tar.lz

https://github.com/eggert/tz

