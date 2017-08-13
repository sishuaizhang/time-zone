
### 2 时区相关概念

参考 https://www.iana.org/time-zones/repository/tz-link.html

|名词|英文|解释|英文解释|示例|
|---|---|---|---|---|
|地区名称|Zone Name(Location Name)|用一个地区最大的城市来命名一个地区,被写在IANA时区数据库中|The name is taken to be a location name corresponding to a file in the IANA Time Zone database, Each location in the tz database represents a region where all clocks keeping local time have agreed since 1970,Locations are identified by continent or ocean and then by the name of the location, which is typically the largest city within the region.  |America/New_York|
|时区ID|Time Zone ID|用地区名称表示时区ID| |America/New_York|
|时区名称|Time Zone Name|时区名称分为STD和DST|||
|时区名称简写|||the abbreviated name of the time zone (such as "CET")||
|时区UTC偏移量|||time zone's offset east of UTC.|UTC-5:30<br>UTC+0:00|
|世界协调时间|UTC|世界协调时间（又称世界标准时间、世界统一时间），是经过平均太阳时(以格林威治时间GMT为准)、地轴运动修正后的新时标以及以「秒」为单位的国际原子时所综合精算而成的时间，计算过程相当严谨精密，因此若以「世界标准时间」的角度来说，UTC比GMT来得更加精准。其误差值必须保持在0.9秒以内，若大于0.9秒则由位于巴黎的国际地球自转事务中央局发布闰秒，使UTC与地球自转周期一致。|||
|格林尼治标准时间|GMT|GMT是根据地球的自转和公转来计算时间，也就是太阳每天经过位于英国伦敦郊区的皇家格林威治天文台的时间就是中午12点|||
