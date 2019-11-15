![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 在SysJobSteps中转换Last_Run_Date和Last_Run_TIme
#### Convert Last_Run_Date And Last_Run_TIme in SysJobSteps
**TIME STAMP**

![#](images/convert-last-run-date-and-last-run-time-in-sysjobs-a.png?raw=true "#")

## Contents

- [中文](#中文) 
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
如果你发现了这篇文章，你可能希望从msdb..sysjobsteps表中的last_run_date和last_run_time列中获取更多的信息。以下是一个快速转换。我做了一个你也可以用在其他函数中的用来表述日期/时间的基本转换。它是“last run literal”，然后我再转换为使用日期名称函数推断日期名称，然后再次转换为缩写的月/日/年和时间。

## English
If you found this post… You probably want to make more sense out of the last_run_date, and last_run_time columns from the msdb..sysjobsteps table. Here is a quick conversion for you. I did a basic conversion to formulate a date/time you could use in other functions. It’s the “last run literal”, then I converted again to extrapolate the Day name using the datename function, and then once more to get an abbreviated Month/Day/Year & time.

---
## Logic
```SQL
-- 使用以下代码来获取有关你的作业和步骤的所有步骤信息和上次运行记录。
--	use this to get all step info about your job, and steps, including last run history.
select
 'job name' = sj.name
, 'step id' = sjs.step_id
, 'step name' = sjs.step_name
, 'last run literal' = dateadd(millisecond, sjs.last_run_time,convert(datetime,cast(nullif(sjs.last_run_date,0) as nvarchar(10))))
, 'last run day' = datename(dw, dateadd(millisecond, sjs.last_run_time,convert(datetime,cast(nullif(sjs.last_run_date,0) as nvarchar(10)))))
, 'last run date' = convert(char, dateadd(millisecond, sjs.last_run_time,convert(datetime,cast(nullif(sjs.last_run_date,0) as nvarchar(10)))), 9)
from
 msdb..sysjobs sj join msdb..sysjobsteps sjs on sj.job_id = sjs.job_id
order by
 sj.name, sjs.step_id asc


```

![#](images/convert-last-run-date-and-last-run-time-in-sysjobs-b.png?raw=true "#")


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

