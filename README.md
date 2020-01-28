![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        

# Use SQL To Find Full Scans, User Scans, Seeks Per Database Per Table
**Post Date: May 6, 2014**        



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process

<p>Here's a quick script to show you the User Scans, User Seeks, etc per Database, Per table.</p>  



## SQL-Logic
```SQL
use MyDatabaseName;
set nocount on
select
distinct
--'database' = db_name(sddius.database_id),
'table' = so.name
, 'index' = si.name
, sddius.user_seeks
, sddius.user_scans
, 'last_user_seek' = convert(char, sddius.last_user_seek, 9)
, 'last_user_scan' = convert(char, sddius.last_user_scan, 9)
from
sys.objects so join sys.indexes si on si.object_id = so.object_id
left outer join sys.dm_db_index_usage_stats sddius on si.index_id = sddius.index_id
where
db_name(sddius.database_id) is not null
and sddius.database_id &gt; 4
and user_scans &gt; 5
and so.type = 'u' and si.type_desc &lt;&gt; 'heap'
and last_user_scan &gt; (select getdate() - 5)
```


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

   
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

