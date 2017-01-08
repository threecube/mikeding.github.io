title: 从一段问题代码说起Spark
date: 2015-12-03 22:09:13
tags: 数据处理
---
     
     val userData = sqlContext.sql( s"""Select uuid, event_type, event_time, user_id from $LOG_TABLE""")
     userData.mapPartitions(iterator => {
     iterator.map(row => {
         val (uuid, event_type, event_time, user_id) = (row(0), row(1), row(2), row(3))
         sqlContext.sql(
             s"""Select $uuid, count(*) from $LOG_TABLE
                 |Where event_time < $event_time and
                 |user_id = $user_id""".stripMargin).drop("uuid")
        })
     }).reduce((df1, df2) => df1.unionAll(df2))

2）代码解释和问题

3） RDD和任务提交过程

4） spark的框架结构

