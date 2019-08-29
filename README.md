# 时区（time-zone）常见问题总结

### 1 概念

https://github.com/sishuai/time-zone/blob/master/time-zone-concept.md

#### 1.1 时区列表

https://www.ibm.com/support/knowledgecenter/en/SSAW57_8.5.5/com.ibm.websphere.nd.multiplatform.doc/ae/rrun_svr_timezones.html

https://en.wikipedia.org/wiki/List_of_time_zone_abbreviations

https://en.wikipedia.org/wiki/List_of_tz_database_time_zones

https://en.wikipedia.org/wiki/Lists_of_time_zones


### 2 经纬度换时区

给定`经纬度`得出`时区名称`和`具体时区UTC偏移量`

https://github.com/go-utils/utils/ 的GetTimeZoneByLatlong方法(golang库)

#### 2.1 `经纬度`到`时区ID`的转换

如：

(42.7235, -73.6931)   ---->   America/New_York [Location Name]

有 http://efele.net/maps/tz/(不再维护)，https://github.com/evansiroky/timezone-boundary-builder 提供的`经纬度`到`时区ID`的转换数据(由于不同国家政治策略的变动，这个数据经常更新) 

各语言的库 https://github.com/evansiroky/timezone-boundary-builder#lookup-libraries



#### 2.2 `时区ID`到`具体夏令时偏移量`的转换

如： 

America/New_York +  2016年12月26日  -->  UTC - 5:00

America/New_York +  2016年10月26日  -->  UTC - 4:00 

有 http://www.iana.org/time-zones 提供`时区ID`到`具体夏令时偏移量`的转换数据(由于不同国家政治策略的变动，这个数据经常更新)(有golang标准库)

https://golang.org/pkg/time/#LoadLocation

https://github.com/golang/go/tree/release-branch.go1.4/lib/time


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


